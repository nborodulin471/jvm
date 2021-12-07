# jvm
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
    
 1. Создается локальная переменная в stack memory в frame main
 
 2. ClassLoader загружается класс Object и создается его экземпляр в heap и в переменную в frame main, сохраняется ссылка на область памяти, где лежит этот объект.
 
 3. ClassLoader загружается класс Integer и создается его экземпляр в heap и в переменную в frame main, сохраняется ссылка на область памяти, где лежит этот объект.
 
 4. Т.к наш класс уже был загружен ClassLoader, то в Metaspace храниться информация методах класса. Вызывем метод с параметрами
 
 5. Создается объект в heap и в stack memory в переменной uselessVar сохраняется ссылка на область памяти, где лежит этот объект.
 
 6. Т.к данный класс в коде встречается впервые, то запускается ClassLoader и просходит загрузка данных класа в Metaspace.
 Затем вызывается сам метод, выполняем его. После завершения выполнения данного метода вызывается сборщик мусора который очищает stack frame(а) System.out.println, 
 затем очищается stack frame(а) printAll и в heap удаляется uselessVar т.к не используется. 
 
 7. Этот класс уже загружен, поэтому в Metaspace храниться информация о методах класса. Вызваем метод. После завершения выполнения данного метода 
 вызывается сборщик мусора. По результату которого очищается stack frame(а) main и все объекты в heap т.к дальше они не используются.
