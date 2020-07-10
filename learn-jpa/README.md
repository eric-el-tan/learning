# JPA

[Difference between JPA and Hibernate](https://www.javaguides.net/2018/12/what-is-difference-between-jpa-and-hibernate.html)

- (specification) JPA defines the interface of how to persist, read and manage java data object on databases.
- (implementation) Hibernate implement the JPA interfaces. It is an *Object/Relational Mapping* framework. It focus on how to map java objects to database tables.

## Spring Data JPA

- Spring Data JPA is not a JPA implementation. It is a library/framework that adds an extra layer of abstraction on top of JPA implementation. It focus on the repository layer. It can create JPA repository without writing any boilerplate code.
- e.g. with *JPARepository* implements PagingAndSortingRepository, CRUDRepository interface
- can use predefined method to access data, e.g. findById(), findAll(), save(), delete().
- can even find and sort data, by adding keyword in method names, such as *EqualsTo*, *OrderByAsc*,
   
- e.g. with *JpaSpecificationExecutor*, you define own search critieria

