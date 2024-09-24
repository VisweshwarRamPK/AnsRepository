
**4) ANY USE CASE WITH ANY DATA STRUCTURE IN JAVA**

**I) FIND II) SORT**

**STUDENT CLASS:**

private String name;

private int id;

public String getName() { return name; }

public void setName(String name) { this.name = name; }

public int getId() { return id; }

public void setId(int id) { this.id = id; }

**DETAILS CLASS:**

public class Details extends Student{

    public static void main(String[] args) {

        List&lt;Student> l=new ArrayList&lt;>();

        Student s1=new Student();

        s1.name=”name";

        s1.id=15;

        l.add(s1);

        Student s2=new Student();

        s2.name="viswa";

        s2.id=60;

        l.add(s2);

**I) FIND:**

**IA) Find Using a For Loop:**

This is a simple approach using an enhanced `for` loop to find a student by their `id`.

for(Student s : l) {

    if(s.id == 46) {

        System.out.println("Found");

        return;

    }

}

System.out.println("Not found");

**IB) Find Using Streams:**

Optional&lt;Student> b = l.stream().filter(a -> a.id == 61).findAny();

if(b.isPresent()) {

    System.out.println("61 found");

} else {

    System.out.println("Not found");

}

**II) SORT:**

Sorting is done using the `Comparator` interface to sort by either the `id` or `name` field.



* **Sort by <code>id</code>: \
</strong>Sorting the list of students by their <code>id</code> using <code>Comparator.comparingInt()</code>.

l.sort(Comparator.comparingInt(Student::getId));

for(Student s : l) {

    System.out.println(s.name + " " + s.id);

}

**Sort by <code>name</code>:</strong>

Sorting the list of students by their `name` using `Comparator.comparing()`.

l.sort(Comparator.comparing(Student::getName));

for(Student s : l) {

    System.out.println(s.name + " " + s.id);

}
