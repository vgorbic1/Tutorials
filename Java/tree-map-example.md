## Display Tree Map

import java.util.*;

class TreeMapDemo {

    private void run() {
        /**
         *  Create an instance of the TreeMap class. This class holds 
         *  a sorted set of mapped data. The key can be any object, 
         *  including a String. The value can be any object, including a
         *  custom class that you would write.
         *  You can declare this variable as type Map or TreeMap like
         *  this:
         *
         *  Map students = new TreeMap();
         *  OR
         *  TreeMap students = new TreeMap();
         *  
         */
        Map<String, Student> students = new TreeMap<String, Student>();

        /**
         *  Now we will add a group of Student objects to the TreeMap
         */
        students.put("a1234", new Student("a1234", "Fred", "Jones", 2.5));
        students.put("b3452", new Student("b3452", "Sally", "Smith", 3.0));
        students.put("f9874", new Student("f9874", "Bill", "Crandall", 3.5));
        students.put("r2234", new Student("r2234", "June", "White", 3.8));
        students.put("c4321", new Student("c4321", "John", "Green", 4.0));
        students.put("u9877", new Student("u9877", "Jill", "Black", 3.2));
        students.put("w3458", new Student("w3458", "Jim", "Brown", 2.0));

        // Now we will output the collections

        displayStudents(students);

        /**
         *  Now we will add 0.2 to Jill's grade point. 
         *  Notice that we don't have to put the 'student' back into 
         *  the TreeMap, it is still there and we are changing it in
         *  place.
         */
        Student student = (Student) students.get("u9877");
        student.adjustGradePointAverage(0.2);

        // And then display the students again to confirm the salary 
        // increase

        displayStudents(students);
    }

    /**
     *  This method outputs the students to the standard output
     *
     *@param  students  The employee TreeMap to be displayed
     */
    private void displayStudents(Map<String, Student> students) {

        System.out.println();
        System.out.println("Student List:");

        for (Map.Entry<String, Student> entry : students.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }

        System.out.println();
    }

    /**
     * The main method for the demo.
     *
     *@param  args  Parameters that are entered on the command line.
     */
    public static void main(String[] arguments) {

        TreeMapDemo demo = new TreeMapDemo();
        demo.run();
    }
}
```

This is the Student class:
```
public class Student {

    private String studentId;
    private String firstName;
    private String lastName;
    private double gradePointAverage;

    /**
     * Constructor for Student.
     */
    public Student() {
        studentId = "Unknown ID";
        firstName = "Unknown";
        lastName = "Unknown";
        gradePointAverage = 4.0;
    }

    /**
     * Basic constructor for Student.
     *
     * @param studentId the Student ID
     * @param firstName the Student's first name
     * @param lastName the Student's last name
     * @param gradePointAverage the Student's grade point average
     */
    public Student(String studentId, String firstName, String lastName, double gradePointAverage) {
        this.studentId = studentId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.gradePointAverage = gradePointAverage;
    }

    /**
     * Adjust the grade point average of the student by the incremental 
     * amount.
     * @param incremental the amount to add to the grade point average
     */
    public void adjustGradePointAverage(double incremental) {
        gradePointAverage += incremental;
    }

    /**
     * A text representation of the Student for debugging.
     * @return the student string
     */
    public String toString() {
        String student = "Student: studentId=" + studentId
                + ", firstName=" + firstName
                + ", lastName=" + lastName
                + ", gradePointAverage=" + gradePointAverage;

        return student;
    }
}
```
