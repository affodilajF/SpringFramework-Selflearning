
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
- Saat sebuah object kita masukkan kedalam Spring Container IoC, maka object tersebut adalah Bean
- By default, bean adalah singleton.

  
### Cara membuat? 
- Untuk membuat bean, kita bisa membuat method di dalam class Configuration.
- Nama method tsb akan menjadi nama beannya, dan return object menjadi object beannya.
- Anotated as @Bean
- Secara otomatis Spring akan mengeksekusi method tersebut, dan return valuenya akan dijadikan obect bean, secara otomatis, dan disimpan di container IoC.

# Duplicate Bean 
- We can register the bean which have same data type
- But the name of the bean should be different each other
- To access the bean, we have to specify the bean name. If none is specified, Spring will be confused about which bean is intended
  
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/1041fae6-113e-4b7d-86a2-ffd62a84f8e2)
  ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/a14d8f4b-572f-40e8-89f3-6079d57f2d2a)

# Primary Bean 
- Pas ada diplicate bean, kita bs bikin satu bean jadi bean primer.
- Jd ntar kita bisa mengakses bean tanpa menyebutkan nama beannya.
- @Primary

# Mengubah Nama Bean 
- By default, bean name is the method name
- Tp bisa diubah
- Gunain method value() milik anotasi @bean
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/bbc3b17e-2613-4d0c-83d5-f43f42234634)

# Dependency Injection 
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

# Circular Dependencies 
- Saat bean A butuh B, B butuh C, C butuh D
- Spring bakalan mendeketksi ini, ntar error

# Depends On 
- Kalo beannya ada DI => object dependenciesnya dibuat duluan
- Kalo beannya gaada DI => urutan pembuatan object bean dilakukan secara random
- Kalo mau ada urutannya, pake anotasi @DependsOn(value={"namaBean"}), maka otomatis bean tsb dibuat setelah bean yang di mention.

# Lazy Bean 
- Bean biasanya dibuat pas awal bat
- Tp bisa dibuat ntar kalo pengen/dibutuhin
- anotasi @Lazy pada beannya

# Scope 
- merupakan strategy cara sebuah object dibuat
- by default, singleton
- Untuk mengubah scope sebuah bean, @Scope(value="namaScope")
- ![image](https://github.com/affodilajF/SpringFramework-Selflearning/assets/130672181/17e2f02b-844d-48f4-a6d6-1cd6bfa076a2)

# Membuat Scope 
- You can create your own scope

# 


















