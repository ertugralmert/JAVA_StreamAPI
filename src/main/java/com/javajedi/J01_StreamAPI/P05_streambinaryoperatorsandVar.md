# Stream Binary Operators and Var
Bunu class içinde açıklama daha doğru olur.

```java
import java.util.ArrayList;

public class Runner() {
    public static void main(String[] args) {
        // var -> değişkendir 
        int i = 5;
        String ifade = "ifade";
// Aynı türden olmayan değişkenleri bir birbirlerine atayamayız.
        Object o = 5;
        o = "ifade";
        o = new String[5];
        /**
         * Object class'ların atası olduğu için "o" içine istediğimizi atayabiliryiz.
         */
        // var object gibi her türlü değeri alabilir. örnek
        var deger = "Mert";
        var deger2 = 5;
        var deger3 = new ArrayList<>();
        /**
         * var tüm değerleri içerisine alabilir. ancak ilk değer ataması yapıldığında (initialize edildiğinde)
         * o değişkenin türüne ataması yapılır. Yani ilk değer olarak int değer atamış isek
         * "var" değişkeninin türü "int" olur
         */
        deger = "Ayşe";
        deger2 = 14; // ilk integer vemriştik integer alabilir.

    }
}


```
### Binary Operator
Bir operasyon yazılır ve ona göre işlem yapılır.  
örnek verelim.

```java
import java.util.List;
import java.util.function.BinaryOperator;

public class Runner() {
    public static void main(String[] args) {
        BinaryOperator<Integer> opr = (a, b) -> a * b;
        List<Integer> sayiListesi = List.of(1, 2, 3, 4, 5,6,7,8);
        sayiListesi.stream()
                .reduce(opr).ifPresent(System.out::println);
    }
}
```

