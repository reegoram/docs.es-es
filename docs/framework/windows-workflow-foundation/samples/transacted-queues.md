---
title: "Colas de transacci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1b011dd-5e0b-482c-9bb0-9d8727038f14
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Colas de transacci&#243;n
En este ejemplo se muestra cómo integrar colas y transacciones en [!INCLUDE[wf](../../../../includes/wf-md.md)] para crear servicios escalables y fiables.<xref:System.Activities.TransactionScope> se utiliza en el flujo de trabajo del cliente para enviar el mensaje a una cola en una transacción mediante <xref:System.ServiceModel.NetMsmqBinding>.<xref:System.ServiceModel.Activities.TransactedReceiveScope> se utiliza en el servidor para recibir mensajes de la cola y actualizar el estado del flujo de trabajo en la misma transacción.  
  
## Demostraciones  
 <xref:System.Activities.Statements.TransactionScope>, <xref:System.ServiceModel.Activities.TransactedReceiveScope>, <xref:System.ServiceModel.NetMsmqBinding>, <xref:System.ServiceModel.Activities.Receive> y correlación basada en contenidos.  
  
## Análisis  
 Para mostrar las características incluidas en este ejemplo, se crea un servicio de flujo de trabajo `RewardsPoints` que realiza un seguimiento de los puntos ganados y se utiliza para una cuenta determinada.El cliente utiliza <xref:System.Activities.WorkflowInvoker> para simular el envío de varias solicitudes a la cola.Para mandar por correo un mensaje a la cola en una transacción, la actividad <xref:System.ServiceModel.Activities.Send> se puede colocar dentro de la propiedad <xref:System.Activities.Statements.TransactionScope.Body%2A> de un objeto <xref:System.Activities.Statements.TransactionScope>.En este ejemplo, el cliente se ejecuta primero, seguido del servidor, para mostrar cómo los mensajes en cola pueden desacoplar las aplicaciones servidor y cliente.  
  
 Cuando el cliente se completa, el servicio se configura y se hospeda.En cuanto se abre, comienza el proceso de los mensajes que ya se han colocado en la cola.Cada mensaje se recibe y se procesa bajo la misma transacción del servidor.En este ejemplo, el primer mensaje recibido es una solicitud `CreateAccount` que crea la instancia e inicializa la correlación de contenidos en función del nombre de cuenta pasado como parte del mensaje de solicitud.Para modelar el tipo de servicio que se podría esperar en el mundo real, estas dos actividades <xref:System.ServiceModel.Activities.TransactedReceiveScope> que procesan los mensajes `UsePoints` y `AddPoints` se colocan en bifurcaciones paralelas dentro de un bucle `while` para que puedan procesar repetidamente estos mensajes en cualquier orden.  
  
 Tanto el objeto <xref:System.Activities.Statements.TransactionScope> como <xref:System.ServiceModel.Activities.TransactedReceiveScope> tienen un punto de persistencia implícito al final de sus ámbitos, por lo que el uso de estas actividades en [!INCLUDE[wf1](../../../../includes/wf1-md.md)] combinadas con colas es una manera fiable de mover el flujo de trabajo desde un estado coherente al siguiente y asegurarse al mismo tiempo de que nunca se pierdan los mensajes.  
  
#### Para configurar, compilar y ejecutar el ejemplo  
  
1.  Instale y configure MSMQ.Vea [Instalar Message Queuing \(MSMQ\)](http://go.microsoft.com/fwlink/?LinkId=178526) para obtener más detalles.  
  
2.  Ejecute el comando siguiente en una línea de comandos para asegurarse de que MSDTC se está ejecutando.`net start msdtc`  
  
3.  Compile el proyecto y abra la aplicación ejecutable o el proyecto en [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] y seleccione una opción de inicio en el menú de depuración.Primero, se crea la cola; a continuación, el cliente se ejecuta y envía mensajes a la cola y, finalmente, el servicio se inicia y se procesan los mensajes.Para salir del programa, presione Entrar.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(valor predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedQueues`