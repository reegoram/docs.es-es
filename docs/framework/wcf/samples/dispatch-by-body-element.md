---
title: "Distribuci&#243;n mediante el elemento del cuerpo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f64a3c04-62b4-47b2-91d9-747a3af1659f
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Distribuci&#243;n mediante el elemento del cuerpo
Este ejemplo muestra cómo implementar un algoritmo alternativo para asignar mensajes entrantes a las operaciones.  
  
 De forma predeterminada, el servicio del distribuidor ejemplar selecciona el método de control adecuado para un mensaje entrante basado en el encabezamiento “Acción” del direccionamiento del WS del mensaje o la información equivalente en la solicitud SOAP del Http.  
  
 Algunas pilas de servicios Web del SOAP 1.1 que no siguen las instrucciones del WS\-I Basic Profile 1.1 no envían mensajes basados en el URI Acción, sino basados en el nombre completo de XML del primer elemento dentro del cuerpo de SOAP.  Igualmente, la parte del cliente de estas pilas podría enviar los mensajes con un encabezado de Http SoapAction vacío o arbitrario, el cual se permitió por la especificación SOAP 1.1.  
  
 Para cambiar la manera en la cual se envían los mensajes a los métodos, el ejemplo implementa la interfaz de extensibilidad <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> en `DispatchByBodyElementOperationSelector`.  Esta clase selecciona operaciones basadas en el primer elemento del cuerpo del mensaje.  
  
 El constructor de clase espera un diccionario lleno con pares de `XmlQualifiedName` y cadenas, con los que los nombres completos indiquen el nombre del primer elemento secundario del cuerpo de SOAP y que las cadenas indiquen el nombre de la operación correspondiente.  `defaultOperationName` es el nombre de la operación que recibe todos los mensajes que no pueden coincidir contra este diccionario:  
  
```  
class DispatchByBodyElementOperationSelector : IDispatchOperationSelector  
{  
    Dictionary<XmlQualifiedName, string> dispatchDictionary;  
    string defaultOperationName;  
  
    public DispatchByBodyElementOperationSelector(Dictionary<XmlQualifiedName,string> dispatchDictionary, string defaultOperationName)  
    {  
        this.dispatchDictionary = dispatchDictionary;  
        this.defaultOperationName = defaultOperationName;  
    }  
```  
  
 Las implementaciones de <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> son muy sencillas de generar ya que solo existe un método en la interfaz: <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A>.  El trabajo de este método es inspeccionar un mensaje entrante y devolver una cadena que iguala el nombre de un método en el contrato de servicios para el extremo actual.  
  
 En este ejemplo, el selector de la operación adquiere <xref:System.Xml.XmlDictionaryReader> para el cuerpo del mensaje entrante utilizando <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>.  Este método ya coloca al lector en el primer elemento secundario del cuerpo del mensaje para que sea suficiente obtener el nombre del elemento vigente y el espacio de nombres URI y combinarlos en `XmlQualifiedName` que se utiliza a continuación para buscar la operación correspondiente del diccionario contenida por el selector de la operación.  
  
```  
public string SelectOperation(ref System.ServiceModel.Channels.Message message)  
{  
    XmlDictionaryReader bodyReader = message.GetReaderAtBodyContents();  
    XmlQualifiedName lookupQName = new  
       XmlQualifiedName(bodyReader.LocalName, bodyReader.NamespaceURI);  
    message = CreateMessageCopy(message,bodyReader);  
    if (dispatchDictionary.ContainsKey(lookupQName))  
    {  
         return dispatchDictionary[lookupQName];  
    }  
    else  
    {  
        return defaultOperationName;  
    }  
}  
```  
  
 Tener acceso al cuerpo del mensaje con <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> o cualquiera de los otros métodos que proporcionan el acceso al contenido del cuerpo del mensaje produce que el mensaje marque como "lectura", que significa que el mensaje no es válido para cualquier otro procesamiento.  Por consiguiente, el selector de la operación crea una copia del mensaje entrante con el método mostrado en el código siguiente.  Dado que la posición del lector no se ha cambiado durante la inspección, el mensaje recientemente creado en el que se copian las propiedades de mensaje y los encabezados del mensaje también, lo que resulta en un en un clon exacto del mensaje original:  
  
```  
  
private Message CreateMessageCopy(Message message,   
                                     XmlDictionaryReader body)  
{  
    Message copy = Message.CreateMessage(message.Version,message.Headers.Action,body);  
    copy.Headers.CopyHeaderFrom(message,0);  
    copy.Properties.CopyProperties(message.Properties);  
    return copy;  
}  
  
```  
  
## Agregar un selector de operación a un servicio  
 Los selectores de operación de la expedición de servicio son las extensiones al distribuidor [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Para seleccionar los métodos en el canal de devolución de llamada de contratos dúplex, hay también selectores de operación de cliente que trabajan de manera muy similar a los selectores de operación de expedición aquí, pero que no se cubren explícitamente en este ejemplo.  
  
 Como la mayoría de las extensiones ejemplares de los servicios, los selectores de la operación de expedición se agregan al distribuidor utilizando los comportamientos.  Un *comportamiento* es un objeto de configuración, que o bien agrega una o más extensiones a la expedición en tiempo de ejecución \(o al tiempo de ejecución del cliente\) o de lo contrario cambia sus valores.  
  
 Dado que los selectores de la operación tienen el ámbito del contrato, el comportamiento adecuado para implementar aquí es <xref:System.ServiceModel.Description.IContractBehavior>.  Dado que la interfaz se implementa como se muestra en una clase derivada <xref:System.Attribute> en el código siguiente, el comportamiento se puede agregar mediante declaración a cualquier contrato de servicios.  Cuando se abre un<xref:System.ServiceModel.ServiceHost> y el tiempo de ejecución de la expedición está generado, todos los comportamientos buscados, bien como atributos en los contratos, operaciones o implementaciones del servicio, o bien como elemento en la configuración del servicio se agregan automáticamente y como consecuencia solicitan contribuir con las extensiones o modificar la configuración predeterminada.  
  
 Para ser breve, el fragmento de código siguiente muestra solo la implementación del método <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%2A>, que realiza los cambios de configuración para el distribuidor en este ejemplo.  No se muestran los otros métodos porque vuelven al llamador sin hacer ningún trabajo.  
  
```  
[AttributeUsage(AttributeTargets.Class|AttributeTargets.Interface)]  
class DispatchByBodyElementBehaviorAttribute : Attribute, IContractBehavior  
{  
    // public void AddBindingParameters(...)   
    // public void ApplyClientBehavior(...)  
    // public void Validate(...)  
```  
  
 Primero, la implementación <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%2A> prepara el diccionario de búsqueda para el selector de la operación procesa una iteración sobre los elementos <xref:System.ServiceModel.Description.OperationDescription> en <xref:System.ServiceModel.Description.ContractDescription>del extremo de servicio.  A continuación, cada descripción de la operación se inspecciona para la presencia del comportamiento `DispatchBodyElementAttribute`, una implementación de <xref:System.ServiceModel.Description.IOperationBehavior> que también se define en este ejemplo.  Aunque esta clase también es un comportamiento, es pasivo y no contribuye activamente con ningún cambio de configuración a la expedición en tiempo de ejecución.  Todos sus métodos vuelven al llamador sin tomar ninguna medida.  El comportamiento de la operación solo existe para que los metadatos exigidos para el nuevo mecanismo de la expedición, a saber, el nombre completo del cuerpo del elemento en cuya aparición se selecciona una operación, puedan estar asociados a las operaciones respectivas.  
  
 Si se busca este tipo de comportamiento, un par de valor creado a partir del nombre completo de XML \(propiedad`QName` \) y el nombre de la operación \(propiedad`Name` \) se agrega al diccionario.  
  
 Una vez rellenado el diccionario, un nuevo `DispatchByBodyElementOperationSelector` se construye con esta información y se establece como el selector de la operación de la expedición en tiempo de ejecución:  
  
```  
public void ApplyDispatchBehavior(ContractDescription contractDescription, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.DispatchRuntime dispatchRuntime)  
{  
    Dictionary<XmlQualifiedName,string> dispatchDictionary =   
                     new Dictionary<XmlQualifiedName,string>();  
    foreach( OperationDescription operationDescription in   
                              contractDescription.Operations )  
    {  
        DispatchBodyElementAttribute dispatchBodyElement =   
   operationDescription.Behaviors.Find<DispatchBodyElementAttribute>();  
        if ( dispatchBodyElement != null )  
        {  
             dispatchDictionary.Add(dispatchBodyElement.QName,   
                              operationDescription.Name);  
        }  
    }  
    dispatchRuntime.OperationSelector =   
            new DispatchByBodyElementOperationSelector(  
               dispatchDictionary,   
               dispatchRuntime.UnhandledDispatchOperation.Name);  
    }  
}  
```  
  
## Implementar el servicio  
 El comportamiento implementado directamente en este ejemplo afecta a cómo se interpretan los mensajes de la conexión y los envían, lo cual es una función del contrato de servicios.  Por consiguiente, el comportamiento se debería declarar en el nivel del contrato de servicios en cualquier implementación del servicio que decida utilizarlo.  
  
 El servicio del proyecto del ejemplo aplica el comportamiento del contrato `DispatchByBodyElementBehaviorAttribute` al contrato de servicios `IDispatchedByBody` y etiqueta cada uno de las dos operaciones, `OperationForBodyA()`  y `OperationForBodyB()`, con un comportamiento de operación `DispatchBodyElementAttribute`.  Cuando se abre un host del servicio para un servicio que implementa este contrato, este metadato lo escoge previamente el generador del distribuidor, tal y como se ha descrito previamente.  
  
 Dado que el selector de la operación se envía solamente basado en el elemento de cuerpo del mensaje y omite la "Acción", para indicar el tiempo de ejecución se exige no comprobar el encabezado "Acción" en las respuestas devueltas asignando el carácter comodín "\*" a la propiedad `ReplyAction` de <xref:System.ServiceModel.OperationContractAttribute>.  Además, se exige tener una operación predeterminada que haya establecido la propiedad “Acción” para el comodín "\*."  La operación predeterminada recibe todos los mensajes que no se pueden enviar y no tienen `DispatchBodyElementAttribute`:  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"),  
                            DispatchByBodyElementBehavior]  
public interface IDispatchedByBody  
{  
    [OperationContract(ReplyAction="*"),   
     DispatchBodyElement("bodyA","http://tempuri.org")]  
    Message OperationForBodyA(Message msg);  
    [OperationContract(ReplyAction = "*"),   
     DispatchBodyElement("bodyB", "http://tempuri.org")]  
    Message OperationForBodyB(Message msg);  
    [OperationContract(Action="*", ReplyAction="*")]  
    Message DefaultOperation(Message msg);  
}  
```  
  
 La implementación de servicio de ejemplo es sencilla.  Cada método ajusta el mensaje recibido en un mensaje de respuesta y lo devuelve al cliente.  
  
## Ejecutar y compilar el ejemplo  
 Al ejecutar el ejemplo, el contenido del cuerpo de las respuestas de la operación se muestra en la ventana de la consola del cliente de una manera parecida al resultado siguiente \(formateado\).  
  
 El cliente envía tres mensajes al servicio cuyo elemento de contenido de cuerpo se denomina `bodyA`, `bodyB`y `bodyX`, respectivamente.  Como se puede diferir de la descripción anterior y el contrato de servicios mostrado, el mensaje entrante con el elemento `bodyA` se envía al método `OperationForBodyA()`.  Dado que no hay ningún destino de la expedición explícito para el mensaje con el cuerpo del elemento `bodyX`, el mensaje se envía a `DefaultOperation()`.  Cada una de las operaciones de servicio contiene el cuerpo del mensaje recibido en un elemento concreto al método y vuelve a él, lo cual se hace para poner en correlación claramente los mensajes de entrada y salida para obtener este ejemplo:  
  
```  
<?xml version="1.0" encoding="IBM437"?>  
<replyBodyA xmlns="http://tempuri.org">  
   <q:bodyA xmlns:q="http://tempuri.org">test</q:bodyA>  
</replyBodyA>  
<?xml version="1.0" encoding="IBM437"?>  
<replyBodyB xmlns="http://tempuri.org">  
  <q:bodyB xmlns:q="http://tempuri.org">test</q:bodyB>  
</replyBodyB>  
<?xml version="1.0" encoding="IBM437"?>  
<replyDefault xmlns="http://tempuri.org">  
   <q:bodyX xmlns:q="http://tempuri.org">test</q:bodyX>  
</replyDefault>  
  
```  
  
#### Configurar, compilar y ejecutar el ejemplo  
  
1.  Asegúrese de realizar el procedimiento de [Procedimiento de instalación única para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Para compilar la solución, siga las instrucciones de [Compilación de los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Para ejecutar el ejemplo en una configuración con un único equipo o con varios, siga las instrucciones de [Ejecución de los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.  Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Interop\AdvancedDispatchByBody`  
  
## Vea también