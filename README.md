# Sudden DAO

Quick and easy use of JPA with a DAO so instant it will shock you.

[![pipeline status](https://gitlab.mccollum.enterprises/smccollum/genericentityejb/badges/master/pipeline.svg)](http://gitlab.mccollum.enterprises/smccollum/genericentityejb/pipelines)
[![license](https://img.shields.io/github/license/thorntail/thorntail.svg)](http://www.apache.org/licenses/LICENSE-2.0)

A DAO (Data Access Object) is almost always needed in a java project. Extend the `eisiges.sudden_dao.GenericPersistenceManager` class and that's it.

## Use Cases

1. Query a database for a list of all objects whose values match an object's non-null object member variables

```java
Rock keyRock = new Rock();
keyRock.setColor(Color.BLUE);
List<Rock> blueRocks = rockManager.getMatching(keyRock);
```

2. Retrieve an object's primary key

```java
rockManager.getId(myObject);
```

## Getting started

1. Add sudden-dao to your project

Maven:
```xml
		<dependency>
			<groupId>es.eisig</groupId>
			<artifactId>sudden-dao</artifactId>
			<version>1.0.0-SNAPSHOT</version>
		</dependency>
```

Gradle:
```groovy
repositories {
    mavenCentral()
}

dependencies {
	implementation 'es.eisig:sudden-dao:1.0.0-SNAPSHOT'
}
```

2. Create a class extending `eisiges.sudden_dao.GenericPersistenceManager`

3. Create an empty constructor which calls `super(Class<T> entityClass)`

4. (optional) add additional methods

```java
@Local // javax.ejb.Local
public class UserBean extends GenericPersistenceManager<MyUser, Long> { // MyUser: entity being managed, Long: type of primary key
	public UserBean(){
		super(MyUser.class);
	}

	public TypedQuery<MyUser> getByBirthdateAsc() {
		return this.find().sortBy(MyUser_.birthdate).ascending().build();
	}
}
```

The following functions are exposed by GenericPersistenceManager:

```java
boolean containsKey(K)

T persist(T)

K getId(T)

T save(T)

T get(K)

void remove(T)

void saveAll(List<T>)

void removeAll(List<T>)

List<T> getAll()

boolean isTableEmpty()

List<T> getMatching(T)
```

