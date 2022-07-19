+++ 
title = "Preguntas frecuentes" 
chapter = true 
weight = 40
+++

#### A continuacion se muestran preguntas frecuentes en los entrenamientos de AWS Cloud Practitioner Essentials

<img src="images/logo-bar.png" alt="drawing"/>

### INFORMÁTICA

**P: ¿Se podría explicar un poco la nomenclatura que se usa para los distintos tipos de instancias?**

Los nombres de tipos de instancia combinan la familia de instancias, la generación y el tamaño de las instancias. 
Especificaciones de hardware
https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/instance-types.html#instance-hardware-specs 

Tipos de Instancias: https://aws.amazon.com/es/ec2/instance-types/

**P: ¿Cómo se cobra las instancia de Amazon EC2?**

Probar Amazon EC2 es gratis. Existen cinco modelos de compra de instancias de Amazon EC2: bajo demanda, Savings Plans, instancias reservadas e instancias de spot. El uso de EC2 se factura en incrementos de segundos, con un mínimo de 60 segundos https://aws.amazon.com/es/ec2/pricing/

**P: ¿Donde veo los costos?**

En el Billing Dashboard, el consumo real. y AWS Cost Explorer para ver el desglose

**P: ¿Se puede programa tareas para detener o encender instancias?**

Si, es posible programar este tipo de tareas. https://aws.amazon.com/es/solutions/implementations/instance-scheduler/

**P: ¿Qué es una instancia spot y cuando utilizarla?**

las instancias SPOTs son para cargas de trabajo más flexibles, que pueden soportar interrupciones, ejemplo ambientes con auto escalabilidad, o procesos batch.

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-best-practices.html

**P: ¿Te avisan cuando te quitan una instancia spot?**

Cuando Amazon EC2 va a interrumpir su instancia de spot, emite un evento dos minutos antes de la interrupción real, sin embargo, de acuerdo a los reportes de cómo los clientes utlizan instancias Spot, el 95% de los clientes que usan Instancias Spot terminan sus cargas de trabajo antes que AWS genere la notificación, solo el 5% de los clientes si les llegan la notificación de que debe terminar la instancia y asegurarse de respaldar sus datos.

**P: ¿Qué factores debo tomar para implementar auto escalado en instancias Amazon EC2?**

Para implementar un grupo de escalado automático para usarlo con una aplicación, Considere lo siguiente:

- Entre cuántas zonas de disponibilidad debe distribuirse el grupo de Auto Scaling.
- Qué recursos existentes se pueden utilizar, como grupos de seguridad o imágenes de máquina de Amazon (AMI).
- Si desea escalar para aumentar o disminuir la capacidad, o solo desea asegurarse de que siempre haya un número específico de servidores en funcionamiento. Tenga en cuenta que Amazon EC2 Auto Scaling puede hacer ambas cosas a la vez.
- Qué métricas son más relevantes para el rendimiento de la aplicación.
- Cuánto tiempo tarda en lanzar y configurar un servidor.
https://docs.aws.amazon.com/es_es/autoscaling/ec2/userguide/get-started-with-ec2-auto-scaling.html

**P: ¿Autoscaling solo aplica para instancias on demand?**

Puede lanzar y escalar automáticamente una flota de instancias bajo demanda e instancias de spot en un solo grupo de Auto Scaling. Además, puede utilizar instancias reservadas o un Savings Plan para conseguir mejores precios de los habituales en las instancias bajo demanda
https://docs.aws.amazon.com/es_es/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html

**P: ¿Amazon EC2 Auto Scaling tiene costo?**

Las características de Amazon EC2 Auto Scaling no tienen cargos adicionales más allá de los que conllevan los servicios para Amazon EC2, CloudWatch (para las políticas de escalado) y los otros recursos de AWS que utilice.

**P: ¿Por cada grupo de auto scaling se necesita un Elastic Load Balancer?**

Si, para distribuir automáticamente el tráfico entrante en la aplicación entre varias instancias del grupo de Auto Scaling, utilice un Elastic Load Balancing.

Normalmente se utilizan juntos, todo va a depender a donde quieres balancear la carga. Lo ideal es que el ELB sea el servicio donde lleguen todas las peticiones de los usuarios y luego las distribuye a las instancias activas en el autoscaling group para que sean procesadas. Por el otro lado el Auto Scaling va a aumentar el número de instancias si la demanda de recursos crece y se activa el auto escalado sea dinamico o predictivo. Ambos servicio se integran para conocer si el ELB tiene que distruibuir la carga a nuevas instancias creadas o por el contrario dejar de enviar peticiones a la instancias eliminadas porque la demanda es baja.

**P: ¿El Elastic Load Balancer también proporciona un nivel de seguridad para que las peticiones no lleguen directamente a las EC2?**

Como servicio administrado, Elastic Load Balancing está protegido por procedimientos de seguridad de red globales de AWS que se describen en elAmazon Web Services: Información general sobre los procesos de seguridad
Utilice agentes de escucha seguros para admitir la comunicación cifrada entre los clientes y los balanceadores de carga. Los balanceadores de carga de aplicaciones admiten oyentes HTTPS. Los balanceadores de carga de red admiten oyentes TLS. Los balanceadores de carga clásicos admiten escucha HTTPS y TLS. Puede elegir entre políticas de seguridad predefinidas para el balanceador de carga con el fin de especificar los conjuntos de cifrado y las versiones de protocolo compatibles con la aplicación.
https://docs.aws.amazon.com/es_es/elasticloadbalancing/latest/userguide/infrastructure-security.html

**P: ¿Cuáles son las diferentes de los tipos de Elastic Load Balancing?**

Elastic Load Balancing admite los siguientes tipos de balanceadores de carga:

- Application Load Balancers: Un Application Load Balancer toma decisiones de enrutamiento en la capa de aplicación (HTTP/HTTPS), admite el enrutamiento basado en rutas y puede dirigir las solicitudes a uno o varios puertos de cada instancia de contenedor del clúster.
- Network Load Balancers. toma las decisiones de enrutamiento en la capa de transporte (TCP/SSL). Puede atender millones de solicitudes por segundo. Una vez que el balanceador de carga ha recibido una conexión, selecciona un destino del grupo de destinos para la regla predeterminada por medio de un algoritmo hash de flujo de direccionamiento
- Gateway Load Balancers: reenviando el tráfico a los dispositivos virtuales que se encuentran en AWS Marketplace de proveedores externos.
- Además, permiten implementar, escalar y administrar dispositivos virtuales, como firewalls, sistemas de prevención y detección de intrusiones así como sistemas de inspección profunda de paquetes 
https://docs.aws.amazon.com/es_es/AmazonECS/latest/developerguide/load-balancer-types.html

**P: ¿Cuáles son las diferencias entre EKS y ECS?**

*Amazon Elastic Container Service (ECS)*

Amazon es un servicio de administración de contenedores altamente escalable y de alto rendimiento propietario de AWS que permite a nuestros clientes ejecutar aplicaciones en un clúster administrado de instancias Amazon EC2 o en AWS Fargate.

- ECS en sí es gratis, solo pagas por Recursos de Amazon EC2 o AWS Fargate que utiliza
- Fácil de implementar con una consola de administración gráfica.
- Las implementaciones pequeñas, medianas prefieren ECS debido a su simplicidad e integragración nativa con múltiples servicios de AWS.

*Amazon Elastic Kubernetes Service (EKS)*

Amazon EKS administra automáticamente la disponibilidad y escalabilidad de los nodos del plano de control de Kubernetes. Estos nodos son responsables de programar contenedores, administrar la disponibilidad de las aplicaciones, almacenar datos de clúster y otras tareas claves.

- La capa de administración de EKS incurre en un costo adicional un cargo mensual por clúster.
- EKS permite integranción con servicios adminitrados de AWS, facilitando la modernización de aplicaciones administradas por nuestros clientes.

**P: ¿Hay planes de tener regiones en Latinoamérica?**

Todavía no se tiene información oficial de cuando se liberará nuevas regiones en Latinoamérica. Sin embargo recientemente se anunciaron **Local Zones** en distintos paises de la región. Consulte al anuncio en siguiente liga: https://aws.amazon.com/blogs/publicsector/aws-announces-local-zones-latin-america/

**P: ¿Existe algún impedimento si posteriormente queremos cambiar a otra región?**

No, puedes configurar recursos/servicios en múltiples regiones, hay que diferenciar cuales son los servicios regionales y globales, puedes transferir datos entre regiones (verificar temas de costos) también puedes replicar tu infraestructura en diferentes regiones en caso que sea necesario,  Hay servicios que nos ayudan a facilitar este proceso de creación de recursos en otras regiones, por ejemplo AWS CloudFormation

**P: ¿Cuál es el funcionamiento de la ubicación de borde, ¿Qué lo diferencia de una zona de disponibilidad?**

Una Ubicación de borde es un centro de datos que realizan cache de las copia de los contenido se utilizan para el servicio de Amazon CloudFront (u otros servicios de acceleración de entrega de contenido), Una zona de disponibilidad tiene al menos un centro de datos o más para proveer los servicios del portafolio de AWS, en donde van alojar las aplicaciones, cargas de trabajo te apalancas de estas AZs para aprovisionar los servicios y recursos de AWS de forma confiable.

**P: ¿Cómo se maneja el cache en el servicio Amazon CloudFront?**

Es posible administrar el tiempo que el contenido se mantiene en *cache* antes de que CloudFront reenvíe otra solicitud al origen. Reducir la duración le permite ofrecer contenido dinámico. Aumentar la duración implica que sus usuarios podrán disfrutar de un mejor rendimiento ya que es más probable que sus archivos se ofrezcan directamente desde la caché perimetral. Una mayor duración también reduce la carga en el origen.
https://docs.aws.amazon.com/es_es/AmazonCloudFront/latest/DeveloperGuide/Expiration.html

**P: ¿AWS Outpost es el único servicio para tener un modelo de nube híbrida?, ¿que otros hay?**

Tenemos muchos otros, existe un conjunto muy amplio para proveer servicios de informática, redes, almacenamiento, seguridad, identidad, integración de datos, administración, monitoreo y operaciones para crear arquitecturas híbridas que satisfagan sus requisitos y casos de uso específicos.
https://aws.amazon.com/es/hybrid/

**P: ¿Qué requisitos debe cumplir el cliente para que AWS pueda colocar el rack de AWS Outposts?**

El sitio debe admitir los requisitos de espacio, red y energía básicos para alojar un Outpost. Los Outposts necesitan de 5 a 15 kVA, pueden admitir enlaces ascendentes de 1/10/40/100 Gbps y espacio para un rack 42U (dimensiones de 80” X 24” X 48”). Como los Outposts requieren conectividad de red fiable a la región de AWS, debe planificar una conexión a Internet pública. Los clientes deben tener soporte Enterprise, el cual ofrece apoyo remoto las 24 horas del día, los 7 días de la semana en 15 minutos, entre otros requisitos. Verificar en el siguiente link: https://aws.amazon.com/es/outposts/rack/hardware-specs/?nc=sn&loc=4

**P: ¿AWS Lambda puede ejecutar código que necesita ejecutar recuros de GPU?**

Por el momento, esta opción no se encuentra disponible.

**P: ¿Durante cuánto tiempo se puede ejecutar una función de AWS Lambda?**

Se pueden configurar las funciones de AWS Lambda para que se ejecuten durante un plazo de hasta 15 minutos por ejecución. Puede establecer un tiempo de espera de cualquier valor entre 1 segundo y 15 minuto

### CONECTIVIDAD

**P: ¿Una VPN terminan en los Edge location?**

No, las conexiones de VPN, tanto Site-to-site y *client VPN* terminan en el **Virtual Private Gateway** de una **VPC**.

**P: ¿Al estar en diferentes tipos de redes en una VPC, estas ya se pueden ver entre sí, independientemente de la configuracion de cada red?**

Cada subred debe estar asociada a una tabla de ruteo que, a su vez, especifica las rutas permitidas para el tráfico saliente de la subred. Cada subred que se crea se asocia automáticamente a la tabla de ruteo principal de la VPC. Es posible cambiar la asociación y el contenido de la tabla de ruteo principal. Para obtener más información, consulte Configurar tablas de enrutamiento.
https://docs.aws.amazon.com/es_es/vpc/latest/userguide/configure-subnets.html

**P: ¿Cómo puedo comunicar dos zonas de disponibilidad?**

A través de las subredes de una **VPC**. Las subredes tienen una relacion 1:1 con las zonas de disponibilidad.

**P: ¿En una VPC nosotros definimos las IP's?**

Amazon VPC le permite aprovisionar una sección de la nube de Amazon Web Services (AWS) aislada de forma lógica, donde podrá lanzar recursos de AWS en una red virtual que usted defina. Puede controlar todos los aspectos del entorno de redes virtual, incluida la selección de sus propios rangos de direcciones IP en notación CIDR (Classless Inter Domain Routing), la creación de subredes y la configuración de tablas de ruteo y gateways de red

https://docs.aws.amazon.com/es_es/vpc/latest/userguide/how-it-works.html#vpc-ip-addressing

**P: ¿A qué se refiere que el filtrado de paquetes en un Security Group sea con "estado" (stateful)?**

Los grupos de seguridad utilizan el seguimiento de las conexiones para realizar un seguimiento de la información sobre el tráfico hacia y desde la instancia. Las reglas se aplican según el estado de la conexión del tráfico para determinar si el tráfico se permite o se deniega. Con este enfoque, los grupos de seguridad tienen estado. Esto significa que se permite la salida de las repuestas al tráfico de entrada de la instancia, independientemente de las reglas de salida del grupo de seguridad y viceversa.

**P: ¿Quién presta ese servicio de última milla entre cliente final y AWS centro de datos?**

Los socios de negocios de telecomunicaciones le brindan flexibilidad y opciones para conectarse a AWS, lo que incluye conexiones exclusivas y monitoreo adicional del enlace de la red entre socios de entrega de AWS Direct Connect y AWS.

https://aws.amazon.com/es/directconnect/partners/?partner-solutions-cards.sort-by=item.additionalFields.partnerNameLower&partner-solutions-cards.sort-order=asc&awsf.partner-solutions-filter-location=location%23latam

**P: ¿Con Amazon Route 53 puedo comprar un dominio?**

Correcto, https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html

**P: ¿Cómo puedo registrar un dominio en Amazon Route 53?**

Información para registro de un nuevo dominio: 

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html#domain-register-procedure

Información para registro de un dominio existente: 

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/MigratingDNS.html

**P: ¿Cómo funcionan los aceleradores de trafico de AWS?**

Puede utilizar Amazon CloudFront para que la entrega de contenido a los usuarios se realice de una forma más rápido, bajando la latencia, existe otros servicios como S3 transfer acceleration o AWS Global Accelarator ambos tienes distintos enfoques pero la idea es aumentar la velocidad de transmisión de los datos y el rendimiento de las apaplicaciones.

### ALMACENAMIENTO Y BASES DE DATOS

**P: ¿Cuándo usamos almacenamiento efímero o volátil (instance store)?**

El almacén de instancias es ideal para el almacenamiento temporal, ya que los datos almacenados en los volúmenes del almacén de instancias no son persistentes a través de paradas de instancia, terminaciones o errores de hardware, se puede usar para realizar copias de seguridad temporales y para almacenar la memoria caché, los registros u otros datos aleatorios de una aplicación. Los volúmenes de almacenamiento de instancias también son útiles para las aplicaciones que se centran en el procesamiento de datos en lugar de almacenarlos.

**P: ¿Elastic Block Storage (EBS) es únicamente para las Amazon EC2?**

Si, al ser Almacenamiento de bloque necesita presentarlo a un Sistema Operativo de la instancia, Amazon EBS le permite crear volúmenes de almacenamiento y asociarlo a instancias de Amazon EC2. Sin embargo, otros servicios como RDS, Redshift, EMR, etc. consume de forma embebida al servicio de EBS.

**P: ¿Los snapshots de EBS son opcionales?**

Si, los Snapshots de los EBS son opcionales y permiten generar un punto restauración del volumen de almacenamiento EBS.

**P: ¿Las clases de S3 Glacier se copian en diferentes zonas de disponibilidad?**

Las clases de almacenamiento Amazon S3 Estándar, S3 Estándar - Acceso poco frecuente y S3 Glacier replican datos en un mínimo de tres zonas de disponibilidad para brindar protección contra la pérdida de una zona entera.

**P: ¿Se puede tener un S3 para un sitio web estático directamente sin crear una instancia de Amazon EC2?**

Correcto, es posible alojar un sitio web estático en Amazon S3, configure un bucket de Amazon S3 destinado al alojamiento del sitio web y cargue el contenido. Con la consola de administración de AWS, puede configurar el bucket de Amazon S3 como un sitio web estático sin escribir ningún código, o sin tener que desplegar una instancia de Amazon EC2.
https://docs.aws.amazon.com/es_es/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html

**P: ¿El servicio Elastic File Service también tiene el servicio para multi-zonas o para única-zona?**

De manera predeterminada, cada objeto del sistema de archivos de EFS (es decir, cada directorio, archivo y enlace) se almacena de manera redundante en múltiples AZ para los sistemas de archivos que utilizan clases de almacenamiento Standard. Si selecciona las clases de almacenamiento de Amazon EFS One Zone, los datos se almacenan de forma redundante en una única AZ.

**P: ¿El servicio Amazon RDS es un SaaS?**

No, Amazon RDS es un servicio administrado de bases de datos relacionales, que podríamos definir como DBaaS.

**P: ¿Se Tiene un comparativo de Amazon Aurora vs PostgreSQL?**

Amazon Aurora ofrece mejoras importantes en comparación con el desempeño de PostgreSQL nativo, ya que realiza una estrecha integración del motor de base de datos con la capa de almacenamiento virtualizado y distribuído basado en SSD para cargas de trabajo de base de datos, reduce las escrituras en el sistema de almacenamiento, minimiza la contención de bloqueos y elimina los retrasos que ocasionan los subprocesos del procesamiento de bases de datos. https://d1.awsstatic.com/product-marketing/Aurora/RDS_Aurora_PostgreSQL_Performance_Assessment_Benchmarking_V1-0.pdf

**P: ¿Se puede migrar bases de datos de Oracle DB a Aurora-MySQL?**

Si lo puedes hacer utilizando el servicio de AWS Database Migration Service (DMS) en combinación con AWS Schema Conversion Tool (SCT). AWS SCT puede ayudar a realizar migraciones heterogéneas, haciendo una preparación de la tabla de la instancia de la base de datos que va a recibir los datos, y Database Migration Service (DMS) haría la migración de los datos entre las bases de datos de origen y destino.

https://aws.amazon.com/es/dms/schema-conversion-tool/?nc=sn&loc=2&refid=f5cf9b9c-13f7-43d8-9578-76f305aef635

**P: ¿AWS tiene algún servicio de backup remoto o tenemos que armarlo, suponiendo que es una nube híbrida?**

AWS Backup centraliza la administración y la conformidad de la protección de datos para las aplicaciones que se ejecutan en entornos híbridos. Con AWS Backup, puede proteger las cargas de trabajo de VMware que se ejecutan en las instalaciones y en VMware CloudTM on AWS, y los datos almacenados en volúmenes de AWS Storage Gateway. https://aws.amazon.com/es/backup/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc

### SEGURIDAD

**P: ¿Puedo implementar un Firewall como Fortinet en AWS?**

Si se puede, desde el AWS Marketplace es posible implementar servicios/productos de seguridad terceros en la nube de AWS; ejemplo se puede implementar un Fortinet FortiGate que permite la mitigación de puntos ciegos para mejorar la conformidad con las políticas mediante la implementación de controles de seguridad críticos dentro de su entorno de AWS. 
https://aws.amazon.com/marketplace/b/0625e4fd-88dd-4dd9-9e57-4a0461f97fb4?ref_=dtl_categories_0625e4fd-88dd-4dd9-9e57-4a0461f97fb4&category=0625e4fd-88dd-4dd9-9e57-4a0461f97fb4

**P: Como se puede activar MFA en el CLI?**

Para usar el MFA en llamadas de API desde el CLI, consulte el siguiente link: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_configure-api-require.html o 
https://aws.amazon.com/es/premiumsupport/knowledge-center/authenticate-mfa-cli/

**P: ¿MFA tiene costo?**

No se cobra ninguna tarifa adicional por el uso.

**P: ¿Qué tipo de chequeos hace Inspector? ¿se publica una lista de vulnerabilidades?**

Realiza validaciones de vulnerabilidad en la instancia Amazon EC2, por ejemplo, si se realizado la actualización del sistema operativo, si hay un parche de seguridad que no se ha aplicado, si cuenta con librerías obsoletas, detectar el acceso a las EC2 desde internet puertos abiertos, activación de sesiones remotas anormales.
https://docs.aws.amazon.com/es_es/inspector/latest/user/findings-types.html

**P: ¿Que es Control Tower?**

AWS Control Tower es un servicio destinado a organizaciones con varios equipos y cuentas que estén buscando la forma más sencilla de configurar su nuevo entorno de AWS multicuenta y de realizar un control a escala. Con AWS Control Tower, los administradores de la nube tienen la tranquilidad de saber que las cuentas de su organización cumplen políticas establecidas mientras que los creadores pueden aprovisionar nuevas cuentas de AWS rápidamente con unos pocos clics.

### FACTURACIÓN Y SOPORTE

**P: ¿El uso de AWS Budgets tiene un costo?**

La creación de Presupuestos no tiene un costo, para mayor referencia consultar el siguiente link: https://aws.amazon.com/es/aws-cost-management/aws-budgets/pricing/

**P: ¿Con que plan de soporte se obtiene todas las validaciones de AWS Truster Advisor?**

AWS Trusted Advisor está habilitado con las validaciones completas a partir del plan de soporte Business.

**P: ¿Por qué termino pagando algunos dólares si estoy en la capa gratuita?**

Algunos productos son gratis por siempre, otros a prueba por tiempo, algunos otros por 12 meses. Es importante conocer el detalle y límites de los términos de uso de la capa gratuita para cada servicio con el fin de no incurrir en gastos no anticipados.

Para evitar cargos inesperados verificar en la consola en Billing / Facturación y se detallará cuanto has consumido de recursos de tu capa gratuita
https://docs.aws.amazon.com/es_es/awsaccountbilling/latest/aboutv2/billing-free-tier.html

**P: ¿Qué pasa si se superan los límites en los de 12 meses gratis? Se cobran o si limita el servicio?**

Si el uso del servicio que se esta consumiento se encuentra por debajo de la capa gratuita y se está cumpliendo con los términos de uso no se generará ningún cobro. Pero si el uspo excede las condiciones de la capa gratuita se comenzará a incurrir en gastos facturables.

**P: ¿Tengo más de 12 meses con la cuenta AWS, pero me siguen apareciendo como free tier algunas instancias EC2 al momento de crearlas, ¿puedo seguir considerándolas de tal forma en mi cuenta o ya no?**

Los tipos de instancias de Amazon EC2 de la free tier siempre aparecerán con dicha etiqueta. Para validar el consumo y si aplica free tier puedes consultar el siguiente link: https://docs.aws.amazon.com/es_es/awsaccountbilling/latest/aboutv2/tracking-free-tier-usage.html

<img src="images/logo-bar.png" alt="drawing"/>