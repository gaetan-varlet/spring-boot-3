# Spring Boot 3

---

## Documentation

- sortie fin novembre 2022
- Release Note : https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Release-Notes
- Guide de migration : https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide

---

## L'univers Spring

C'est un framework libre pour concevoir des applications Java. Spring s'occupe de l'exécution globale de l'application. Les développeurs peuvent se concentrer sur la configuration du projet et les traitements métiers.

- **Spring Core** : coeur de Spring qui gère la création et le cycle de vie des objets avec les annotations `@Autowired`, `@Controller`, `@Service`, `@Repository`, etc...
- **Spring MVC** : permet de construire des applications web basé sur l'API Servlet
- **Spring WebFlux** : permet de construire des applications web réactives
- **Spring Data** : permet de gérer le mapping objet-relationnel (ORM)
- **Spring Batch** : permet de gérer les traitements par lots
- **Spring Security** : fournit des fonctionnalités d'authentification, d'autorisation et de sécurité
- **Spring Boot** : permet de créer facilement et rapidement des applications Spring avec un Tomcat embarqué

---

## Spring Boot : les principes

- **les starters** :
  - un starter est un ensemble de dépendances prêt à l'emploi, par exemple pour le starter web, il y a _Spring MVC_, _Jackson_, _Tomcat_...
  - plus besoin de gérer les versions de chaque starter, uniquement la version du starter parent qui va gérer la version de toutes les autres dépendances
- **l'auto-configuration** : permet de configurer automatiquement l'application à partir des jars trouvés dans le classpath (nos dépendances). Plus besoin des fichiers `appconfig-mvc.xml`, `web.xml` et `persitence.xml` (Hibernate)

---

## Rappel sur les versions de Spring Boot

- première version majeure depuis 4 ans et demi (**X**.y.z)
- une version mineure tous les 6 mois (x.**Y**.z)
- corrections de bugs et de sécurité tous les 3-4 semaines (x.y.**Z**)

---

## Support

12 mois minimum pour une "version"

![Support](./diapos/support.png)

---

## Prérequis pour passer

Migration un peu plus _difficile_ qu'une montée de version mineure

- passer à la version 2.7 (fortement conseillé)
- être au moins en Java 17

Spécifique Insee :

- passage à puppet 6 (pas de Java 17 sur puppet 3)

---

## Les principales montées de version de bibliothèques

- Spring 5 (2017) => Spring 6 (novembre 2022)
- Hibernate 5 => Hibernate 6
- Tomcat 9 => Tomcat 10
  - passage de Java EE à Jakarta EE
  - imports `javax.*` deviennent `jakarta.*`
- Spring Batch 4 => [Spring Batch 5](https://docs.spring.io/spring-batch/docs/current/reference/html/whatsnew.html#whatsNew)
- support natif de GraalVM

---

## Retour d'expérience (1)

- montée de version de Spring Security
  - en Spring Boot 2.7, passage en Spring Security 5.8
  - en Spring Boot 3.0, passage en Spring Security 6.0
  - lien de la classe de sécurité : [exemple](https://github.com/gaetan-varlet/formation-api-rest/blob/master/applications/application-serveur-2-springboot/src/main/java/fr/insee/formationapirest/config/SecurityConfigurationKeycloakImpl.java)
- changement dans le mapping d'URL
  - **GET /some/greeting** => OK
  - **GET /some/greeting/** => erreur 404
- renommage des properties
  - utilisation de `spring-boot-properties-migrator`
  - changement au runtime / signalement dans la log

---

## Retour d'expérience (2)

- changement de la dépendance de Springdoc (Swagger)

avant :

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-ui</artifactId>
	<version>${springdoc-openapi.version}</version><!-- 1.6.14 -->
</dependency>
```

après :

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
	<version>${springdoc-openapi.version}</version><!-- 2.0.2 -->
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
