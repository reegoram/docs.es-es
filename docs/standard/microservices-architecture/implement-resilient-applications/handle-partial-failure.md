---
title: Control de errores parciales
description: Arquitectura de Microservicios de .NET para aplicaciones .NET en contenedores | Control de errores parciales
keywords: Docker, microservicios, ASP.NET, contenedor
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: b7d16acf3de2d395da70e8f46e59c129dec24f71
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="handling-partial-failure"></a><span data-ttu-id="467c7-104">Control de errores parciales</span><span class="sxs-lookup"><span data-stu-id="467c7-104">Handling partial failure</span></span>

<span data-ttu-id="467c7-105">En los sistemas distribuidos a las aplicaciones basadas en microservicios, hay un riesgo de error parcial omnipresente.</span><span class="sxs-lookup"><span data-stu-id="467c7-105">In distributed systems like microservices-based applications, there is an ever-present risk of partial failure.</span></span> <span data-ttu-id="467c7-106">Por ejemplo, un único contenedor/microservicio puede producir un error o podría no estar disponible para responder durante un breve período, o se puede bloquear una única máquina virtual o servidor.</span><span class="sxs-lookup"><span data-stu-id="467c7-106">For instance, a single microservice/container can fail or might not be available to respond for a short time, or a single VM or server can crash.</span></span> <span data-ttu-id="467c7-107">Puesto que los clientes y servicios son procesos independientes, es posible que un servicio no pueda responder de forma oportuna a solicitud del cliente.</span><span class="sxs-lookup"><span data-stu-id="467c7-107">Since clients and services are separate processes, a service might not be able to respond in a timely way to a client’s request.</span></span> <span data-ttu-id="467c7-108">El servicio podría estar sobrecargadas y responde muy lentamente a las solicitudes de, o simplemente no está accesible durante un breve tiempo debido a problemas de red.</span><span class="sxs-lookup"><span data-stu-id="467c7-108">The service might be overloaded and responding extremely slowly to requests, or might simply not be accessible for a short time because of network issues.</span></span>

<span data-ttu-id="467c7-109">Por ejemplo, considere la posibilidad de la página de detalles de pedido desde el eShopOnContainers aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="467c7-109">For example, consider the Order details page from the eShopOnContainers sample application.</span></span> <span data-ttu-id="467c7-110">Si la ordenación microservicio deja de responder cuando el usuario intenta enviar un pedido, una implementación incorrecta del proceso del cliente (la aplicación web MVC), por ejemplo, si el código de cliente usara RPC sincrónica sin tiempo de espera, se bloquea los subprocesos indefinidamente Esperando una respuesta.</span><span class="sxs-lookup"><span data-stu-id="467c7-110">If the ordering microservice is unresponsive when the user tries to submit an order, a bad implementation of the client process (the MVC web application)—for example, if the client code were to use synchronous RPCs with no timeout—would block threads indefinitely waiting for a response.</span></span> <span data-ttu-id="467c7-111">Además de crear una experiencia de usuario incorrectos, consume cada espera no responde o a un subproceso bloquea y subprocesos son muy valiosos en aplicaciones muy escalables.</span><span class="sxs-lookup"><span data-stu-id="467c7-111">In addition to creating a bad user experience, every unresponsive wait consumes or blocks a thread, and threads are extremely valuable in highly scalable applications.</span></span> <span data-ttu-id="467c7-112">Si hay demasiados subprocesos bloqueados, finalmente en tiempo de ejecución de la aplicación puede quedarse sin subprocesos.</span><span class="sxs-lookup"><span data-stu-id="467c7-112">If there are many blocked threads, eventually the application’s runtime can run out of threads.</span></span> <span data-ttu-id="467c7-113">En ese caso, la aplicación puede tornarse más global que no responde en lugar de simplemente parcialmente no responde, tal como se muestra en la figura 10-1.</span><span class="sxs-lookup"><span data-stu-id="467c7-113">In that case, the application can become globally unresponsive instead of just partially unresponsive, as show in Figure 10-1.</span></span>

![](./media/image1.png)

<span data-ttu-id="467c7-114">**Figura 10-1**.</span><span class="sxs-lookup"><span data-stu-id="467c7-114">**Figure 10-1**.</span></span> <span data-ttu-id="467c7-115">Errores parciales debido a las dependencias que afectan la disponibilidad de subprocesos de servicio</span><span class="sxs-lookup"><span data-stu-id="467c7-115">Partial failures because of dependencies that impact service thread availability</span></span>

<span data-ttu-id="467c7-116">En una aplicación basada en microservicios grande, puede se amplifique cualquier error parcial, especialmente si la mayor parte de la interacción de microservicios interno se basa en las llamadas sincrónicas de HTTP (que se considera un antipatrón).</span><span class="sxs-lookup"><span data-stu-id="467c7-116">In a large microservices-based application, any partial failure can be amplified, especially if most of the internal microservices interaction is based on synchronous HTTP calls (which is considered an anti-pattern).</span></span> <span data-ttu-id="467c7-117">Piense en un sistema que recibe millones de llamadas entrantes al día.</span><span class="sxs-lookup"><span data-stu-id="467c7-117">Think about a system that receives millions of incoming calls per day.</span></span> <span data-ttu-id="467c7-118">Si el sistema tiene un diseño incorrecto que se basa en cadenas largas de las llamadas sincrónicas de HTTP, estas llamadas entrantes podrían producir muchos millones de más de las llamadas salientes (supongamos que una proporción 1:4) al docenas de microservicios interno como dependencias sincrónicas.</span><span class="sxs-lookup"><span data-stu-id="467c7-118">If your system has a bad design that is based on long chains of synchronous HTTP calls, these incoming calls might result in many more millions of outgoing calls (let’s suppose a ratio of 1:4) to dozens of internal microservices as synchronous dependencies.</span></span> <span data-ttu-id="467c7-119">Esta situación se muestra en la figura 10-2, especialmente dependencia \#3.</span><span class="sxs-lookup"><span data-stu-id="467c7-119">This situation is shown in Figure 10-2, especially dependency \#3.</span></span>

![](./media/image2.png)

<span data-ttu-id="467c7-120">**Figura 10-2**.</span><span class="sxs-lookup"><span data-stu-id="467c7-120">**Figure 10-2**.</span></span> <span data-ttu-id="467c7-121">El impacto de tener un diseño incorrecto que incluye cadenas largas de solicitudes HTTP</span><span class="sxs-lookup"><span data-stu-id="467c7-121">The impact of having an incorrect design featuring long chains of HTTP requests</span></span>

<span data-ttu-id="467c7-122">Error intermitente es prácticamente garantizada en distribuida y en la nube en función de sistema, aunque cada dependencia sí tiene una disponibilidad excelente.</span><span class="sxs-lookup"><span data-stu-id="467c7-122">Intermittent failure is virtually guaranteed in a distributed and cloud based system, even if every dependency itself has excellent availability.</span></span> <span data-ttu-id="467c7-123">Debe ser un hecho que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="467c7-123">This should be a fact you need to consider.</span></span>

<span data-ttu-id="467c7-124">Si no diseñar e implementar técnicas para asegurar la tolerancia a errores, pueden ampliarse incluso pequeños tiempos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="467c7-124">If you do not design and implement techniques to ensure fault tolerance, even small downtimes can be amplified.</span></span> <span data-ttu-id="467c7-125">Por ejemplo, 50 dependencias con 99,99% de disponibilidad se crearán varias horas de tiempo de inactividad cada mes debido a este efecto dominó.</span><span class="sxs-lookup"><span data-stu-id="467c7-125">As an example, 50 dependencies each with 99.99% of availability would result in several hours of downtime each month because of this ripple effect.</span></span> <span data-ttu-id="467c7-126">Cuando se produce un error en una dependencia de microservicio al controlar un gran volumen de solicitudes, dicho error puede saturar todos los subprocesos de solicitud disponible en cada servicio rápidamente y se bloqueará toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="467c7-126">When a microservice dependency fails while handling a high volume of requests, that failure can quickly saturate all available request threads in each service and crash the whole application.</span></span>

![](./media/image3.png)

<span data-ttu-id="467c7-127">**Figura 10-3**.</span><span class="sxs-lookup"><span data-stu-id="467c7-127">**Figure 10-3**.</span></span> <span data-ttu-id="467c7-128">Error parcial ampliado por microservicios con cadenas largas de las llamadas sincrónicas de HTTP</span><span class="sxs-lookup"><span data-stu-id="467c7-128">Partial failure amplified by microservices with long chains of synchronous HTTP calls</span></span>

<span data-ttu-id="467c7-129">Para minimizar este problema, en la sección "*microservicio asincrónica integración exigir la autonomía de microservicio*" (en el capítulo sobre arquitectura), se recomienda usar la comunicación asincrónica entre interno microservicios.</span><span class="sxs-lookup"><span data-stu-id="467c7-129">To minimize this problem, in the section "*Asynchronous microservice integration enforce microservice’s autonomy*” (in the architecture chapter), we encouraged you to use asynchronous communication across the internal microservices.</span></span> <span data-ttu-id="467c7-130">Brevemente explicamos más en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="467c7-130">We briefly explain more in the next section.</span></span>

<span data-ttu-id="467c7-131">Además, es fundamental que diseña las aplicaciones cliente y microservicios para controlar los errores parciales, es decir, crear microservicios resistente y cliente de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="467c7-131">In addition, it is essential that you design your microservices and client applications to handle partial failures—that is, to build resilient microservices and client applications.</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="467c7-132">[Anterior] (index.md) [siguiente] (partial-error-strategies.md)</span><span class="sxs-lookup"><span data-stu-id="467c7-132">[Previous] (index.md) [Next] (partial-failure-strategies.md)</span></span>