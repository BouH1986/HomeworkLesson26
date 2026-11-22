Урок 26. Понимание JVM


public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}


ClassLoaders пытается найти и загрузить класс JvmComprehension, 
Application ClassLoader передает в Platform ClassLoader, а тот Bootstrap ClassLoader. 
Bootstrap ClassLoader ищет класс, если находит загружает, если не находит отдает 
Platform ClassLoader, тот в свою очередь так же ищет и если не находит отдает в 
Application ClassLoader, в итоге класс загружается в Metaspace.  

Затем происходит Linking - связывание: 
Verify - проверка, что код валиден, 
Prepare - подготовка, 
Resolve - разрешение ссылок на другие классы. 

Далее происходит инициализация - выполняются static инициализаторы и
инициализаторы static полей.

0 - создается фрейм в стеке void main  
1 - создается фрейм в стеке "int i = 1";  
2 - создается объект класса "Object" в куче и ссылка "o" в стеке  
3 - создается объект класса "Integer" в куче и ссылка "ii" в стеке  
4 - создается фрейм в стеке "printAll", параметрами передаются ссылки на объекты в куче  
5 - создается объект класса "Integer" в куче и ссылка "uselessVar" в стеке  
6 - создается фрейм в стеке куда передаются ссылки на объекты "o", "i", "ii"  
7 - создается фрейм в стеке куда передается ссылка на объект со строкой, содержащей "finished"  
по завершению выполнения программы сборщик мусора удаляет все объекты и ссылки на них  






