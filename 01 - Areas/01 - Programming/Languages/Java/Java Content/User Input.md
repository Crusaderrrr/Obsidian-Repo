---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
Need the help of **Scanner**.
![[Pasted image 20250731172929.png]]

**It should be imported it**:
`import java.util.Scanner;`

**Use**:
```java
public class Main {
	public static void main(String [], args) {
	
		Scanner scanner = new Scanner(System.in);

		System.out.printLn("Enter your name: ");
		String name = scanner.nextLine();

		System.out.printLn("Hello " + name);
	
		scanner.close();
	}
}
```

The scheme is like this: *type* **name** = scanner.**next**<mark style="background: #FF5582A6;">Type</mark>(); 
<mark style="background: #FF5582A6;">Type</mark>  could be Int, Double, Boolean, etc.
For *String* it should be `nextLine();`

# Array input 
```java
import java.util.Scanner;

public class Main {
  public static void main(String [] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Specify the number of foods: ");
    int size = scanner.nextInt();

    String[] foods = new String[size];

    for (int i = 0; i < size; i++) {
      System.out.print("Enter the food's name: ");
      foods[i] = scanner.next();
    }

    for (String food : foods) {
      System.out.println(food);
    }
    scanner.close();
  }
}
```

Could be implemented like this.