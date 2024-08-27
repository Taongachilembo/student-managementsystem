
# student-managementsystem
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

Running the code:

    Make sure you have Python installed on your system. This code was written and tested using Python 3.9, but it should work with other versions of Python 3 as well.
    Open a text editor or an IDE (Integrated Development Environment) of your choice.
    Create a new Python file (e.g., student_management.py) and copy the code provided above into the file.
    Save the file.ave the file.
    Open a terminal or command prompt and navigate to the directory containing the student_management.py file.
