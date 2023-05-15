# OOP-Week-9
1.(a) By making use of an example from the above scenario, distinguish between a class and an instantiation of a class. (3 points)
A class is essentially a template that defines the properties and methods of an object. It represents a category of objects that share common characteristics. An instantiation of a class, on the other hand, is a concrete object that is created based on the blueprint provided by the class.

(b) By giving two examples, explain how the principles of inheritance can be incorporated into the design of this administration program. (4 points)
In object-oriented programming, inheritance is a principle that enables a class to acquire properties and methods from another class. In the context of the administration program, there are two ways to incorporate inheritance:
1. A base class can be created that contains general properties and methods of a GUI. The specific GUIs for each module can inherit from this base class and add their own unique properties and methods. For instance, a base class named "ModuleGUI" can be created, and each module-specific GUI can inherit from it.
2. Another way to use inheritance is by creating a hierarchy of classes that represent different levels of functionality. For example, a base class named "GUI" can be created, and subclasses such as "BasicGUI", "AdvancedGUI", and "PremiumGUI" can be created to represent different levels of functionality.

(c) Describe how the use of libraries can facilitate the development of programs like this company’s administration program. (3 points)
Libraries are a useful tool in programming that can provide pre-existing code for common tasks like managing databases, handling files, and authenticating users. This can save developers time and effort as they don't have to create these functionalities from scratch, allowing them to focus on the main purpose of the program.

2. The company employs several sales personnel to sell its products to different retailers. Each branch of the company keeps track of its own sales with a suite of programs that include the two classes SalesPerson and Sales.

 

public class SalesPerson {

// each object contains details of one salesperson

private String id;

private Sales[] salesHistory; // details of the different sales

private int count = 0; // number of sales made



//constructor for a new salesperson

public SalesPerson(String id){

// code missing

}

 

// constructor for a salesperson transferred (together with their sales details) from another branch

public SalesPerson(String id, Sales[] s, int c){

// code missing

}

 

public int getCount(){return count;}

public String getId() {return id;}

public void setSalesHistory(Sales s){

salesHistory[count] = s;

count = count +1;

}

 

public double calcTotalSales(){

// calculates total sales for the salesperson

// code missing

}

 

public Sales largestSale(){

// calculates the sale with the largest value

// code missing

}

}

 

Each instance variable is initialized when a SalesPerson object is instantiated.

(a) Complete the constructor public SalesPerson(String id), from the SalesPerson class. (2 points)
```
public SalesPerson(String id){
this.id = id;
this.salesHistory = new Sales[100]; // Initialize the sales history array with a fixed length of 100
this.count = 0; // Set the initial count to 0
}
```

(b) Explain why accessor methods are necessary for the SalesPerson class. (3 points)
Accessor methods, such as getters and setters, are necessary for the SalesPerson class to provide controlled access to its private instance variables. Since the id, salesHistory, and count instance variables are declared as private, they cannot be accessed directly from other classes. Accessor methods provide a way to retrieve or modify the values of these instance variables while maintaining encapsulation, which is an important principle of object-oriented programming.

public class Sales {

// each object contains details of one sale

private String itemId;     // id of the item

private double value;      // the price of one item

private int quantity;      // the number of the items sold

// constructor missing

public double getValue() {return value;}

public int getQuantity() {return quantity;}

}

 

(c) (i) Construct unified modelling language (UML) diagrams to clearly show the relationship between the SalesPerson and Sales classes.

Note: There is no need to include mutator or accessor methods or a constructor. (4 points)

(c) (ii) Outline a negative effect that a future change in the design of the Sales object might have on this suite of programs. (2 points)
If there are any future changes to the Sales object's design such as adding or removing instance variables or methods, it could negatively affect the suite of programs as a whole. This is because the SalesPerson class or other classes that depend on the Sales class may need to be modified to accommodate the changes. For example, if a new instance variable is added to the Sales class, the SalesPerson class may need to be modified to adjust to this change. If the changes are not implemented correctly, it could lead to errors or unexpected behavior in the program. Furthermore, any other classes that rely on the Sales class may also require modification to adapt to the changes, which could be a time-consuming and error-prone process.

The company employs several sales personnel. The different salesPerson objects are held in the array salesPeople. The Driver class contains various methods that operate on the SalesPerson and Sales classes. The Driver class contains the following code:

public static void main(String[] args){

SalesPerson[] salesPeople = new SalesPerson[6];

salesPeople[0] = new SalesPerson("100");

salesPeople[1] = new SalesPerson("101");

salesPeople[2] = new SalesPerson("102");

salesPeople[0].setSalesHistory(new Sales("A100",300.00,10));

salesPeople[0].setSalesHistory(new Sales("A200",1000.00,2));

salesPeople[1].setSalesHistory(new Sales("A300",2550.40,10));

System.out.println(salesPeople[2].getId());

System.out.println(salesPeople[0].getCount());

System.out.println(salesPeople[1].getSalesHistory(0).getValue());

System.out.println(salesPeople[0].calcTotalSales());

 }

(d) State the output after running this code. (4 points)
102
2
2550.4
4600.0

(e) Construct the method calcTotalSales(), in the SalesPerson class that calculates the total value of the sales for a specific SalesPerson object. (5 points)
```
public double calcTotalSales() {
double totalSales = 0;
for (int i = 0; i < count; i++) {
totalSales += salesHistory[i].getValue() * salesHistory[i].getQuantity();
}
return totalSales;
}
``` 

(f) By making use of any previously written methods, construct the method highest(), that returns the ID of the salesperson whose sales have the largest total value. (5 points)
```
public static String highest(SalesPerson[] salesPeople) {
double maxSales = 0;
String id = "";
for (int i = 0; i < salesPeople.length; i++) {
double totalSales = salesPeople[i].calcTotalSales();
if (totalSales > maxSales) {
maxSales = totalSales;
id = salesPeople[i].getId();
}
}
return id;
}
```

(g) Construct the method addSales(Sales s, String id), in the Driver class, that will add a new Sales object s, to the salesperson with a specified ID.

Note: You can assume that the ID is a valid one. (4 points)
```
public static void addSales(Sales s, String id, SalesPerson[] salesPeople) {
for (int i = 0; i < salesPeople.length; i++) {
if (salesPeople[i].getId().equals(id)) {
salesPeople[i].setSalesHistory(s);
break;
}
}
}
```

A further class in this suite of programs is the Payroll class. This class is run at the end of each month to calculate each salesperson’s salary, which is based on the sales that have been made during that month.

(h) Suggest changes that must be made to the SalesPerson class and/or the Sales class to allow these calculations to be made. (3 points)
To allow the calculation of salesperson salaries, the Sales class may need to be updated to include a date field that indicates when the sale was made. The SalesPerson class may also need to be updated to include a method that calculates the sales made within a given time period.

(i) Discuss the use of polymorphism that occurs in this suite of programs. (3 points)
Polymorphism is used in this suite of programs when methods such as calcTotalSales() and largestSale() in the SalesPerson class are called on Sales objects. The Sales class is a subclass of the Object class, and since all classes in Java inherit from the Object class, these methods can be called on Sales objects. This allows for greater flexibility in the design of the program and makes it easier to add new functionality in the future.
