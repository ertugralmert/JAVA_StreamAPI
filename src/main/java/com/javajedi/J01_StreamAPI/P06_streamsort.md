# Stream Sort
Class mantığında bakalım

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Runner() {
    public static void main(String[] args) {
        List<String> isimListesi = List.of("Mert", "Dilara", "Ali", "Mehmet", "Mahmut", "Ayşse");
        isimListesi.forEach(System.out::println);
        System.out.println("-------------");
        // A'dan Z'ye sırala
        isimListesi.stream()
                .sorted()
                .forEach(System.out::println);
        System.out.println("-------------");
        // Z'den A'ya sırala
        isimListesi.stream()
                .sorted(Comparator.reverseOrder())
                .forEach(System.out::println);
        /**
         * Hiçbir List ile yapılan stream() işlemi gerçek liste üzerinde manipülasyon yapmaz.
         * Yani orjinal liste değişmez .
         * Tree sıralı yapar ve değiştirir.
         */
        isimListesi = new ArrayList<>(List.of("Mert", "Dilara", "Ali", "Mehmet", "Mahmut", "Ayşse"));
        Collections.sort(isimListesi);
        isimListesi.forEach(System.out::println);
        /**
         * Dikkat ->>> collections içinde var olan "sort" method'u 
         * orjinal liste üzerinde manipülasyon yapar liste sıralar. orjinali dğeişir.
         */
    }
}
```