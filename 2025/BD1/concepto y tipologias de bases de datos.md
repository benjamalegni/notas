### intro a DB's
- un sistema gestor de bases de datos (SGBD) consiste en una coleccion de datos interrelacionados y un conjunto de programas para acceder a dichos datos. la coleccion de datos, normalmente denominada base de datos, contiene info relevante para una empresa. El objetivo principal de este es proporcionar una forma de almacenar y recuperar la informacion de una base de datos de manera que sea tanto practiva como eficiente

la gestion de los datos implica tanto ==la definicion de estructurads para almacenar la info como la provision de mecanismos para la manipulacion de la info==. ademas, los sistemas de bases de datos deben proporcionar la **fiabiliadad** de la info almacenada, a pesar de las caidas del sistema o los intentos de accesos sin autorizacion. si los datos van a ser compartidos entre diversos usuarios, el sistema debe evitar posibles resultados anomalos

## aplicacion de los sistemas de DB
los sistemas de bases tienen amplia gama de aplicaciones en diversos sectores
- aplicaciones empresariales
	- sistema de gestion de clientes (CRM) utilizados por empresas y gestionar info sobre clientes mejorar el servicio y personalizar las interacciones
	- sistema de gestion de recursos humanos(HRMS) bases de datos que almacenan info de empleados, desde datos personales hasta registros de salarios, vacaciones y evaluaciones de desempeno
	- ERP (enterprise resource planning) integran diversos procesos empresariales como la contabilidad, finanzas, compras y produccion en una sola plataforma que depende de una base de datos centralizada
- e-commerce
	- gestion de inventario: rastrear productos, stock, proveedores y ventas
	- personalizacion de la experiencia del usuario: se almacenan datos sobre el comportamiento y preferencias de los usuarios para ofrecer recomendaciones personalizadas
- sector salud
	- historiales clinicos electronicos (EHR): almacenan info medica de pacientes, diagnosticos, tratamientos, prescripciones y resultados de laboratorio
	- gestion de hospitales: info sobre camas, personal, pacientes y recursos medicos
- etc...


# sistemas de archivos convencionales vs bases de datos
1. r**edundancia e inconsistencia de datos:** programadores pueden crear archivos con formatos distintos, generando duplicaion de info y posibles inconsistencias, como cambios no reflejados en todos los archivos
2. **dificultad en el acceso a los datos**: si surgen nuevas necesidades es necesario crear un nuevo programa o hacerlo manualmente, lo cual es ineficiente
3. **aislamiento de datos** 