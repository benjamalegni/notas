1. Explicar la diferencia entre Verificación y Validación. Dar 2 ejemplos concretos de cada una. 

	verificacion es un proceso formal e interno en el cual se verifica el producto que se esta desarrollando. En cambio validacion se refiere al testeo por parte de usuarios.

	verificacion se centra en preguntarse si lo que esta haciendo se esta haciendo correctamente y validacion se centra en preguntarse si el sistema hace lo que el usuario necesita

	ejemplos: verificacion: unit testing, linting
	validacion: UAT, demos, prototipos

2. Explicar la pirámide de testing. ¿Por qué se recomienda tener muchos unit tests y pocos E2E? 
	porque los unit tests son los menos costosos de la suite de test. son modulares y ayudan a mantener un control en lo que hacen ciertas partes del codigo. los tests e2e son muy costosos y por lo tanto no se usan tanta cantidad de estos, pero igualmente tienen una alta importancia.
	
3. Definir qué es un Unit Test según Khorikov. ¿Qué significa que sea determinista? 
	define 3 puntos principales:
	- verifica una pequena porcion de comportamiento
	- lo hace rapido
	- lo hace de forma aisladas a otros tests
	con determinista se refiere a que si no cambia el codigo siempre va a devolver el mismo resultado
	
4. Explicar los 4 pilares de un buen unit test (protección contra regresiones, resistencia al refactoring, feedback rápido y mantenibilidad). 
	- proteccion contra regresiones: debe detectar que no al implementar funcionalidades no se rompen otras funcionalidades ya implementadas
	- resistencia al refactoring: no debe fallar si se cambia el comportamiento interno, solo verifica con interacciones al exterior
	- feedback rapido: debe ejecutarse rapidamente
	- mantenibilidad: deben ser facil de leer, de entender y de modificar
	
5. Definir: false positive y false negative. ¿Cuál es más dañino para un equipo y por qué? 
	- false positive es un error de testing que sucede aunque el sistema funcione correctamente
	- false negative es un error del sistema que no es dectado por la suite de testing
	es mucho mas peligroso un falso negativo. hay errores que conocemos y podemos preveernos como desarrolladores, pero encontrar aquellos errores que no conocemos y no son detectados puede ser mucho mas riesgoso en comparacion.
6. Explicar el patrón AAA (Arrange / Act / Assert) y por qué se recomienda una sola llamada en Act.
	arrange: importar dependencias, inicializar variables, instanciar objetos, etc.
	act: llamar al segmento que estamos testeando
	assert: verificar que los resultados obtenidos son correctos

ej 2:
que tipo de test aplicar: unit, integration, E2E.
7. Validar que el cálculo de impuestos de una factura sea correcto para distintos porcentajes. 
	unit
8. Verificar que un endpoint REST persiste correctamente un usuario en una base PostgreSQL real. 
	integracion
9. Verificar que el login funciona desde la interfaz web hasta la base de datos. 
	E2E
10. Verificar que el sistema arranca correctamente y responde a un request básico luego del deploy. 
	integracion
11. Verificar que un servicio envía un email cuando se registra un usuario, sin enviar correos reales.
	integracion

ej 3:
Ejercicio 3 – Unit Testing con JUnit 5 (AAA y casos borde) Dado el siguiente código: public class PasswordValidator { public boolean isValid(String password) { if (password == null) return false; if (password.length() < 8) return false; boolean hasUpper = false; boolean hasLower = false; boolean hasDigit = false; for (char c : password.toCharArray()) { if (Character.isUpperCase(c)) hasUpper = true; if (Character.isLowerCase(c)) hasLower = true; if (Character.isDigit(c)) hasDigit = true; } return hasUpper && hasLower && hasDigit; } } a) Escribir al menos 8 unit tests usando JUnit 5 que cubran casos normales y casos borde. b) Los nombres de los tests deben seguir la convención: Metodo_Escenario_ResultadoEsperado. c) Aplicar AAA. Cada test debe tener una sola llamada en Act. d) Indicar qué tipo de cobertura se logra (line vs branch) y qué casos faltan si existieran.