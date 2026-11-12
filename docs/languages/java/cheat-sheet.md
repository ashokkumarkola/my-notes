# Java Cheat Sheet

## JDK

```bash
java -version
javac Main.java          # compile → Main.class
java Main                # run
java Main.java           # run single file directly (Java 11+)
sudo apt install openjdk-21-jdk
```

## Program

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

## Types

| Primitive | Wrapper | Example |
|---|---|---|
| `int` | `Integer` | `int n = 5;` |
| `long` | `Long` | `long l = 5L;` |
| `double` | `Double` | `double d = 1.5;` |
| `boolean` | `Boolean` | `boolean ok = true;` |
| `char` | `Character` | `char c = 'a';` |

```java
String s = "hi";
var list = new ArrayList<String>();   // type inference
final int MAX = 10;                   // constant
```

## Control flow

```java
if (x > 0) { } else if (x == 0) { } else { }
for (int i = 0; i < n; i++) { }
for (String item : items) { }
while (cond) { }

String r = switch (day) {
    case "SAT", "SUN" -> "weekend";
    default -> "weekday";
};
```

## OOP

```java
public interface Shape { double area(); }

public class Circle implements Shape {
    private final double r;
    public Circle(double r) { this.r = r; }
    @Override public double area() { return Math.PI * r * r; }
}

public record User(int id, String name) {}   // immutable data class
```

| Keyword | Meaning |
|---|---|
| `extends` | Inherit class |
| `implements` | Implement interface |
| `abstract` | No instances, partial impl |
| `static` | Belongs to class, not object |
| `final` | Cannot change / override / extend |
| `private / protected / public` | Access levels |

## Collections

```java
List<String> list = new ArrayList<>();      list.add("a"); list.get(0);
Map<String, Integer> map = new HashMap<>(); map.put("a", 1); map.getOrDefault("b", 0);
Set<Integer> set = new HashSet<>();         set.add(1); set.contains(1);
List<Integer> fixed = List.of(1, 2, 3);     // immutable
```

## Streams

```java
List<Integer> evens = nums.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .toList();

int total = nums.stream().mapToInt(Integer::intValue).sum();
```

## Exceptions

```java
try {
    risky();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    cleanup();
}

try (var reader = Files.newBufferedReader(path)) { }   // auto close
```

## Build tools

| Task | Maven | Gradle |
|---|---|---|
| Compile | `mvn compile` | `./gradlew build` |
| Test | `mvn test` | `./gradlew test` |
| Package | `mvn package` | `./gradlew jar` |
| Clean | `mvn clean` | `./gradlew clean` |
| Config | `pom.xml` | `build.gradle` |
