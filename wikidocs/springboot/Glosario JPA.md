Alcance : 
- Integrando JPA a un proyecto de springboot
- Conexión a una base de datos MySQL
- Modelado de entidades de una base de datos
- Creación de un controlador reactivo para el listado de registros
- Cobertura de código para :
	- Controlador REST
	- Servicios DAO
	
Integrando JPA a un proyecto de springboot
```xml
  
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
    <scope>runtime</scope>  
</dependency>
  
<dependency>  
	<groupId>org.springframework.boot</groupId>  
	<artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>
```
Modelado de entidades de una base de datos
Creación de un controlador reactivo para el listado de registros