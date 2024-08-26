
# student-managementsystem

    Analysis
a. SOLID Principles:
    Single Responsibility Principle (SRP): The SMS(StudentManagementSystem) class violates this principle as it is responsible for both managing the student database and interacting with the user. These responsibilities should be separated.
    Open/Closed Principle (OCP): The code does not provide a clear way to extend the functionality without modifying the existing classes. For example, adding new actions or features would require changes to the StudentManagementSystem class.
b. DRY (Don't Repeat Yourself):
    The update_student_info method in the StudentManagementSystem class contains repetitive logic to find the correct student and update their information. This logic could be extracted to a separate method.
c. KISS (Keep It Simple Stupid):
    The StudentManagementSystem class is responsible for managing the student database and handling user interactions. This makes the class complex and difficult to maintain.
d. YAGNI (You Ain't Gonna Need It):
    The update_student method in the Student class allows updating all student attributes, even if the caller only needs to update one. This adds unnecessary complexity.
    
    Refactoring
To address the identified issues, we refactored the code below:
a. Separate Responsibilities:
    Create a StudentRepository class to handle the student database operations, separating the database management from the user interaction.
    Create a StudentManagementConsole class to handle the user interface and interaction with the StudentRepository.
b. Eliminate Redundancy:
    Extract the logic to find and update a student's information in the StudentRepository class.
c. Simplify the Design:
    Reduce the complexity of the StudentManagementSystem class by delegating responsibilities to the StudentRepository and StudentManagementConsole classes.
d. Avoid Unnecessary Features:
    Simplify the update_student method in the Student class to only update the necessary attributes.

```python
class Student:
""Represents a student with an ID,name,age and major""
    def __init__(self, id, name, age, major):
        self.id = id
        self.name = name
        self.age = age
        self.major = major

    def update_name(self, name):
        self.name = name

    def update_age(self, age):
        self.age = age

    def update_major(self, major):
""Update the major of the student ""
        self.major = major

    def display_student(self):
"""Print the student's information in a formatted string"""
        print(f"ID: {self.id}, Name: {self.name}, Age: {self.age}, Major: {self.major}")

class StudentRepository:
"""manages a collection of objects"""
    def __init__(self):
        self.students = []
""initalize a new student_repository with an empty list of students""

    def add_student(self, student):
""add a new student to the repository""
        self.students.append(student)

    def remove_student(self, student_id):
"remove a student from the repository"
        for student in self.students:
            if student.id == student_id:
                self.students.remove(student)
                break

    def update_student(self, student_id, name=None, age=None, major=None):
""update the information of a student in the repository based on their ID""
        for student in self.students:
            if student.id == student_id:
                if name:
                    student.update_name(name)
                if age:
                    student.update_age(age)
                if major:
                    student.update_major(major)
                break

    def display_all_students(self):
""print the information of all students in the repository.""
        for student in self.students:
            student.display_student()

class StudentManagementConsole:
    def __init__(self):
""initialize a new student_management_console""
        self.repository = StudentRepository()

    def run_menu(self):
""display a menu and handle user input to perform various student management operation""
        while True:
            self.display_menu()
            choice = input("Enter your choice (1-5): ")
            if choice == "1":
                self.add_student()
            elif choice == "2":
                self.delete_student()
            elif choice == "3":
                self.update_student()
            elif choice == "4":
                self.show_all_students()
            elif choice == "5":
                print("Exiting...")
                break
            else:
                print("Invalid choice. Please try again.")
"""display the main menu options"""

    def display_menu(self):
        print("\nStudent Management System")
        print("1. Add Student")
        print("2. Delete Student")
        print("3. Update Student")
        print("4. Show All Students")
        print("5. Exit")

    def add_student(self):
""" prompt the user for student information and add a new student to the reporsitory"""
        id = int(input("Enter student ID: "))
        name = input("Enter student name: ")
        age = int(input("Enter student age: "))
        major = input("Enter student major: ")
        student = Student(id, name, age, major)
        self.repository.add_student(student)
        print("Student added successfully.")

    def delete_student(self):
"""prompt the user for a student ID and remove the corresponding student from the repository""
        student_id = int(input("Enter student ID to delete: "))
        self.repository.remove_student(student_id)
        print("Student deleted successfully.")

    def update_student(self):
        student_id = int(input("Enter student ID to update: "))
        name = input("Enter new name (leave blank to skip): ")
        age = input("Enter new age (leave blank to skip): ")
        major = input("Enter new major (leave blank to skip): ")
        self.repository.update_student(student_id, name, age, major)
        print("Student updated successfully.")

    def show_all_students(self):
""display the information of all students in the repository""
        print("\nAll Students:")
        self.repository.display_all_students()

Documentation:

    Comments:
        The code includes comments explaining the purpose of each class and method.
        The run_menu method in the StudentManagementConsole class is documented, explaining the flow of the menu system.

 Conclusion
The refactored student management system code addessess the identfied issues and follows best pratices for software design and development
By separating resposiblities,eliminating redundancy,simplifying the design,and avoiding unnecessary features,the code has become more maintainabe
and extensible.
