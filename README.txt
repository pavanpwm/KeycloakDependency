
This is a dependency spring boot project with keycloak + spring security configured 
Before anything, you need to install and configure Keycloak Server on your pc. Follow this video
https://youtu.be/kXrhF7dB7qI




All you need to do is 

1. download the jar file from here
https://github.com/pavanpwm/KeycloakDependency/raw/main/KeycloakDependency-0.0.1-SNAPSHOT.jar

2. add this in your spring boot projects build path.


3. Copy following config to src/main/resources/application.properties

#url where keycloak is hosted
keycloak.auth-server-url=http://localhost:8280/auth
#realm name
keycloak.realm=SpringKeycloakPOC
#client name
keycloak.resource=api1
keycloak.public-client=true
#uncomment below line if you are sending authentication token to any of this api endpoints
#keycloak.bearer-only=true
#set different port for running multiple apis at a time
server.port=8080
#for CORS allowed origins
# * means all origins are allowed.
#you can specify an origin if you want allow only one origin
origins.allowed=*



4. Use below annotation for your SpringBootApplication with MAIN class

@SpringBootApplication(scanBasePackages={"keycloak.poc"})



5. We need following depdndencies so,
copy following code to your pom.xml, then do <Maven Update>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.5.6</version>
		<relativePath />
	</parent>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>
		<dependency>
			<groupId>org.keycloak</groupId>
			<artifactId>keycloak-spring-boot-starter</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<properties>
		<java.version>1.8</java.version>
		<keycloak-adapter-bom.version>15.0.2</keycloak-adapter-bom.version>
	</properties>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.keycloak.bom</groupId>
				<artifactId>keycloak-adapter-bom</artifactId>
				<version>${keycloak-adapter-bom.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>		
	



7. Now run the Main class.




**********************************************************************************


For those curious minds who want to know how I created above jar?? Follow em

1. Download the above project 
2. Import to eclipse as maven project eclipse(preferred)
3. Then follow this video
https://youtu.be/VgN1FaPXU6A
