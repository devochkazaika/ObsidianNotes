```
implementation 'org.mapstruct:mapstruct:1.4.2.Final'  
annotationProcessor 'org.mapstruct:mapstruct-processor:1.4.2.Final'
```
Создаем интерфейс
```java
public interface Mappable<E, D>{  
    E toEntity(D dto);  
    D toDto(E entity);  
}
```
Делаем компоненту для спринга
```java
@Mapper(componentModel = "spring")  
public interface DataMapper extends Mappable<Data, DataDto> {}
```
