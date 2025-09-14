### diseno de software
- planificar antes de construir
- facilitar la comunicacion con multiples stakeholders
- proveer con un **modelo de analisis** "manejable" para sistemas complejos
- brindar **preescripciones** para la implementacion del sistema
- la arquitectura es un artefacto, pero tambien parte del proceso de desarrollo (architecting)

#### example: client-server architecture
![[Pasted image 20250906182504.png]]
Estructura:
![[Pasted image 20250906182534.png]]
Category: Component & Connector or Allocation 

Elements: Tier—a logical grouping of runtime components. There are many ways to partition tiers. Some examples include functional responsibilities, compute platforms, team responsibilities, communication mechanisms, security requirements, and data access. 

Relations Belongs to—used to group components into a tier. Communicates with—shows how tiers or the components within interact with one another. This relation may be specialized to include information about protocols and communication constraints. Allowed to communicate with—indicates which tiers may communicate with components in other tiers. Allocated to—maps tiers to physical compute platforms. 

Rules for use: A component may belong to only one tier. Components within a tier are only allowed to communicate with other Rules for Use components within the same. Additional constraints describing tier communication can enhance reasoning and improve maintainability. A common approach is to allow communication only among adjacent tiers. 

Strengths: Promotes security, performance, availability, maintainability, modifiability. Can be used to reason about costs and deployment. Strengths 

Weaknesses: As a runtime construct, tiers can be difficult to enforce in large systems. Systems with many tiers can inhibit performance and maintainability.

## filosofia
crear -> comunicar -> analizar

## referencias bibliograficas
Software architecture in practice
Design it!
Designing software architecures
Design patterns

# Arquitectura de software
## requerimientos e implementacion
la breca entre los requerimientos y la implementacion es a menudo demasiado grande.

El rol de la arquitectura:
la arquitectura actua como "puente" entre los requerimientos del sistema y su implementacion
![[Pasted image 20250906183117.png]]

### def. Arquitectura
"software architecture is the structure of a software product. This includes elements, the externally visible properties of the elements, and the relationships between the elements"
"all architecture is design but not all design is architecture. Architecture represents the significant design decisions that shape a system, where significant is measured by cost of change"

![[Pasted image 20250906183316.png]]

#### funcion de un arquitecto de software
![[Pasted image 20250906190819.png]]

### ej: mi calculadora app
![[Pasted image 20250906185833.png]]

### arquis como blueprints
![[Pasted image 20250906190221.png]]

### arquis como decisiones
![[Pasted image 20250906190244.png]]

#### ejemplos de decisiones de arquitectura
- uso de un patron de layers para organizar el sistema
- insercion de un intermediario para separar la aplicacion que requiere un web service de la aplicacion que provee (e implementa) dicho servicio
- utilizacion de encriptacion con clave simetrica?
- utilizacion de un algoritmo que garantiza que no se producen memory leaks?

