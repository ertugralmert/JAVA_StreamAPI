# Collections Tür Dönüşümleri
Bu kısmı aşğaıdaki gibi açıklayalım.

```java
import java.util.List;
import java.util.TreeSet;

public class Runner() {
    public static void main(String[] args) {
        List<String> isimListesi = List.of("Mert", "Dilara", "Ayşse", "Ali", "Mehmet", "Mahmut", "Mert", "Dilara", "Ayşse");
        /**
         * Set<String> tekrar olmayan liste
         * TreeSet<String>
         */
        //1. Yöntem
        TreeSet<Strip> isimler = isimListesi.stream()
                .collect(TreeSet::new, TreeSet::add, TreeSet::addALL);
        // 2. Yöntem
        TreeSet<String> isimler2 = isimListesi.stream()
                .collect(Collectors.toCollection(TreeSet::new));
        
        //Map<Strig, Integer> -> ad, uzunluk
        Map<String,Integ er> isimUzunlukMap = isimListesi.stream()
                .collect(Collector.toMap(isim->isim, String::length));
    }
}
```