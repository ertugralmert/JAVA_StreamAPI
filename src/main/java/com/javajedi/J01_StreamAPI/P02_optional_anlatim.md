# Optional
Normal şartlarda bir değerin Null olup olmadığını kontrol etmeliyiz.  
Undefined -> Null  
Eğer çağırdığımız değer yoksa o bize NullPointerException fırlatır.  
örn: satis.getFiyat(); -> eğer yoksa NullPointerException hatası alırız.

```java
import java.util.Optional;

public class Runner() {
    public static void main(String[] args) {
        // Normal şartlarda if ile null kontrol edebiliriz ama bu saçma olur
        if (ifade != null) {
            System.out.println(ifade.length());
        }

        // Bunun yerine "optional" kavramını kullanırız.
        // Daha anlamlı ve düzenli bir yapı olur.
        Optional<String> isim; // tanımlama
        isim = Optional.of("mert"); // içinde değer olan bir optional tanımlar.
        if (isim.isEmpty()) { // optional değişkeni boş ise true döner
            System.out.println("isim boştur");
        }
        isim = Optional.empty(); // içinde boş olan bir optional tanımlar.
        if (isim.isPresent()) { // optional değişkeni boş degilse true döner
            System.out.println("Bir isim tanımlanmıştır");
        }
        // Dikkat!!! Boş olduğu halde get ile okuma yaparsak değer null döner 
        String optionalDeger = isim.get(); // Optional değişkeninin içindeki değeri alır
        /**
         * Buradaki amaç null yok etmek değil. Bu yapı diyorki bak bu değer null gelebilir ona göre kullan!!
         */
        

    }
}
```
