## Online Course Management System

## Objective

Simulate a system design interview by applying core Object-Oriented Programming (OOP) concepts to design and implement an object-oriented model for a real-world use case.

## Scenario

You are asked to design an Online Course Management System using OOP principles. The system supports:
 User Roles: Student, Instructor
 Functionalities:
 Course Creation  Enrollment
 Assignment Upload and Grading  Role-based Access Control

Task 1: UML Class Diagram



## Relationships:
  Inheritance: Student and Instructor inherit from User
 Association:
	Course is associated with Instructor and multiple Students 	Assignment is associated with Course
	Grade is associated with Student and Assignment

Task 2: Code (JavaScript Implementation)

```
// Base User class
class User {
  constructor(userID, name, email) {
    this.userID = userID;
    this.name = name;
    this.email = email;
  }

  login() {
    console.log(`${this.name} logged in.`);
  }

  logout() {
    console.log(`${this.name} logged out.`);
  }
}

// Student class extends User
class Student extends User {
  constructor(userID, name, email, studentID) {
    super(userID, name, email);
    this.studentID = studentID;
    this.enrolledCourses = [];
    this.grades = [];
  }

  enroll(course) {
    course.enrollStudent(this);
    this.enrolledCourses.push(course);
  }

  uploadAssignment(assignment, file) {
    assignment.addSubmission(this, file);
  }

  viewGrades() {
    console.log(` ${this.name}'s Grades:`);
    this.grades.forEach(grade => {
      console.log(`• ${grade.assignment.title}: ${grade.score}`);
    });
  }
}

// Instructor class extends User
class Instructor extends User {
  constructor(userID, name, email, instructorID) {
    super(userID, name, email);
    this.instructorID = instructorID;
    this.courses = [];
  }

  createCourse(courseID, title, description) {
    const course = new Course(courseID, title, description, this);
    this.courses.push(course);
    return course;
  }

  gradeAssignment(assignment, student, score) {
    const grade = new Grade(student, assignment, score);
    student.grades.push(grade);
  }
}

// Course class
class Course {
  constructor(courseID, title, description, instructor) {
    this.courseID = courseID;
    this.title = title;
    this.description = description;
    this.instructor = instructor;
    this.students = [];
    this.assignments = [];
  }

  enrollStudent(student) {
    if (!this.students.includes(student)) {
      this.students.push(student);
    }
  }

  addAssignment(assignment) {
    this.assignments.push(assignment);
  }
}

// Assignment class
class Assignment {
  constructor(assignmentID, title, dueDate) {
    this.assignmentID = assignmentID;
    this.title = title;
    this.dueDate = dueDate;
    this.submissions = [];
  }

  addSubmission(student, file) {
    this.submissions.push({ student, file });
  }
}

// Grade class
class Grade {
  constructor(student, assignment, score) {
    this.student = student;
    this.assignment = assignment;
    this.score = score;
  }
}
```

## Task 3: Explanation of OOP Design
1. Abstraction We model real-world entities like Student, Instructor, and Course using classes with relevant behaviors.
2. Encapsulation Data members like grades, enrolledCourses, and submissions are manipulated through methods like uploadAssignment() and viewGrades() rather than direct access.
3. Inheritance Student and Instructor both extend the User class to reuse login/logout functionalities and core attributes.
4. Polymorphism The login() method is inherited and can be overridden if needed to behave differently based on role.

## SOLID Principles Used
Single Responsibility: Each class has a single, focused purpose.
Open/Closed: Easily extendable (e.g., adding new user roles) without modifying existing code.
Liskov Substitution: Objects of Student and Instructor can replace User without breaking functionality.
Interface Segregation and Dependency Inversion are less relevant in this simple implementation but could be applied in a scaled-up version.

## Sample Test

javascript code

const instructor1 = new Instructor(1, "Dr. Rao", "rao@example.com", "I100"); const course1 = instructor1.createCourse("C101", "OOP with JavaScript", "An intro to OOP");

const student1 = new Student(2, "Alice", "alice@example.com", "S101");

student1.enroll(course1);

const assignment1 = new Assignment("A1", "OOP Basics", "2025-08-01"); course1.addAssignment(assignment1);

student1.uploadAssignment(assignment1, "alice_oop_assignment.docx"); instructor1.gradeAssignment(assignment1, student1, 95); student1.viewGrades();

## Conclusion

This project simulates a real-world Online Course Management System using OOP principles. The implementation showcases core concepts such as inheritance, encapsulation, abstraction, and
polymorphism, aligning with SOLID principles for clean and scalable design.
