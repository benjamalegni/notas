### SOA y diseño monolitico
- Si bien las arquitecturas orientadas a servicios (SOA) son un estilo muy popular para las aplicaciones Web …
- Todos los servicios (o lógica de negocio) de la aplicación están empaquetados en un único artefacto para despliegue 
	- el monolito
	- Esto implica que cualquier cambio en la aplicación requiere un re-despliegue de todo la aplicación
	- Adicionalmente, si se desea escalar, debe escalarse toda la aplicación

## implicancias para el desarrollo
![[Pasted image 20251029092129.png]]
Los distintos equipos de desarrollo y operaciones trabajan sobre
el mismo repositorio y sobre distintas partes de toda la aplicación, y no en forma desacoplada

### por que usar microservicios?
- La forma en que un sistema de software se empaqueta y se despliega afecta directamente ciertos atributos de calidad
	- Escalabilidad, disponibilidad, mantenibilidad, performance, etc.
- Esto suele alinear bien con procesos/equipos ágiles

- En 2002, Amazon formuló un conjunto de reglas para sus desarrolladores, que luego derivó en el concepto de microservicios
- Muchas de las guias de diseño para SOA también aplican a microservicios
	- Entonces cuál es la diferencia?

### explicacion detallada
Un (micro)servicio debe ser lo suficientemente “pequeño” como para ser desarrollado por un único equipo y ser facilmente testeable

- Principio de Responsabilidad Unica (POO), en el sentido que una clase o conjunto de clases deben tener una funcionalidad cohesiva y bajo acoplamiento con otras clases (que implementan otras responsabilidades)
- El servicio debe “encapsular” cambios relacionados a su responsabilidad

- Un microservicio no solo involucra su código fuente (por ej., SpringBoot) sino la capacidad de ser desplegado independientemente de otros microservicios -> runtime

## de monolito a micro-servicios
monolito:
- Un solo archivo ejecutable
- Que se despliega/escala como un todo

micro-servicios:
- Varios archivos ejecutables
- Que se despliega cada uno de forma autónoma
- Cada microservicio es multi-funcional: front-end, back-end, BD

Relación con la Ley de Conway
- Mayor independencia (y responsabilidad) de los equipos respecto a los servicios desarrollados


## microservicios y equipos
Cada servicio es propiedad de un único equipo
- Lo cuál significa que el equipo es responsable por todo el ciclo de vida del microservicio 
	 ->“you build it, you run it”
- La coordinación entre los equipos debiera estar limitada a las responsabilidades implementadas por cada microservicio y a las interfaces del servicio

#### gestion de DB
![[Pasted image 20251029095828.png]]

#### tipos de arquitecturas
![[Pasted image 20251029095842.png]]

### principios de arquitectura
Una arquitectura de microservicios es un tipo de arquitectura SOA 
- Aunque no toda arquitectura SOA tiene que ser de microservicios

Una arquitectura de microservicios prescribe que cada unidad de despliegue debe contener solo un servicio o uno pocos servicios cohesivos
- La restricción de despliegue es un factor distintivo

microservicios y contenedores:
Docker, Kubernetes, Rancher, etc.
	- Normalmente se suelen desplegar en ambientes cloud

### protocolos de comunicacion
- Los microservicios se comunican sólo mediante mensajes a través de la red
- La comunicación debe ser independiente de la tecnología de implementación de cada microservicio
- Algunos mecanismos comunes son:
	- REST (sobre HTTP)
	- Mensajes/eventos asíncronos

### ejemplo de aplicacion
![[Pasted image 20251029101016.png]]

### ejemplo mas complejo
![[Pasted image 20251029101038.png]]

## microservicios y atributos de calidad
(Como otros estilos arquitectónicos), los microservicios tienden a favorecer ciertos atributos de calidad:
- Availability and reliability
- Modifiability
- Performance
- Scalability
- Deployability
- Service autonomy
- …

### modificabilidad
- El equipo puede re-diseñar y re-desplegar cada microservicio independientemente
- El equipo tiene liberar para emplear distintos lenguajes, frameworks, bibliotecas y patrones para diseñar e implementar cada microservicio
- Los microservicios son componentes poco acoplados, y accesibles solo a través de sus contratos
- Sin embargo, el desarrollo de microservicios suele implicar un esfuerzo extra de programación (en comparación a ”sin microservicios”)

### reusabilidad
- El objetivo es reusar un microservicio dado en otra aplicación
- Una posible limitación es la dependencia de otros componentes
- Otro aspecto a considerar es la “cantidad” de funcionalidad asignada a un microservicio (la regla de “las 2 pizzas” es discutible)
- Fan-out: el número de servicios “hijos” dependientes de un microservicio que los invoca directamente

tipos de fan-out:
- Fan-out en amplitud (shallow): el microservicio tiene varios hijos (directos) y la cadena de solicitudes (profundidad) es normalmente corta
	- Menos paso de mensajes
		-> menor latencia
- Fan-out en profundidad (deep): el microservicio tiene un número pequeño de hijos (directos), pero la cadena de solicitudes puede ser larga
	- Mayor paso de mensajes -> mayor latencia, pero también un mayor potencial de reusabilidad de microservicios Deployment and Operations for Software Engineers


### escalabilidad
- Cada microservicio puede ser escalado independientemente, utilizando pools, clusters y grids (entre otros mecanismos)
	- Escalado horizontal, que generalmente involucra contenedores o VMs
- Las facilidades de despliegue de los microservicios hacen que tengan una buena alineación con la elasticidad de los ambientes de cloud computing

#### relacion con spring
![[Pasted image 20251029101529.png]]

# desarollo de microservicios
- Descomposición del problema y modelamiento/diseño en términos de entidades y servicios
- Granularidad de cada uno de los servicios
- Protocolos de comunicación
- Diseño de las interfaces
- Endpoints a exponer
- Gestión de configuración y despliegue
- Procesamiento de eventos
- Por ej., para comunicar cambios de estado o datos
- Descubrimiento y ruteo de servicios
- Balanceo de servicios y resiliencia
- Seguridad
- Logging y trazabilidad
- …

