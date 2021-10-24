----INSTRUCTIONS----

1. Create a maven project in Eclipse(preferred bcoz may have problems in updating classpaths)

2. Download KeycloakDependency-0.0.1-SNAPSHOT.jar
https://github.com/pavanpwm/configured-keycloak-dependecy/blob/main/KeycloakDependency-0.0.1-SNAPSHOT.jar

3. Copy the jar to src/main/resources/

4. Copy following config to src/main/resources/application.properties

#url where keycloak is hosted
keycloak.auth-server-url=http://localhost:8280/auth
#realm name
keycloak.realm=SpringKeycloakPOC
#client name
keycloak.resource=api1
keycloak.public-client=true
#remove below comment if you are sending authentication token to any of this api endpoints
#keycloak.bearer-only=true
#set different port for running multiple apis at a time
server.port=8080
#for CORS allowed origins
# * means all origins are allowed.
#you can specify an origin if you want allow only one origin
this.api.allowed.origins=*


5. Copy below main class to src/main/java/
//you can name it however you want, but keep the main method same

import keycloak.poc.KeycloakDependencyApplication;

public class Api1Application {
	public static void main(String[] args) {
		KeycloakDependencyApplication.main(args);
	}
}





6. 5. Copy following code to your pom.xml, then do <Maven Update>

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
			<groupId>keycloak.dependency</groupId>
			<artifactId>KeycloakDependency</artifactId>
			<version>0.0.1-SNAPSHOT</version>
			<scope>system</scope>
			<systemPath>${project.basedir}/src/main/resources/KeycloakDependency-0.0.1-SNAPSHOT.jar</systemPath>
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









NOTE: 

You should configure Keycloak before doing this and change the configuration accordingly in application.properties file







IF YOU ARE TOO LAZY TO DO ALL THIS THEN YOU CAN JUST IMPORT A MAVEN PROJECT FROM HERE AND JUST FOLLOW SOME INSTRUCTION THERE


