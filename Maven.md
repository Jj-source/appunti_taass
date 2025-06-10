2025-06-07 11:54

Status: #adult

Tags:
# Maven

Maven è un tool di gestione delle build e delle dipendenze per progetti Java. Automatizza la compilazione, il packaging e il deploy del codice. Alternativa ad Ant e Gradle.

- Standardizzazione della struttura del progetto.
- Gestione automatica delle dipendenze tramite Maven Central Repository.
- Facilità di configurazione rispetto a script di build manuali.

Eviti problemi tipo non avere il .jar sul pc, o avere versioni sbagliate.

![[Maven_struttura.png]]

```Maven
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"%3E

	<modelVersion>4.0.0</modelVersion>
	<groupId>com.example</groupId>
	<artifactId>my-app</artifactId>
	<version>1.0-SNAPSHOT</version>
	<packaging>jar</packaging>
	<dependencies>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
			<version>5.3.15</version>
		</dependency>
 	</dependencies>
</project>
```

Comandi
- *mvn clean* → Cancella i file di build.
- *mvn compile* → Compila il codice sorgente.
- *mvn test* → Esegue i test unitari.
- *mvn package* → Genera il .jar o .war del progetto.
- *mvn install* → Installa il pacchetto nella repository locale.
- *mvn dependency: tree* → Mostra la struttura delle dipendenze del progetto.

##### .jar (Java Archive)
Un file `.jar` è un formato di archivio che aggrega molti file in uno solo. È comunemente usato per distribuire librerie, applicazioni e componenti Java.
##### .war (Web Application Archive)
Tipo speciale di file `.jar` utilizzato specificamente per distribuire applicazioni web Java. 
Contengono tutti i componenti necessari per un'applicazione web, inclusi servlet, JSP (JavaServer Pages), HTML, JavaScript, e altri file di risorse.


# References
