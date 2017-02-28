# Nectia Java Guidelines

## 1 Abstract

El presente contenido contiene las normas y practicas generales para el desarrollo de software utilizando java 
que deben aplicarse en todos los proyectos desarrollados en Nectia que utilicen este lenguaje.

## 2 Contenido

- [Abstract](#1-abstract)
- [Contenido](#2-ontenido)
- [Java](#3-java)
    - [Nomenclatura](#31-nomenclatura)
    - [Logging](#32-logging)
    - [Inyección de dependencias](#33-inyeccion-de-dependencias)
    - [Documentación de código](#34-documentacion-de-codigo)
- [Pruebas Unitarias](#4-pruebas-unitarias)
- [Spring](#5-spring)
- [JPA](#6-jpa)
    - [Entidades](#61-entidades)
    - [Relaciones](#62-relaciones)
    - [Repositorios](#63-repositorios)
    - [Pruebas](#64-pruebas)
- [Control de versiones](#7-control-de-versiones)
    - [Versionamiento](#71-versionamiento)
    - [Git](#72-git)

## 3 Java

### 3.1 Nomenclatura

Se debe utilizar la nomenclatura estandar de Java, más información se puede ver en: 
http://www.oracle.com/technetwork/java/codeconventions-135099.html

### 3.2 Logging

Se debe utilizar la abstracción slf4j, la cual permite utilizar diferentes implementaciones para realizar el log de la aplicación, 
para este proyecto se utilizará la implementación logback.

Por convención se imprimirá en el log por lo menos lo siguiente:

- Llamada a método con nivel Info.
- Parámetros enviados al método con nivel Debug.
- Parámetros de salida del método con nivel Debug.
- Cada vez que se capture un error mediante TryCatch con nivel Error.
Ej:

```java
private static final Logger LOG = LoggerFactory.getLogger(MiClase.class);

@RequestMapping("/")
public String index(String parametro) {
    LOG.info("Llamada a index");
    if (LOG.isDebugEnabled()){
        LOG.debug("Parametro: {}", parametro);
    }

    //Lógica

    if (LOG.isDebugEnabled()){
        LOG.debug("Respuesta: ");
    }
    return "index";
}
```

### 3.3 Inyección de dependencias

Para la inyección de dependencias se utiliza la especificación JSR 330, la cual utiliza las anotaciones de javax.inject. 
Spring soporta esto y funciona de la misma forma que sus anotaciones, 
por lo que se debe utilizar @Inject en vez de @Autowired, y @Named en vez de @Component o @Service.

### 3.4 Documentación de código

Como estándar de documentación se utilizará JavaDoc con el siguiente detalle por componente:

#### Documentación por archivo

```java
/**
 * {Nombre proyecto}
 * (c) {Año de desarrollo} {Cliente}
 */
```

#### Documentación por clase

```java
/**
 * Descripción de la clase
 * 
 * @author <a href="mailto:desarrollador@nectia.com">Nombre Desarrollador</a>
 * @version 1.0
 */
```

#### Documentación por método

```java
/**
 * Descripción del método
 * @since {Número de versión de la clase en la que se agregó el método (omitir en caso de ser la versión 1.0)} 
 * @param id Descipción del parametro que recibe el método
 * @return Descripción del retorno del método
 */
```

## 4 Pruebas Unitarias

Las pruebas automatizadas permiten verificar que una funcionalidad es correcta sin necesidad de realizar una prueba de usuario, 
esto acelera el proceso de validación de funcionalidades, además es útil cuando se realiza refactorización del código 
o se agrega una nueva funcionalidad para verificar que lo ya desarrollado continue funcionando correctamente.

Cada método debe contar con a lo menos una prueba unitaria, además debe existir a lo menos una prueba de integración 
por cada funcionalidad de negocio de la aplicación, estas se deben excluir de las pruebas ejecutadas durante la compilación.

Para realizar las pruebas se debe utilizar la librería JUnit, en caso de que una función necesite emular una llamada 
a otra función o servicio se deben utilizar mocks mediante la librería mockito.

## 5 Spring

## 6 JPA

### 6.1 Entidades

### 6.2 Relaciones

### 6.3 Repositorios

### 6.4 Pruebas 

## 7 Control de versiones

### 7.1 Versionamiento

Para el correcto nombramiento de cada versión se debe utilizar la convención definida en http://semver.org/, 
la cual define la siguiente estructura: v1.2.3-metadata.

En donde el número “1” corresponde a una versión mayor, este se incrementa cada vez que la aplicación sufre cambios drásticos, 
el “2” se incrementa cuando se agregan nuevas funcionalidades, 
el “3” se incrementa cada vez que se crea una nueva versión con correcciones 
y por último el “-metadata” corresponde a información adicional referente al tipo de versión que es, esta puede ser beta, 
rc (release candidate) o release.

### 7.2 Git

[Cheatsheeps de git](https://zeroturnaround.com/rebellabs/git-commands-and-best-practices-cheat-sheet/)

#### 7.2.1 Gitflow

[Gitflow](https://danielkummer.github.io/git-flow-cheatsheet/index.html) es utilizado en los proyectos que versionen con Git.

Las ramas deben ser creadas con la nomenclatura X-Y-Z, donde:
> X: Es el nombre corto del proyecto
> Y: Es el numero de la funcionalidad en el administrador de tareas (ej. planio)
> Z: Es una descripcion corta de la tarea

> Por ejemplo, si quisieramos crear un login para nuestro proyecto Gestor de copias que esta representada con el numero 13098, deberiamos crear
> una rama con la siguiente nomenclatura.

```
gestcop-13098-crear_login (note la separacion con guion bajo en la descripcion)
```

Al comenzar a trabajar en una nueva funcionalidad de seben realizar los siguientes pasos:
- Se debe crear una rama de funcionalidad, que esta acorde a la misma creada en el gestor de tareas (ej. planio)
- A partir de la rama de funcionalidad se debe crear una rama por tarea 

Los pasos para crear una nueva rama son los siguientes. Es importante recordar que se utiliza gitflow para esto:

1. Si el proyecto es nuevo, debemos inicializar gitflow con la siguiente instruccion. 
```git flow init -d```
Esto permite crear la estructura de ramas por defecto (master, develop, hotfix, etc).
2. Luego en la rama 'develop' creamos un nuevo feature de la siguiente forma:
```git flow feature start [rama-feature]```
Esto crear una nueva rama con nombre [rama-feature], y nos posicionara en la misma
3. Una vez que terminemos nuestro feature lo damos por finalizado con la instruccion
```git flow feature finish [rama-feature]```


### 7.3 SVN (Deprecado)