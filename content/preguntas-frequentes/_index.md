+++ 
title = "Preguntas frecuentes" 
chapter = true 
weight = 40
+++

#### A continuacion se muestran preguntas frecuentes en los entrenamientos de AWS Cloud Practitioner Essentials

<img src="images/logo-bar.png" alt="drawing"/>

**P: ¿Qué les ocurre a mis instancias de Amazon EC2 si elimino mi ASG?**

R: Si posee un grupo de EC2 Auto Scaling (ASG) con instancias en ejecución y decide eliminar el ASG, se interrumpirán las instancias y se eliminará el ASG.

**P: ¿Qué ocurre si una actividad de escalado hace que alcance mi límite de instancias de Amazon EC2?**

Amazon EC2 Auto Scaling no puede escalar más allá del límite de instancias de Amazon EC2 que usted puede ejecutar. Si necesita más instancias de Amazon EC2, complete el formulario de solicitud de instancias EC2 de Amazon.

**P: Si tengo datos instalados en un grupo de EC2 Auto Scaling y más tarde se crea dinámicamente una nueva instancia, ¿los datos se copian a las nuevas instancias?**

Los datos no se copian automáticamente de las instancias existentes a las nuevas. Puede usar enlaces de ciclo de vida para copiar los datos o una base de datos de <a href="https://aws.amazon.com/rds/" target="_blank">Amazon RDS</a> que incluya réplicas.

<img src="images/logo-bar.png" alt="drawing"/>