# IntelliJ Shortcuts ⌨

* `double tap shift`: Search anything in project. 
* `ctrl + alt`: Refactor / Format Code.
* `ctrl + shift + enter`: Complete current statement.
* `ctrl + /`: Comment line.
* `ctrl + shift + /`: Comment block.
* `hold ctrl + click`: goto declaration/definition.
* `alt + enter`: show intended actions for error fix.
* `alt + insert`: Insert constructor/getters/setters in class.
* `atrl + alt + o`: Remove all un used classes.
* `ctrl + w`: Expand Selection.
* `ctrl + alt + v`: declare the statement in a variable.




# Java Documentation ☕

For more information, use [Oracle's Documentation](https://docs.oracle.com/javase/tutorial/index.html).


<details>
<summary>Topics</summary>

</details>

<details>
<summary>String Buffer / String Builder</summary>

* When using a String, if we try to update the value of an existing String, then instead of updating, it will create a 
  new String. which is not efficient.
* String Buffer and String builder classes are same in terms of implementation.
* The only difference is that String Buffer is `thread safe`, which means they can be used while working with multiple
  threads, which means that if one thread is accessing the String, the other thread has to wait.
* String builder is `not thread safe`.

      // Instantiation and appending
      StringBuffer sbf = new StringBuffer("Osama");
      sbf.append(" Khan");
      System.out.println(sbf);
      
      // Replacing
      sbf.replace(0, 5, "Taha");
      System.out.println(sbf);
      
      // Deleting
      sbf.delete(5, 10);
      System.out.println(sbf);


</details>




<details>
<summary>Streams</summary>

### Streams

Visit the [Page](https://stackify.com/streams-guide-java-8/) or [Video](https://www.youtube.com/watch?v=Q93JsQ8vcwY) for more.

* A simple enum is created:

      public enum Gender {
          MALE, FEMALE
      }

* A person class:

      public class Person {
          private String name;
          private int age;
          private Gender gender;
      
          @Override
          public String toString() {
              return "Person{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      ", gender=" + gender +
                      '}';
          }
      
          public Person(String name, int age, Gender gender) {
              this.name = name;
              this.age = age;
              this.gender = gender;
          }
      
          public String getName() {
              return name;
          }
      
          public void setName(String name) {
              this.name = name;
          }
      
          public int getAge() {
              return age;
          }
      
          public void setAge(int age) {
              this.age = age;
          }
      
          public Gender getGender() {
              return gender;
          }
      
          public void setGender(Gender gender) {
              this.gender = gender;
          }
      }

* Main Function with all the operations:

      public static List<Person> getPeople() {
          return List.of(
              new Person("Osama Khan", 23, Gender.MALE),
              new Person("Fatima Khan", 10, Gender.FEMALE),
              new Person("Hadi Rehman", 25, Gender.MALE),
              new Person("Alina Khan", 67, Gender.FEMALE),
              new Person("Uzair Shah", 45, Gender.MALE),
              new Person("Zeb Khan", 83, Gender.FEMALE),
              new Person("Usman Khan", 102, Gender.MALE),
              new Person("Anar Gul", 96, Gender.MALE)
          );
      }

      public static void main(String[] args) {
      // write your code here
    
            List<Person> people = getPeople();
    
            // Imperative approach means doing stuff using loops and stuff.
            // Declarative Approach means using streams.
    
            // Filtering using streams
            System.out.println("------------ Filtering using streams ------------");
            List<Person> females = people.stream()
                    .filter(person -> person.getGender().equals(Gender.FEMALE))
                    .collect(Collectors.toList());
            females.forEach(System.out::println);
            System.out.println();
    
            // Sorting stuff Ascending
            System.out.println("------------ Sorting stuff Ascending ------------");
            List<Person> sortedWithAge = people.stream()
                    .sorted(Comparator.comparing(Person::getAge))
                    .collect(Collectors.toList());
            sortedWithAge.forEach(System.out::println);
            System.out.println();
    
            // Sorting stuff Descending
            System.out.println("------------ Sorting stuff Descending ------------");
            List<Person> sortedWithAgeDescending = people.stream()
                    .sorted(Comparator.comparing(Person::getAge).reversed())
                    .collect(Collectors.toList());
            sortedWithAgeDescending.forEach(System.out::println);
            System.out.println();
    
            // All Match Ex. Everyone in this list that has an age greater than 50
            System.out.println("------------ All Match ------------");
            boolean allMatchExample = people.stream()
                    .allMatch(person -> person.getAge() > 5);
            System.out.println(allMatchExample);
            System.out.println();
    
            // All Match Ex. Everyone in this list that has an age greater than 5
            System.out.println("------------ Any Match ------------");
            boolean anyMatchExample = people.stream()
                    .anyMatch(person -> person.getAge() > 120);
            System.out.println(anyMatchExample);
            System.out.println();
    
            // All Match Ex. Everyone in this list that has an age greater than 5
            System.out.println("------------ None Match ------------");
            boolean noneMatchExample = people.stream()
                    .noneMatch(person -> person.getName().equals("John"));
            System.out.println(noneMatchExample);
            System.out.println();
    
            // Max
            System.out.println("------------ Max ------------");
            people.stream()
                    .max(Comparator.comparing(Person::getAge))
                    .ifPresent(System.out::println);
            System.out.println();
    
            // Min
            System.out.println("------------ Min ------------");
            people.stream()
                    .min(Comparator.comparing(Person::getAge))
                    .ifPresent(System.out::println);
            System.out.println();
    
            // Grouping
            System.out.println("------------ Grouping ------------");
            Map<Gender, List<Person>> groupByGender = people.stream()
                    .collect(Collectors.groupingBy(Person::getGender));
            groupByGender.forEach((gender, people1) -> {
                System.out.println(gender);
                people1.forEach(System.out::println);
                System.out.println();
            });
    
            // Example: out of all females, print the name of female with the lowest age.
            System.out.println("------------ Example ------------");
            Optional<String> youngestFemaleAge = people.stream()
                    .filter(person -> person.getGender().equals(Gender.FEMALE))
                    .min(Comparator.comparing(Person::getAge))
                    .map(Person::getName);
            youngestFemaleAge.ifPresent(System.out::println);
            System.out.println();
      }


</details>


<details>
<summary>Date, Time and Number Formatting</summary>

### Date, Time, Currency and Number Formatting
  
* Symbol Representation.

  M = `month`, m = `minute`, y = `year`, d = `day`, s = `second`, h = `hour`, E = `dayName`


* Creating a new Locale

      // Create a default locale
      Locale usLocale = Locale.US; // prints: en_US
      
      // Create a Locale if not available by default
      Locale myLocale = new Locale("en", "IN"); // prints: en_IN

* Print a date using a locale

      DateFormat df_US = DateFormat.getDateInstance(DateFormat.DEFAULT, Locale.US);
      System.out.println(df_US.format(new Date())); // prints: Jan 14, 2021

      DateFormat df_UK = DateFormat.getDateInstance(DateFormat.DEFAULT, Locale.UK);
      System.out.println(df_UK.format(new Date())); // prints: 14 Jan 2021


* Printing Currencies with locale

      NumberFormat x = NumberFormat.getCurrencyInstance(Locale.US);
      Locale indiaLocale = new Locale("en", "IN");
      Locale pakLocale = new Locale("en", "PK");

      NumberFormat us     = NumberFormat.getCurrencyInstance(Locale.US);
      NumberFormat india  = NumberFormat.getCurrencyInstance(indiaLocale);
      NumberFormat china  = NumberFormat.getCurrencyInstance(Locale.CHINA);
      NumberFormat france = NumberFormat.getCurrencyInstance(Locale.FRANCE);
      NumberFormat pak = NumberFormat.getCurrencyInstance(pakLocale);
      
      System.out.println("US: "     + us.format(12000));
      System.out.println("India: "  + india.format(12000));
      System.out.println("China: "  + china.format(12000));
      System.out.println("France: " + france.format(12000));
      System.out.println("Pakistan: " + pak.format(12000));


* Date and time classes and their instantiations are shown below:

      // Local date class
      LocalDate ld = LocalDate.now(); // get current date
      LocalDate ld2 = LocalDate.of(2021, Month.JANUARY, 13); // using month as an enum
      LocalDate ld3 = LocalDate.of(2021, 1, 13);
      System.out.println(ld2);
  
      // Local Time class
      LocalTime lt = LocalTime.now();
      LocalTime lt2 = LocalTime.of(9, 6, 3);
      System.out.println(lt);
  
      // Local date time class
      LocalDateTime ldt = LocalDateTime.now();
      System.out.println(ldt.toString());
  
      // Instant, quite similar to local date time, but with zone
      Instant i = Instant.now();
      ZonedDateTime zdt = i.atZone(ZoneId.of("Asia/Kolkata"));
      System.out.println(zdt);
  
      // creates a locale.
      Locale l = new Locale("en", "pk");
      System.out.println("locale language: " + l.getDisplayLanguage());
      System.out.println("locale Country: " + l.getDisplayCountry());

* A function that takes a date and locale, returns date in the required format:

      public static String getFormattedDate(LocalDate date, Locale locale) throws DateTimeException, NoLocaleFoundException, ParseException {
          DateFormat currentFormat = new SimpleDateFormat("yyyy-MM-dd");
          if (locale.getCountry().equals("UK")) {
              DateFormat targetDateFormat = new SimpleDateFormat("dd-MM-yyyy");
               return targetDateFormat.format(currentFormat.parse(date.toString()));
          } else if (locale.getCountry().equals("US")) {
              DateFormat targetDateFormat = new SimpleDateFormat("MM-dd-yyyy");
              return targetDateFormat.format(currentFormat.parse(date.toString()));
          } else {
              throw new NoLocaleFoundException("The Given locale is not available.");
          }
      }

      // Calling the above function in main class.
      try {
          System.out.println("US DateFormat: " + getFormattedDate(LocalDate.now(), new Locale("en", "us")));
          System.out.println("UK DateFormat: " + getFormattedDate(LocalDate.now(), new Locale("en", "uk")));
      } catch (Exception ex) {
          System.out.println("Exception occurred: " + ex.getMessage());
      }

* A function that takes a number and rounds off the number upto given decimal places:

      // String buffer, Fix this.
      public static double getFormattedNumber(double number, int decimalPlaces)
        throws NumberFormatException {
          BigDecimal bigDecimal = new BigDecimal(Double.toString(number));
          bigDecimal = bigDecimal.setScale(decimalPlaces, RoundingMode.HALF_UP);
          return bigDecimal.doubleValue();
      }
    
      // calling the above funtion in main 
      try {
          System.out.println("Formatted Number: " + getFormattedNumber(24.45546, 1));
      } catch (Exception ex) {
          System.out.println("Exception occurred: " + ex.getMessage());
      }




</details>


<details>
<summary>Exceptional Handling</summary>

### Exceptional Handling

* Exceptions are handled by simply adding try-catch-finally block on the code in which the exception
can occur:

      try {
          int[] x = {1, 2};
          System.out.println(x[4]);
      } catch (ArrayIndexOutOfBoundsException ar_ex) {
          System.out.println("Index of array is out of bounds: " + ar_ex);
      } catch (Exception ex) {
          System.out.println("There is an Exception: " + ex);
      } finally {
          System.out.println("Close Connection");
      }

* `Note:` "Finally" always gets executed, even is exception is caught or not.
* We can catch specific exceptions by using their name in the catch block or just handle any exception by using Exception in the catch block.
* We can through an exception on runtime to handle it:

      try {
          int x = 0;
          int y = 10 / x;
  
          if (x == 0) {
              throw new Exception();
          }
      } catch (Exception ex) {
          System.out.println("Exception occurred: " + ex.getMessage());
      }

* We can also create our own custom exceptions.

      public class YCannotBeZero extends Exception {
          public YCannotBeZero(String message) {
              super(message);
          }
      }
  
* Now we can throw this exception. 
  
      try {
          float x = 20;
          float y = 10 - x;

          if (y < 0) {
              throw new YCannotBeZero("Y cannot be less than 0");
          }
      } catch (YCannotBeZero | AnyOtherException ex) {
          System.out.println("Exception occurred: " + ex.getMessage());
      }

* We can also specify or mark functions if they can through some exceptions

      public void main getData(int id) throws IOException, IndexOutOfBoundsException {
          // Code
      }

</details>

<details>
<summary>Hibernate</summary>

### 1. Setup MySQL

* Install MySQL.
* Open CMD in the `C:\Program Files\MySQL\MySQL Server 8.0\bin` path, and enter the following command:

      mysql -u root -p

* It will ask for a password, enter the password and now we have access to MySQL.
* Now create a user to access the database using the following command.

      CREATE USER 'dbadmin'@'localhost' IDENTIFIED BY 'password';

* Once the user is created, you can check if the user exists by using the following command:

      SELECT user FROM mysql.user;

* Now create a database using the following query:
  
      CREATE DATABASE testdb;
  
* Create a table using the following query. Make sure to select the database using `use databaseName` command to select the database for table creation.
  
      CREATE TABLE Employee (
        firstName VARCHAR(30) NOT NULL, 
        lastName VARCHAR(30) NOT NULL, 
        employeeId INT UNSIGNED NOT NULL PRIMARY KEY
      );

  The `show tables` command will show all tables in the database, and `describe tablename` command will show details of the table.


* Now we have to give privileges to the user that we just created in order to access the database. use the query below to assign privileges.

       GRANT ALL PRIVILEGES ON testdb.employee TO 'dbadmin'@'localhost' WITH GRANT OPTION;

* To check the privileges of a user, use the following query:

      SHOW GRANTS FOR 'dbadmin'@'localhost';

### 2. Setup Classes

* Create a new XML file called `persistence.xml` inside the `main/resources/META-INF` folder.
* Add the following contents in the `persistence.xml` file:

      <?xml version="1.0" encoding="UTF-8" ?>
      
      <persistence version="2.0"
      xmlns="http://java.sun.com/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://java.sun.com/xml/ns/persistence http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd">
      
          <!-- Define a name used to get an entity manager. Define that you will
          complete transactions with the DB  -->
          <persistence-unit name="JavaTraining" transaction-type="RESOURCE_LOCAL">
      
              <!-- Define the class for Hibernate which implements JPA -->
              <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
              <!-- Define the object that should be persisted in the database -->
              <class>com.contour.hibernate.Employee</class>
              <properties>
                  <!-- Driver for DB database -->
                  <property name="javax.persistence.jdbc.driver" value="com.mysql.jdbc.Driver" />
                  <!-- URL for DB -->
                  <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost/testdb" />
                  <!-- Username -->
                  <property name="javax.persistence.jdbc.user" value="dbadmin" />
                  <!-- Password -->
                  <property name="javax.persistence.jdbc.password" value="admin" />
              </properties>
          </persistence-unit>
      </persistence>

  Note that the contents in the persistence.xml file contains information about the user, database, classes etc
  

* Now add a class, which will be served as an entity in relation with the database.

      import javax.persistence.*;
      import java.io.Serializable;
      
      @Entity(name = "employee")
      @Table(name = "employee")
      public class Employee implements Serializable {
      
          // Properties
      
          @Id
          @Column(name = "employeeId", unique = true)
          private int employeeId;
      
          @Column(name = "firstName", nullable = false)
          private String firstName;
      
          @Column(name = "lastName", nullable = false)
          private String lastName;
      
      
          // Getters and Setters
          public int getEmployeeId() { return employeeId; }
          public void setEmployeeId(int employeeId) { this.employeeId = employeeId; }
          public String getFirstName() { return firstName; }
          public void setFirstName(String firstName) { this.firstName = firstName; }
          public String getLastName() { return lastName; }
          public void setLastName(String lastName) { this.lastName = lastName; }
      
      }

* Now add a repository class to perform CRUD operations on the entity:
* An example repository class with main function is shown below:

      import javax.persistence.*;
      import java.util.*;
    
      public class Main {
      
          // Creating Entity Manager
          private static final EntityManagerFactory ENTITY_MANAGER_FACTORY = Persistence
                  .createEntityManagerFactory("JavaTraining");
      
          // CRUD Operations
          public static void addEmployee(int id, String firstName, String lastName) {
              EntityManager em = ENTITY_MANAGER_FACTORY.createEntityManager();
              EntityTransaction et = null;
              try {
                  et = em.getTransaction();
                  et.begin();
                  Employee emp = new Employee();
                  emp.setEmployeeId(id);
                  emp.setFirstName(firstName);
                  emp.setLastName(lastName);
                  em.persist(emp);
                  et.commit();
              } catch (Exception ex) {
                  if (et != null) {
                      et.rollback();
                  }
                  ex.printStackTrace();
              } finally {
                  em.close();
              }
          }
      
          public static void getEmployee(int id) {
              EntityManager em = ENTITY_MANAGER_FACTORY.createEntityManager();
              String query = "SELECT e FROM employee e WHERE e.employeeId = :empId";
              TypedQuery<Employee> tq = em.createQuery(query, Employee.class);
              tq.setParameter("empId", id);
              Employee emp = null;
              try {
                  emp = tq.getSingleResult();
                  System.out.println(emp.getFirstName() + " " + emp.getLastName());
              } catch (NoResultException exception) {
                  exception.printStackTrace();
              } finally {
                  em.close();
              }
          }
      
          public static void getEmployees() {
              EntityManager em = ENTITY_MANAGER_FACTORY.createEntityManager();
              String query = "SELECT e FROM employee e WHERE e.employeeId IS NOT NULL";
              TypedQuery<Employee> tq = em.createQuery(query, Employee.class);
              List<Employee> emps;
              try {
                  emps = tq.getResultList();
                  for (Employee e : emps) {
                      System.out.println(e.getFirstName() + " " + e.getLastName());
                  }
              } catch (NoResultException exception) {
                  exception.printStackTrace();
              } finally {
                  em.close();
              }
          }
      
          public static void updateFirstNameOfEmployee(int id, String firstName) {
              EntityManager em = ENTITY_MANAGER_FACTORY.createEntityManager();
              EntityTransaction et = null;
              Employee emp = null;
              try {
                  et = em.getTransaction();
                  et.begin();
                  emp = em.find(Employee.class, id);
                  emp.setFirstName(firstName);
                  em.persist(emp);
                  et.commit();
              } catch (Exception ex) {
                  if (et != null) {
                      et.rollback();
                  }
                  ex.printStackTrace();
              } finally {
                  em.close();
              }
          }
      
          public static void deleteEmployee(int id) {
              EntityManager em = ENTITY_MANAGER_FACTORY.createEntityManager();
              EntityTransaction et = null;
              Employee emp = null;
              try {
                  et = em.getTransaction();
                  et.begin();
                  emp = em.find(Employee.class, id);
                  em.remove(emp);
                  et.commit();
              } catch (Exception ex) {
                  if (et != null) {
                      et.rollback();
                  }
                  ex.printStackTrace();
              } finally {
                  em.close();
              }
          }
      
      
      
          public static void main(String[] args) {
          // write your code here
      
              // Testing Hibernate
      
               // Adding data
               addEmployee(1, "Osama", "Khan");
               addEmployee(2, "Aamir", "Hanif");
               addEmployee(3, "Hadi", "Rehman");
      
              // Getting single employee by Id
              getEmployee(1);
              getEmployee(2);
              getEmployee(3);
      
              // Getting all employees
              getEmployees();
      
              // Updating
               updateFirstNameOfEmployee(3, "Tariq");
      
              // Deletion
              deleteEmployee(3);
      
              ENTITY_MANAGER_FACTORY.close();
          }
      
      }



</details>

<details>
<summary>Data Conversion / Typecasting</summary>

## Data Conversion / Typecasting

* ### Implicit Casting
  
Implicit casting means automatic conversion of one data type to another. see the example below:

    short x = 2;
    int y = x + 2;

According to the above example, we can simply fit `short(2 bytes)` inside an `int(4 bytes)` without any error and conversion.

Hierarchy: `byte > short > int > long > float > double`

`Note: ` There is no data loss in implicit casting.

* ### Explicit Casting

Consider the example below:

    double x = 1.1;
    int y = x + 2; // error
    int y = (int)x + 2; // explicit.

In the above example, we are trying to fit `double(8 bytes)` in an `int(4 bytes)`, which does not make any sense, and we are also getting an error. 

We can force the conversion by using explicit typecasting. In this way, we are taking the most significant 4 bytes 
of a double and fitting it in an integer, and the remaining 4 bytes of double are lost.

`Note: ` There is data loss in explicit casting.

* ### Conversion of Strings

Converting any primitive type into an integer :

      int no = 12;
      String.valueOf(no); // Good
      Integer.toString(no); // Good
      "" + no; // not a good practice

Converting String to any primitive type. Use `PremitiveDatatypeName.parseDTName(strValue)`:

      String myString = "1234";
      int foo = Integer.parseInt(myString);

</details>


<details>
<summary>Math Class</summary>

## Math Class

* Use the following link for [Math](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html) class documentation.

</details>


<details>
<summary>Get Class Type</summary>

### Get Class Type

    String x = "123";
    
    System.out.println(x.getClass()); // prints: class java.lang.String 
    System.out.println(x.getClass().getSimpleName()); // prints: String 
    System.out.println(x instanceof String); // prints: true

</details>

<details>
<summary>Strings</summary>

### Strings

    System.out.println("apple".compareTo("banana")); // prints: -1
    System.out.println("apple".compareTo("apple")); // prints: 0
    if ("apple" == "apple") {} // Compares addresses of strings
    if ("apple".equals("apple")) {} // Compares values of strings

</details>

<details>
<summary>Open Closed Principle</summary>

### Open Closed Principle
Open closed principle states that, a class is `open for extention` and `Closed for modification`.
The example below shows a convert class with a `convertToXML()` method. let's say we have to add a much better method called `convertTOJSON()`. So we can add another function in the same class which is against the open closed principle as we are modifying the class. The class could be an alrady tested class and we may add a bug by modifying it. so we can extend it and add another class that holds `convertToJSON()` function.

    public class Convert {
    
        public void ConvertToXML() {
            System.out.println("Converting data to XML");
        }

        // public void ConvertToJSON() {} // Against OPEN CLOSED PRINCIPLE
    
    }

    public class ConvertToJson extends Convert {
    
        public void convertToJSON() {
            System.out.println("Convert data to JSON");
        }
    
    }

</details>

<details>
<summary>Boxing / Unboxing</summary>

### Boxing / Unboxing

Boxing and Unboxing is explained in the example below.

    public class Person {
    
        protected String name;
    
        public String getName() {
            return this.name;
        }
    
    }

    public class Employee extends Person {
    
        private int salary;

        public int getSalary() {
            return salary;
        }
    
    }

    public static void main(String[] args) {
	// write your code here

        // Normal Instantiations
        Person P = new Person();
        Employee E = new Employee();

        // Instantiations with parent classes/interfaces.
        Object OP = new Person(); // Object is the parent of every class.
        Person PE = new Employee();

        // Accessing methods
        P.getName(); // allowed
        P.getSalary(); // getSalary() is a method in employee, not allowed (error)
        O.getName(); // Not allowed.

        // To make a parent object access the child's method, use typecasting
        ((Person)O).getName(); // Now this will work.
        ((Employee)P).getSalary(); // Now this will work.
        
    }

</details>

<details>
<summary>Collections</summary>

### Collections

`Java Collection Framework`: Collections are the containers that group multiple items in a single group. Store and manipulate data at realtime.

`Collection Framework Hierarchy`: The images below shows the hierarchy:

![](images/LinearCollection.PNG)
![](images/Map.PNG)

* #### ArrayList
  
      // Store only Integers
      ArrayList<Integer> integerList = new ArrayList<Integer>();
      integerList.add(1);
      integerList.add(2);
      integerList.add(3);
      integerList.add(4);
      integerList.add(5);
  
      // Store dynamic data
      ArrayList list = new ArrayList(); // OR // ArrayList<Object> list = new ArrayList<Object>();
      list.add("osama");
      list.add(21);
      list.add(12.90);
  
      // Printing
      System.out.println("Integer List: " + integerList);
      System.out.println("Integer List: " + list);
  
      // getting data from arraylist
      int age = integerList.get(0);
      Object data = list.get(0); // using object since we don't know the type.
      System.out.println(age + " " + data);
  
      // Updating values
      list.set(0, "hadi");
      System.out.println("New List: " + list);
  
      // Contains function
      System.out.println(list.contains(12.9));
  
      // iteration
      for (short i = 0; i < list.size(); i++) {
          System.out.print(list.get(i) + " ");
      }
  
      // iteration using enhanced for loop
      for (Object o : list) {
          System.out.print(o + " ");
      }
  
      // printing using iterator
      Iterator<Integer> it = integerList.iterator();
      // System.out.print(it.next() + " ");
      // System.out.print(it.next() + " ");
      // System.out.print(it.next() + " ");
  
      // iterating through interator, removing element
      while (it.hasNext()) {
          int num = it.next();
          if (num == 4) {
              it.remove();
          }
      }
      System.out.println(integerList);

* #### HashMap
  
      // Creating hashmap
      // It contains other functions just like arraylist.
      // Hashmaps do not have an order
      HashMap<String, Integer> hm = new HashMap<String, Integer>();
      hm.put("osama", 123);
      hm.put("hadi", 12);
      hm.put("aamir", 1);
      System.out.println(hm);
      System.out.println(hm.get("hadi"));
      hm.remove("aamir");
      System.out.println(hm);
      System.out.println(hm.containsKey("osama"));
      System.out.println(hm.containsValue(123));
      hm.replace("hadi", 3434);
      System.out.println(hm);
      System.out.println(hm.keySet());


</details>

<details>
<summary>Generics</summary>

### Generics

</details>

<details>
<summary>Composition and Aggregation</summary>

### Composition Code Example

    class Floors {
      int rooms; // just for understanding
    }
    
    class Building {

        // this should be final.
        private final Floors[] floors;
        
        // Creating instance inside class. Cannot be passed through args.
        public Building() {
            this.floors = new Floors[5];
        }
    }

### Aggregation Code Example

    class Door {
        int hp;
    }
    
    class Car {
        // Not final
        private Door[] doors;
    
        // Passing doors from args for aggregation
        public Car(Door[] doors) {
            this.doors = doors;
        }
    }

</details>


<details>
<summary>Abstraction</summary>

### Abstraction

* For a class to be abstract, at least one method should be abstract. We can also mark a class abstract.
* Classes that are abstract might not have a definition, but the definition is overriden by a child class.
* A method is marked abstract because its definition is meant to be defined by its child class.
* Abstract methods cannot have a body.

      abstract class A {
      
          // Abstract method cannot have a body.
          public abstract void abstractMethod();
      
          // Non Abstract method.
          public void printName() {
              System.out.println("Printing Class A!");
          }
      
      }
      
      // You have to mark this class abstract or define abstractMethod().
      abstract class B extends A {
      
          // This class does not define abstractMethod() from class A.
      
          // Non Abstract method.
          @Override
          public void printName() {
              System.out.println("Printing Class B!");
          }
      
      }
      
      class C extends B {
      
          // For this to implement, we need to mark Class B as Abstract.
          @Override
          public void abstractMethod() {
              System.out.println("Abstract Method!");
          }
      }

</details>


<details>
<summary>Interfaces</summary>

### Interfaces

* Functions declared in an interface should be defined in the class.
* If a class implements more than 1 interfaces, than all the functions from both the interfaces should be defined.
* It is a good practise to declare all the abstract methods in interfaces. Declaring normal methods in interface is not a good practise.

      public interface IWork {
          public abstract void code();
          public void attendMeeting();
      }

      public interface IExercise {
          public void walk();
          public void run();
      }

      public abstract class Person implements IExercise, IWork {
          @Override
          public void walk() {}
      
          @Override
          public void run() {}
      
          @Override
          public void attendMeeting() {}
      }

      public class Employee extends Person {   
          @Override
          public void code() {
              System.out.println("Code!");
          }
      }

</details>


<details>
<summary>Some Concepts</summary>

## Some Concepts

Difference between == and .equals()

    String s1 = new String("osama");
    String s2 = new String("osama");
    System.out.println(s2 == s1); // false, == checks memory address, reference
    System.out.println(s1.equals(s2)); // true, check values

Arrays

    int[] arr1 = new int[] {1, 2, 3, 4, 5};
    System.out.println(Arrays.toString(arr1));

Multi-dimensional arrays

    int [][] arr = new int [2][2];
    arr[0][0] = 4;
    System.out.println(Arrays.deepToString(arr));

Implicit Casting, Automatic casting, no data loss

    // byte > short > int > long > float > double
    short x = 1;
    int y = x + 2;
    System.out.println(y);

Explicit casting, data loss

    float f = 56.4f;
    int g = (int)f + 4;
    System.out.println(g);

Explicit casting for strings

    String num = "123";
    int numToInt = Integer.parseInt(num);
    System.out.println(numToInt);
    String numToString = String.valueOf(numToInt);
    System.out.println(numToString);

Reading input using scanner class

    Scanner scanner = new Scanner(System.in);
    System.out.print("Enter Number: ");
    int number = scanner.nextInt(); // this line reads the input based on the data type.
    System.out.println("Number is: " + number);

For reading strings

    System.out.print("Name: ");
    String name = scanner.next();
    System.out.println(name);

For reading complete lines

    System.out.print("Full Name: ");
    String fullName = scanner.nextLine().trim(); //.trim() removes blank spaces before and after strings
    System.out.println(fullName);

</details>

<details>
<summary>General Documentation</summary>

## Variables

 * ###  4 types of variables
    1. Instance variables: These are non-static variables declared as fields in classes.
    2.  class variables: static variables that are only for the class and not for the objects.
    3. local variables: local variables are simple declared variables.
    4. Parameters: these are the variables that are passed as an argument in a function.

 * ### Naming conventions
    1. java is case-sensitive.
    2. begin the name with a letter instead of an _, or a number or $ sign.
    3. use pascal casing for Classes, Interfaces and camelCasing for variables.
    4. while declaring constants/final, caps all letters and add _ in gaps e.g. static final int BIKE_SPEED;

 * ### Primitive data-types
    1. byte     8-bit       0
    2. short    16-bit      0
    3. int      32-bit      0
    4. long     64-bit      0L
    5. float    32-bit      0.0f
    6. double   64-bit      0.0d
    7. boolean  2-bit       false
    8. char     4-bit       0000
    9. String is not a data-type, it's a class.
    
## Arrays

* ### Arrays Demo
        // Arrays
        // declares an array of integers
        int[] anArray;
    
        // allocates memory for 10 integers
        anArray = new int[10];
    
        // initialize first element
        anArray[0] = 100;
    
        // initialize second element
        anArray[1] = 200;
    
        // and so forth
        anArray[2] = 300;
        anArray[3] = 400;
        anArray[4] = 500;
        anArray[5] = 600;
        anArray[6] = 700;
        anArray[7] = 800;
        anArray[8] = 900;
        anArray[9] = 1000;
    
        System.out.println("Element at index 0: " + anArray[0]);
        System.out.println("Element at index 1: " + anArray[1]);
        System.out.println("Element at index 2: " + anArray[2]);
        System.out.println("Element at index 3: " + anArray[3]);
        System.out.println("Element at index 4: " + anArray[4]);
        System.out.println("Element at index 5: " + anArray[5]);
        System.out.println("Element at index 6: " + anArray[6]);
        System.out.println("Element at index 7: " + anArray[7]);
        System.out.println("Element at index 8: " + anArray[8]);
        System.out.println("Element at index 9: " + anArray[9]);

* ### Declare arrays of other types

        // declare arrays of other types
  
        byte[] anArrayOfBytes;
        short[] anArrayOfShorts;
        long[] anArrayOfLongs;
        float[] anArrayOfFloats;
        double[] anArrayOfDoubles;
        boolean[] anArrayOfBooleans;
        char[] anArrayOfChars;
        String[] anArrayOfStrings;

* ### Syntax for assigning values to arrays

        //Alternatively, you can use the shortcut syntax to create and initialize an array:
        
        int[] anArray = {
            100, 200, 300,
            400, 500, 600,
            700, 800, 900, 1000
        };
* ### Multi-dimensional arrays
    In the Java programming language, a multidimensional array is an array whose components are themselves arrays. This is unlike arrays in C or Fortran. A consequence of this is that the rows are allowed to vary in length, as shown in the following MultiDimArrayDemo program:

        class MultiDimArrayDemo {
            public static void main(String[] args) {
    
                String[][] names = {
                    {"Mr. ", "Mrs. ", "Ms. "},
                    {"Smith", "Jones"}
                };
    
                // Mr. Smith
                System.out.println(names[0][0] + names[1][0]);
    
                // Ms. Jones
                System.out.println(names[0][2] + names[1][1]);
            }
        }

* ### Copying arrays
  The following program, ArrayCopyDemo, declares an array of char elements, spelling the word "decaffeinated." It uses the System.arraycopy method to copy a subsequence of array components into a second array:

        class ArrayCopyDemo {
            public static void main(String[] args) {
                char[] copyFrom = { 'd', 'e', 'c', 'a', 'f', 'f', 'e',
                                    'i', 'n', 'a', 't', 'e', 'd' };
                char[] copyTo = new char[7];
        
                System.arraycopy(copyFrom, 2, copyTo, 0, 7);
                System.out.println(new String(copyTo));
            }
        }

    The output from this program is:
  
        caffein

* ### Array Manipulations
    Arrays are a powerful and useful concept used in programming. Java SE provides methods to perform some of the most common manipulations related to arrays. For instance, the ArrayCopyDemo example uses the arraycopy method of the System class instead of manually iterating through the elements of the source array and placing each one into the destination array. This is performed behind the scenes, enabling the developer to use just one line of code to call the method.

    For your convenience, Java SE provides several methods for performing array manipulations (common tasks, such as copying, sorting and searching arrays) in the java.util.Arrays class. For instance, the previous example can be modified to use the copyOfRange method of the java.util.Arrays class, as you can see in the ArrayCopyOfDemo example. The difference is that using the copyOfRange method does not require you to create the destination array before calling the method, because the destination array is returned by the method:

        class ArrayCopyOfDemo {
            public static void main(String[] args) {
        
                char[] copyFrom = {'d', 'e', 'c', 'a', 'f', 'f', 'e',
                    'i', 'n', 'a', 't', 'e', 'd'};
                    
                char[] copyTo = java.util.Arrays.copyOfRange(copyFrom, 2, 9);
                
                System.out.println(new String(copyTo));
            }
        }
    As you can see, the output from this program is the same (caffein), although it requires fewer lines of code. Note that the second parameter of the copyOfRange method is the initial index of the range to be copied, inclusively, while the third parameter is the final index of the range to be copied, exclusively. In this example, the range to be copied does not include the array element at index 9 (which contains the character a).

    Some other useful operations provided by methods in the java.util.Arrays class, are:

1. Searching an array for a specific value to get the index at which it is placed (the binarySearch method).
2. Comparing two arrays to determine if they are equal or not (the equals method).
3. Filling an array to place a specific value at each index (the fill method).
4. Sorting an array into ascending order. This can be done either sequentially, using the sort method, or concurrently, using the parallelSort method introduced in Java SE 8. Parallel sorting of large arrays on multiprocessor systems is faster than sequential array sorting.


## Operators

* ### Assignment Operators
  It is represented by =, and it is normally used to assign a value to a variable.

      int speed = 0;
      float height = 1.7f;
  
* ### Arithmetic Operators
  `+`, `-`, `/`, `*`, `%` are the arithmetic operators. + can be used to concatenate strings.
  
* ### Unary Operators
  1. `+` indicates that the number is positive.
  2. `-` indicates that the number is negative.
  3. `++` increment
  4. `--` decrement
  5. `!` Logical compliment
  
* ### Equality and relational operators
  1. `==`
  2. `!=`
  3. `>`
  4. `>=`
  5. `<`
  6. `<=`

* ### Conditional Operators
  1. `&&` 
  2. `||`
  
* ###  The Type Comparison Operator instanceof
  The instanceof operator compares an object to a specified type. You can use it to test if an object is an instance of a class, an instance of a subclass, or an instance of a class that implements a particular interface.

  The following program, InstanceofDemo, defines a parent class (named Parent), a simple interface (named MyInterface), and a child class (named Child) that inherits from the parent and implements the interface.

      class InstanceofDemo {
        public static void main(String[] args) {
              Parent obj1 = new Parent();
              Parent obj2 = new Child();
      
              System.out.println("obj1 instanceof Parent: "
                  + (obj1 instanceof Parent));
              System.out.println("obj1 instanceof Child: "
                  + (obj1 instanceof Child));
              System.out.println("obj1 instanceof MyInterface: "
                  + (obj1 instanceof MyInterface));
              System.out.println("obj2 instanceof Parent: "
                  + (obj2 instanceof Parent));
              System.out.println("obj2 instanceof Child: "
                  + (obj2 instanceof Child));
              System.out.println("obj2 instanceof MyInterface: "
                  + (obj2 instanceof MyInterface));
          }
      }
  
      class Parent {}
      class Child extends Parent implements MyInterface {}
      interface MyInterface {}

  Output:

      obj1 instanceof Parent: true
      obj1 instanceof Child: false
      obj1 instanceof MyInterface: false
      obj2 instanceof Parent: true
      obj2 instanceof Child: true
      obj2 instanceof MyInterface: true
  
  When using the instanceof operator, keep in mind that null is not an instance of anything.



* ### Bitwise and bitshift operators

  1. `&` AND 
  2. `|` OR
  3. `^` XOR


</details>



