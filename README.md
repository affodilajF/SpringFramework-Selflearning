
# Inversion Of Control (IoC)
- An principal in software development
- Migrating the control of object or program to framework container.
- An IoC Framework => Container IoC memiliki kontrol untuk mengeksekusi program kita, memanajemen object pada program kita, dan melakukan abstraction terhadap program kita.
- Saat menggunakan framework IoC, biasanya kita mengikuti cara kerja framework tersebut

### Spring adalah IoC
Ada applicationContext, adalah containernya spring IoC. 
Biasanya kan bikin kode di main class dll, tp kalo IoC engga, semuanya diserahkan ke mereka2. 

![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/8435e258-75da-4a1e-805e-3742fbf946f3)

# Application Context
- An interface
- Representation of container IoC in Spring
- Banyak class implementasinya, secara garis besar dibagi menjadi 2 jenis implementasi => XML dan Annotation.
- menampung konfigurasi dan dependensi aplikasi. Application context digunakan untuk mengelola pembuatan dan inisialisasi bean, dan untuk menyediakan akses ke bean tersebut untuk komponen lain dalam aplikasi.


# Configuration 
- To make ApplicationContext, we need Configuration Class
- Annotated as @Configuration
- kelas tersebut berisi konfigurasi untuk Spring Container.
- Kelas config bean dapat dibuat berkali-kali, namun method bean tetap bersifat static.

![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/45da0024-1498-499b-8daf-53682423d509)

# Singleton 
- Design Patterns untuk pembuatan object
- Objet is only created once
- Objeknya satu, dipake terus-terusan kalo diakses berkali-kali
- SPRING BY DEFAULT SELALU SINGLETON 

### Cara membuat? 
-> Static method 

# Bean 
Ada 2 cara pembuatan bean : 
- @Bean
- @Component

## Bean (ordinary bean, @Bean) --------------------
- Saat sebuah object kita masukkan kedalam Spring Container IoC, maka object tersebut adalah Bean
- By default, bean adalah singleton.

  
### Cara membuat? 
- Untuk membuat bean, kita bisa membuat method di dalam class Configuration.
- Nama method tsb akan menjadi nama beannya, dan return object menjadi object beannya.
- Anotated as @Bean
- Secara otomatis Spring akan mengeksekusi method tersebut, dan return valuenya akan dijadikan obect bean, secara otomatis, dan disimpan di container IoC.

### Duplicate Bean 
- We can register the bean which have same data type
- But the name of the bean should be different each other
- To access the bean, we have to specify the bean name. If none is specified, Spring will be confused about which bean is intended
  
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/1041fae6-113e-4b7d-86a2-ffd62a84f8e2)
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/a14d8f4b-572f-40e8-89f3-6079d57f2d2a)

### Primary Bean 
- Pas ada diplicate bean, kita bs bikin satu bean jadi bean primer.
- Jd ntar kita bisa mengakses bean tanpa menyebutkan nama beannya.
- @Primary

### Mengubah Nama Bean 
- By default, bean name is the method name
- Tp bisa diubah
- Gunain method value() milik anotasi @bean
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/bbc3b17e-2613-4d0c-83d5-f43f42234634)

### Dependency Injection 
- Saat membuat object, kita sering membuat object yang bergantung dengan object lain.
- Dependency Injection (DI) adalah teknik dimana kita bisa mengotomisasi proses pembuatan object yang bergantung dengan object lain (called dependencies)
- Dependencies akan secara otomatis di-inject (dimasukkan) kedalam object yang membutuhkannya
- Ga wajib pake DI, tp kalo appnya dah kompleks, bakalan sangat membantu. 

- Spring tu IoC yang pake DependencyInjection

- Ini manual :
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/ca862c61-6e3e-41c3-ba1d-c2d0a727be04)

- Ini pake DI :
  - Bean bisa memiliki parameter
  - Parameter akan dicarikan di bean yang lain, kalo gada, error
  - ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/50362fe4-dcaf-4faa-b7ba-e93109a09b5f)
  - Duplicate bean? @Qualifier(value="namaBean")

### Circular Dependencies 
- Saat bean A butuh B, B butuh C, C butuh D
- Spring bakalan mendeketksi ini, ntar error

### Depends On 
- Kalo beannya ada DI => object dependenciesnya dibuat duluan
- Kalo beannya gaada DI => urutan pembuatan object bean dilakukan secara random
- Kalo mau ada urutannya, pake anotasi @DependsOn(value={"namaBean"}), maka otomatis bean tsb dibuat setelah bean yang di mention.

### Lazy Bean 
- Bean biasanya dibuat pas awal bat
- Tp bisa dibuat ntar kalo pengen/dibutuhin
- anotasi @Lazy pada beannya

### Scope 
- merupakan strategy cara sebuah object dibuat
- by default, singleton
- Untuk mengubah scope sebuah bean, @Scope(value="namaScope")
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/17e2f02b-844d-48f4-a6d6-1cd6bfa076a2)

### Membuat Scope 
- You can create your own scope

### Life Cycle 
- Spring container memiliki spring container
- Saat pertama kali spring berjalan dan membuat bean, Spring akan memberitahu bean tsb bahwa bean telah siap, artinya semua dependencies sudah dimasukkan.
- Saat spring mati, sping mmbritahu kpd bean bahwa bean tsb akan dihancurkan.

### Life Cycle Callback 
- By default, bean gabisa tahu alur hidup Spring ketika selesai membuat bean dan ketika akan menghancurkan bean
- Jika kita interested untuk bereaksi ketika alur hidup spring terjadi, maka kita bisa implements interface InitializingBean dan DiposableBean.
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/16c2d7b3-1ed7-4052-ace6-d18d20a35070)
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/f50fe251-3067-4da9-8809-941330a0df33)

### Life Cycle Anotation 
- Menggantikan interface InitializingBean dan DisposableBean
- Pakai method @initMethod() dan destroyMethod()
- Methodnya harus tanpa param
- Return value ada po gada bakalan dihiraukan
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/a6d5887e-1cc9-4dd4-90f4-3cb67c494cc7)
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/d338708c-c22f-4b64-9aa6-e414856a5822)

### Import 
- Ntar kita bakalan bikin banyak configuration class
- Untuk mengimoprt gunakan @import
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/741a9c43-20c2-4d8e-8809-0ceefe0a8b42)

### Component scan 
- Secara otomatis mengimport Configuration di sebuah package dan sub package secara otomatis
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/2da94f31-1daa-450b-a63c-b333e30ed7e3)

  
# Component Bean (@Component) -----------------------------
- Cara otomatis membuat bean adalah dengan menggunakan anotasi @Component

  Ini scr otomatis di regist as bean. 
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/231f977f-4c96-46c0-9f7f-8f68421fe200)

- Hanya mendukung pembuatan satu bean
- Constraint
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/303df0e8-78e8-4358-9247-b5500bc7b723)
  
### Constructor Based Dependency Injection in @Component bean
- Only 1 constructor
- Kalo pembuatan bean dengan cara biasa, kita bisa buat suatu bean memiliki DI terhadap bean lain.
- Kalo pembuatan bean dengan @Component, gmn caranya? banyak
  - Pakai constructor param
    ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/c9f027d7-9c91-43b1-8a34-e05d649dbede)
    
    Kelas yang menjadi kelas injectan itu HARUS bean juga!
    
  - Pakai Setter-based Dependency Injection
    ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/a16f8701-7a94-4917-879c-8c26fa429eca)

  - Field-base Depndency Injection
    DI langsung menggunakan field. Pake @Autowired. DAH GK DI REKOMEN SKIP AJ Y
  
#### Multiple constructor 
- @Autowired => menandai contructor mana yang akan digunakan untuk DI pada bean yang @Component  
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/12a5824d-8eab-4769-96c7-e5d7fe84ce28)

### Qualifier in @Component bean
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/ea811318-2b39-4fc8-8c66-493d03df4b43)

# Optional Dependency 
- By default semua dependency itu wajib. Artinya kalo spring gbs nemuin bean yang dibutuhkan saat DI, maka akan terjadi error.
- Tapi bisa dibikin OPTIONAL (tdk wajib)
- Dependency tsb diwrap dengan java.util.Optional<T>
- Bisa menggunakan pada @Bean (method param) ataupun @Component (const param, setter method param, field) 
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/27fb4a4b-58ca-4012-94bd-c2c29ac71bfd)

# Factory Bean 
- We cannot modifying third party library (or other classes yang bukan milik kita) for applying anotations
- Solution? @Bean method or @Component (which are wrapperd by Factory Bean class)
- Contoh :
  Kelas PaymentGatewayClient adalah third party yang gabisa di modif.

  Caranya buat kelas yang implements FactoryBean. Kelas ini bisa ditreatment dengan @Bean dan @Component.
  Terus yauda problem solved.
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/ea59494e-fbb0-4cbb-9933-50fcf9f2a507)

# Inheritance 
- As if you are want to acesses Bean, simply call the class type of the bean.
- Another way is to call using bean's parent class / parent interface
- Example :
  Having an interface called "MerchantService" and bean which implementing that interface called "MerchantServiceImpl",
  to acesses the bean, not only using the MerchantServiceImple but also can be using MerchantService (the parent interface).
- But be careful, MerchantService could possibly having lots of derivative, make sure there not will be error duplicate
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/ef985b45-29d2-4b68-adcb-724aa1c6ee2e)

# Bean Factory
- Adalah interface
- ApplicationContext itu implements BeanFactory

# Listable Bean Factory 
- Turunan BeanFactory
- BeanFactory is only capable to acesses single bean, means jika ada duplicate bean kita hrs sebutkan satu persatu namanya.
- Listable Bean factory bisa digunakan untuk mengakses beberapa bean sekaligus. 

# - 
# - 
# - 
# - 

# Event Listener
- Komunikasi antar kelas menggunakan Event
- Event di spring? Objek turunan dari ApplicationEvent
- Listener di spring? Turunan dari ApplicationListener
- 

# 













