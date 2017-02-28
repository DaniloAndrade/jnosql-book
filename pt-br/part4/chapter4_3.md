## CrudRepisotry

Além dos repositórios de família de colunas e também de documentos o Artemis também possui o CRUDRepository. Essa interface tem como objetivo auxiliar na criação de classes repositórios específicas paraas entidadesalém de facilitar na criação de uma query.

Para utilizar esse recurso é necessário apenas criar uma interface que extenda de **CrudRepository**.

```java
    interface PersonRepository extends CrudRepository<Person> {

    }
```

E injete o recurso, é necessário definir também o qualificador Database que será responsável por dizer para qual tipo de banco a informação será enviada.

```java
@Inject
@Database(DatabaseType.DOCUMENT)
private PersonRepository documentRepository;
@Inject
@Database(DatabaseType.COLUMN)
private PersonRepository columnRepository;
```

  
Com isso o Artemis se encarregará de utilizar o apropriado banco de dados e cuidará de implementar os métodos.



```java
PersonRepository repository = null;

Person person = new Person();
person.setNickname("diana");
person.setName("Diana Goodness");

List<Person> people = Collections.singletonList(person);

repository.save(person);
repository.save(people);
repository.save(people, Duration.ofHours(2));
repository.update(person);
repository.update(people);
repository.update(people);
```


