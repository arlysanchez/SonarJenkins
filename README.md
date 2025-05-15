README_help

# docker
Repositorio en el cual se agregan las diferentes imagenes a trabajar en diferentes carpetas, las cuales contienen un `docker-compose` y algunas el `Dockerfile` cuando es necesario crear una imagen propia.

<br>


# Jenkins
Se instalan los siguientes plugins

 Route: `~/Administrar Jenkins/plugins` buscar los plugin he instalar uno a uno sin reiniciar

1. **Role-based Authorization Strategy** para el manejo de los roles, [Documentación Oficial](https://plugins.jenkins.io/role-strategy/). Una vez instalado se deben seguir los siguientes pasos.
*POST-INSTALACIÓN*:
1. Para habilitar el plugin se debe ir al apartado `~/Administrar Jenkins/Tool/Authentication/Autorización` donde se debe tomar la opción `Role Based Strategy`. 	
2. Para agregar roles y permisos se debe ir al apartado `~/Administrar Jenkins/Manage and Assign Roles` y seguir las recomendaciones de la [Documentación Oficial](https://plugins.jenkins.io/role-strategy/).


<br>

2. **Maven** para compilar los proyectos Java, [Documentación oficial](https://plugins.jenkins.io/maven-plugin/).
 
**Primero instalar Maven integration Route: `~/Administrar Jenkins/plugins`

*POST-INSTALACIÓN*: Una vez instalado el plugin se debe ir al apartado `~/Administrar Jenkins/Tool/Maven` y agregan una instalación con la versión que se desea trabajar.

<br>

3. **SonarQube** para el análisis de código, [Documentación oficial](https://plugins.jenkins.io/sonar/). Una vez instalado se deben seguir los siguientes pasos.

*POST-INSTALACIÓN*

1. Se debe lanzar el contenedor de [SonarQube](#sonarqube) y generar un **token**, en el apartado `~/Administration/Security/Users`, ejemplo: `squ_e99b79ef86f2812670d1f714a33f6757c52624e6`, una vez generado se debe copiar y guardar, ya que solo se muestra una sola vez.

2. De vuelta en **Jenkins** , se debe crear una **Secret** con el **Token** generado en **SonarQube**, en el apartado `~/Administrar Jenkins/Credentials/System/Global Credentials/add Credential`, en el tipo o (`King`) según el idioma, se de seleccionar `Secret text` y llenar los campos, el valor del **Token** se debe ingresare en el campo `Secret`.
	
3. Siguiendo con la configuración en [SonarQube](#sonarqube) se debe ir al apartado `~/Administration/Configuration/webhooks` y agregar un nuevo `hook`, en el cual se agrega la url de **Jenkins** `http://jenkins:9080/sonarqube-webhook/` (la ruta es asi, porque en el nombre del servicio  creado en el compose de docker es jenkins, siendo que los contenedores estan en la misma red se comunican por el nombre del servicio), el nombre es de libre elección. 
	
4. Siguiendo con la configuración en **Jenkins**, Para habilitar el plugin se debe ir al apartado `~/Administrar Jenkins/Configurar el Sistema/SonarQube servers` y agregar una instalación, en el cual se agrega la url de **Sonarqube** `http://sonarqube:9000`(para windows es localhost, sin embargo para docker es el nombre del servicio), el nombre es de libre elección y se debe seleccionar el **Secret** creado en el punto anterior el cual se muestra .

