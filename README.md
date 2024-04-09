JPA KI ORM 

# DATA SOURCE 
- Kalo pake Spring Data JPA dan Spring Boot, otomatis dibuatkan DataSource. Jd gperlu bikin scr manual.
- To change DataSource configuration, go to application properties
- Liat konfigurasinya? dengan prefix spring.datasource.*

# JPA CONFIGURATION 

# ENTITY MANAGER FACTORY 
- SB otomatis membuat bean EntityManagerFactory

# TANPA ENTITY MANAGER
- Saat menggunakan Spring Data JPA, kita jarang membuat Entity Manager lagi.
- Spring mmbwa konsep Repository (diambil dari buku Domain Driven Design)
- Repository? an layer to manage data (misalnya di database)

# REPOSITORY
- Setiap entity yg dibuat di JPA, akan dibuatkan Repositorynya
- An interface
- Automatically implementing AOP by Spring
- Make repos? implements JPARepository<T.ID>, Anotation @Repository (optional)

# CATEGORY REPOSITORY 
- JpaRepository adl turunan CrudRepository dan ListCrudRepository, which bnyk method buat operasi CRUD
- G perlu lg pake Entity Manager untuk crud, cukup JpaRepo
- REMEMBER : In Jparepo, create and update method digabung dlm satu method save()

# DECLARATIVE TRANSACTION
- Manajememen
