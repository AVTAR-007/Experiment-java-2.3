# Experiment-java-2.3
Part A: Sorting Employee Objects Using Lambda Expressions
import java.util.*;

class Employee {
    String name;
    int age;
    double salary;

    public Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    @Override
    public String toString() {
        return name + " | Age: " + age + " | Salary: $" + salary;
    }
}

public class EmployeeSorting {
    public static void main(String[] args) {
        List<Employee> employees = new ArrayList<>();
        employees.add(new Employee("Avtar Singh", 21, 55000));
        employees.add(new Employee("Rahul Sharma", 25, 75000));
        employees.add(new Employee("Simran Kaur", 22, 68000));
        employees.add(new Employee("Anjali Mehta", 24, 72000));

        // Sort by name
        employees.sort((e1, e2) -> e1.name.compareTo(e2.name));
        System.out.println("Sorted by Name:");
        employees.forEach(System.out::println);

        // Sort by age
        employees.sort((e1, e2) -> e1.age - e2.age);
        System.out.println("\nSorted by Age:");
        employees.forEach(System.out::println);

        // Sort by salary descending
        employees.sort((e1, e2) -> Double.compare(e2.salary, e1.salary));
        System.out.println("\nSorted by Salary (Descending):");
        employees.forEach(System.out::println);
    }
}
Part B: Filtering and Sorting Students Using Streams
import java.util.*;
import java.util.stream.*;

class Student {
    String name;
    double marks;

    public Student(String name, double marks) {
        this.name = name;
        this.marks = marks;
    }

    @Override
    public String toString() {
        return name + " | Marks: " + marks;
    }
}

public class StudentFilterSort {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
                new Student("Avtar Singh", 82),
                new Student("Rahul Sharma", 67),
                new Student("Simran Kaur", 91),
                new Student("Anjali Mehta", 77),
                new Student("Rohit Verma", 88)
        );

        System.out.println("Students with Marks > 75, Sorted by Marks:");
        students.stream()
                .filter(s -> s.marks > 75)
                .sorted(Comparator.comparingDouble(s -> s.marks))
                .map(s -> s.name + " - " + s.marks)
                .forEach(System.out::println);
    }
}
Part C: Stream Operations on Product Dataset
import java.util.*;
import java.util.stream.*;
import java.util.Map.Entry;

class Product {
    String name;
    double price;
    String category;

    public Product(String name, double price, String category) {
        this.name = name;
        this.price = price;
        this.category = category;
    }

    @Override
    public String toString() {
        return name + " | $" + price + " | " + category;
    }
}

public class ProductStreamOperations {
    public static void main(String[] args) {
        List<Product> products = Arrays.asList(
                new Product("Laptop", 95000, "Electronics"),
                new Product("Smartphone", 55000, "Electronics"),
                new Product("Desk Chair", 12000, "Furniture"),
                new Product("Dining Table", 25000, "Furniture"),
                new Product("Running Shoes", 5000, "Apparel"),
                new Product("T-Shirt", 1500, "Apparel")
        );

        // Group by category
        Map<String, List<Product>> grouped = products.stream()
                .collect(Collectors.groupingBy(p -> p.category));
        System.out.println("Products Grouped by Category:");
        grouped.forEach((cat, list) -> {
            System.out.println(cat + ": " + list);
        });

        // Most expensive in each category
        Map<String, Optional<Product>> maxByCategory = products.stream()
                .collect(Collectors.groupingBy(p -> p.category,
                        Collectors.maxBy(Comparator.comparingDouble(p -> p.price))));
        System.out.println("\nMost Expensive Product in Each Category:");
        maxByCategory.forEach((cat, prod) -> System.out.println(cat + ": " + prod.get()));

        // Average price of all products
        double avgPrice = products.stream()
                .collect(Collectors.averagingDouble(p -> p.price));
        System.out.println("\nAverage Price of All Products: $" + avgPrice);
    }
}
<img width="1024" height="1536" alt="Java Program Outputs and Data Sorting" src="https://github.com/user-attachments/assets/0c49b8b1-00bb-4a01-a248-de6847d74f57" />
