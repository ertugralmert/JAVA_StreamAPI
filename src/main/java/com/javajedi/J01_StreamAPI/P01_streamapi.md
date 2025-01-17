# Java Stream API
Bir youtube videosu çektiğinizi ve yüklediğinizi var sayalım.  
Video boyuyu 300mb olsun.  
1. Senaryo -> önce video kullanıcının bilgisayarına indirilir sonra kullanıcı videoyu kesintisiz bir şekilde izlemeye başlar.  
 Bir internet sitesine giridğimizde öncelikle tüm bilgilerin pc'ye yüklenmesi gerekir. (html gbi)
1 byte -> 8 bit ; 100mbit -> 12.5mb/s  
Burada bu durum çok uzun zaman alabilir.  
Fazla boyutlu bir video indrmek istediğiniz için kotanız dolabilir  
bir videoyu sadece göz gezdirmek için bile açsan beklemek zorundasın.  
sunucu tarafında da fazlaca yük oluşur.  
Tek olumlu yönü indirdikten sonra kesintisiz izlemek.  
bu doğru bir yöntem değildir.
2. Senoryo:  
Video olabildiğince küçük parçalara bölünü ve her bir parça ayrı ayrı indirilir. bu indirme  
işlemi kullanıcı bir sonraki parçayı izlemek istediğinde yada ona akış olarak yaklaştığında indirilir.  
Buna Stream diyebilir.  

> Stream de yapılan işlemler kullandıktan sonra silinir . Bellek şişirme gibi durumlar olmuyor.

```java
import java.util.stream.Stream;

public class RunnerStream() {
    public static void main(String[] args) {
        //Stream sınıfını kullanacağız.
        Stream<String> bosStream = Stream.empty(); // boş bir steam, count = 0;
        System.out.println("bosStream= "+ bosStream.count());
        // birdaha çalıştırmak istediğimizde hat alırız. HATA -> Stream has already been operated upon or closed
        // tekrar kullanmak için yeni bir tnaımlama gerekir.
        System.out.println("bosStream= "+ bosStream.count()); // hata fırlatacak.
        
        Stream<String> tekKayit = Stream.of("Mert"); // count : 1
        System.out.println("tek kayit: "+ tekKayit.count());
        
        Stream<String> cokluStream = Stream.of("Mert","Dilara","Ayşse"); //count 3
        System.out.println("Çoklustream: "+ cokluStream.count());
        
        //Görüldüğü gibi tek kullanım yapıyoruz her seferinde
        
    }
}
```
### Stream API
Kendi başına fonsiyonal programlamayı içinde barındıran bir yapıdır. Genel olarak  
tüm uygulamarda data saklamak için Collections kullanırız, ancak bu dataları işlemek için  
Stream Kullanmamız gereklidir.  
Peki Collections lar stream'e nasıl dönüşür?

```java
import java.util.stream.Stream;
public class Runner{
    public static void main(String[] args) {
        List<String> haftaninGunleri = List.of("Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma", "Cumartesi", "PAzar");
        Stream<String> streamHaftaninGunleri = haftaninGunleri.stream(); //stream'e çevirdik
        streamHaftaninGunleri.filter(gun->gun.contains("i")).forEach(System.out::println);
// içinde i harfi geçenleri incele
        // streamHaftaninGunleri.filter(gun->gun.contains("i")).forEach(System.out::println);
// yukarıdaki çalışmayacak çünkü 2 defa kullanılmaz.
        
        //ancak bu tek seferlik kullanım çok saçma
        // aşağıdaki gibi aynı stream'i defalarca kullanabiliriz.
        haftaninGunleri.stream().filter(gun->gun.contains("i")).forEach(System.out::println);
        haftaninGunleri.stream().filter(gun->gun.contains("ş")).forEach(System.out::println);
        haftaninGunleri.stream().filter(gun->gun.contains("Ç")).forEach(System.out::println);
        haftaninGunleri.stream().filter(gun->gun.contains("s")).forEach(System.out::println);
    }
}



```
### Stream Fonksiyonları
1- Sonsuz stream

```java
import java.util.stream.Stream;

public class Runner() {
 public static void main(String[] args) {
  Stream<Double> sonsuzSayiDizisi = Stream.generate(Math::random); //0-1 arasında rastgele sayı üretecek
  // yukarıdaki stream bize maliyeti 0. Ancak kullanmaya başladıkça biz bırkaana kadar maliyeti artacaktır.
  // aşağıdaki method'a sleep ekleyceğiz ki pc'niz bağırmasın sonsuz döngü olacak
  sonsuzSayiDizisi.forEach(sayi->{
   System.out.println("sayı =" + sayi);
   try{
       Thread.sleep(1000L);
   }catch (Exception exception){
       
   }
  });
  // 1000,1995,3985 ....
  Stream<Integer> sayilar = Stream.iterate(1000, s-> s*2 -5);
  sayilar.forEach(sayi->{
   System.out.println("sayı =" + sayi);
   try{
    Thread.sleep(1000L);
   }catch (Exception exception){

   }
  });
  
  Stream<Integer> sonsuzSonluSayiListesi = Stream.iterate(400_000,s->402_000, s-> s+ 150);
  sonsuzSonluSayiListesi.forEach(sayi->{
   System.out.println("sayı =" + sayi);
   try{
    Thread.sleep(1000L);
   }catch (Exception exception){

   }
  });
 }
}
```
### reduce
```java
public class Runner(){
 public static void main(String[] args) {
  String[] adiniz = new String[]{"M", "E", "R", "T"};
  for(String ad: adiniz)
      isminiz.append(ad);
  System.out.println("isminiz: "+isminiz);
  
  //bunu stream ile yalım
  
 }
}
```

```java
import java.util.stream.Stream;

public class Runner() {
 public static void main(String[] args) {
  Stream<String> streamAdiniz = Stream.of("M", "E", "R", "T");
  String ifade = streamAdiniz.reduce("",(x,y)->x+y);
  System.out.println("ifade: "+ifade);
  
  // Bunu eski konulara göre yapsaydık
  String[] adiniz = new String[]{"M", "E", "R", "T"};
  StringBuilder isminiz = new StringBuilder();
  for (String ad: adiniz)
      isminiz.append(ad);
  System.out.println("isminiz: "+ isminiz);
 }
}
```
* Notların ortalamasını alalım  
```java
public class Runner() {
 public static void main(String[] args) {
     Stream<Integer> ogrenciNotlari = Stream.of(56,87,34,98,32,50);
     int toplam = ogrenciNotlari.reduce(0,(x,y)->x+y);
  System.out.println("ortlama: " + (toplam/6));
 }
}
```


