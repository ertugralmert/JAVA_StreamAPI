# Stream Filter
* Bunu bir class ile açıklayalım bir tane Satış class'ımız olduğunu varsayın. veya oluşturun.

```java
import java.util.List;
import java.util.Optional;

public class Runner() {
    // Bir tane Satis clas oluşturun. Urunad, satisfiyatı ekleyin.
    //getter,setter, id, constructor ayarlayın aşağıdaki sınıfı kullanabilrsiniz.
    public static void main(String[] args) {
        List<Satis> satisListesi = new ArrayList<>();
        satisListesi.add(new Satis("Asus Laptop", 65_000));
        satisListesi.add(new Satis("HP 32' Monitör", 15_400));
        satisListesi.add(new Satis("Acer Laptop", 35_500));
        satisListesi.add(new Satis("Macbook Pro", 95_999));
        satisListesi.add(new Satis("Palit VGA Adapter", 39_999));
        satisListesi.add(new Satis("Asrock Motherboard i9", 21_500));
        satisListesi.add(new Satis("Toshiba Laptop", 65_000));
        satisListesi.add(new Satis("Monster Laptop", 50_000));
        satisListesi.add(new Satis("Samsung Monitor 27inch", 18_700));
        satisListesi.add(new Satis("Thermaltech Kasa 100W", 11_200));

        /**
         * x -> benim satış nesnem olsun.
         */
        satisListesi.stream().filet(x -> x.getUrunAdi().contains("Laptop"))
                .forEach(System.out::println);
        //İçinde Laptop içeren ürünleri yazdırır.
        System.out.println("----------------------");
        satisListesi.stream().filter(x -> x.getSatisFiyati() > 50_000)
                .forEach(System.out::println);
        System.out.println("-------------------------");
        satisListesi.stream().filter(satis -> satis.getUrunAdi().startsWith("Sa"))
                .forEach(System.out::println);
        System.out.println("--------------------------");
        List<Satis> findMonitor = satisListesi.stream()
                .filter(x -> x.getUrunAdi().contatins("Monitor")).toList();
        findMonitor.forEach(System.out::println);
        // sonuna toList() ekleyerek bulduklarımız ı listeye dönüştürdük.
        System.out.println("----------------------------");
        // ilk bulduğunu getirsin
        Optional<Satis> bulunan = satisListesi.stream()
                .filter(x -> x.getUrunAdi().equalsIgnoreCase("Acer LAptop"))
                .findFirst(); //findFirst optionaldır.
        /**
         * Şimdi Optional'a eşitledik ancak null gelebilir. Bu bize zaten
         * işaret veriyor dmeiştik. şimdi bunu ekrana  yazdırırken öyle yapalım
         */
        bulunan.ifPresent(s->{
            System.out.println(s.getSatisFiyati());
        });
        
        // İki kkoşul birden kullanabliriz.
        satisListesi.stream()
                .filter(x-> x.getUrunAdi().startsWith("A") && x.getSatisFiyati()>30_000)
                .forEach(System.out::println);

    }
}
```