# Unit1_OOP
"""
===========================================================
Unit 1 DISCUSSION: Python OOP, Namespaces, and Copying
===========================================================

INSTRUCTIONS:
In this assignment, you will build and explore object-oriented programming (OOP) concepts in Python.
You are provided with starter code containing TODO sections. Your task is to complete, modify, and
analyze the code to demonstrate understanding of inheritance, namespaces, and object copying.
"""


from copy import copy, deepcopy


# TODO 1:
# Create a parent class.
#
# Requirements:
# - Include at least one class variable.
# - Include at least two instance variables.
# - Include a constructor (__init__).
# - Include a method that returns or displays information about the object.
#
# Replace the pass statement with your implementation.

class ParentClass:
    # Class variable
    species = "Human"

    def __init__(self, name, age):
        # Instance variables
        self.name = name
        self.age = age

    def info(self):
        return f"Name: {self.name}, Age: {self.age}, Species: {ParentClass.species}"


# TODO 2:
# Create a child class that inherits from the parent class.
#
# Requirements:
# - Use inheritance.
# - Add at least one new class variable.
# - Add at least two new instance variables.
# - Add at least one new method.
# - Override a method from the parent class.
#
# Replace the pass statement with your implementation.

class ChildClass(ParentClass):
    # New class variable
    school = "Generic Academy"

    def __init__(self, name, age, grade, hobbies):
        # Call parent constructor
        super().__init__(name, age)

        # New instance variables
        self.grade = grade
        self.hobbies = hobbies  # list (mutable)

    # New method
    def add_hobby(self, hobby):
        self.hobbies.append(hobby)

    # Override parent method
    def info(self):
        return (f"Name: {self.name}, Age: {self.age}, Grade: {self.grade}, "
                f"School: {ChildClass.school}, Hobbies: {self.hobbies}")


# TODO 3:
# Create a function that demonstrates class namespaces and instance namespaces.
#
# Your function should:
# - Create at least two objects of the child class.
# - Access a class variable through the class itself.
# - Access the same class variable through an object.
# - Add a new attribute to only one object after it is created.
# - Display each object's namespace using __dict__.
# - Display information about the class namespace.

def demonstrate_namespaces():
    print("\n=== Namespace Demonstration ===")
    # Create two child objects
    c1 = ChildClass("Alice", 12, 7, ["Drawing"])
    c2 = ChildClass("Bob", 13, 8, ["Gaming"])

    # Access class variable through class
    print("Class variable via class:", ChildClass.school)

    # Access class variable through object
    print("Class variable via object:", c1.school)

    # Add new attribute to only one object
    c1.favorite_color = "Blue"

    # Display namespaces
    print("\nObject 1 namespace:", c1.__dict__)
    print("Object 2 namespace:", c2.__dict__)

    # Display class namespace
    print("\nClass namespace:", ChildClass.__dict__)


# TODO 4:
# Create a function that demonstrates shallow copying and deep copying.
#
# Requirements:
# - Create an object that contains nested mutable data.
# - Create a shallow copy.
# - Create a deep copy.
# - Modify the original object's nested data.
# - Display the original object, shallow copy, and deep copy.
# - Use comments to explain the difference between shallow and deep copying.

def demonstrate_copying():
    print("\n=== Copy Demonstration ===")

    # Object with nested mutable data
    original = ChildClass("Charlie", 14, 9, ["Chess", ["Robotics", "Coding"]])

    # Shallow copy
    shallow = copy(original)

    # Deep copy
    deep = deepcopy(original)

    # Modify nested data in original
    original.hobbies[1].append("AI Engineering")

    print("\nOriginal object:", original.hobbies)
    print("Shallow copy:", shallow.hobbies)
    print("Deep copy:", deep.hobbies)

    print("\nExplanation:")
    print("- Shallow copy shares nested mutable objects with the original.")
    print("- Deep copy creates completely independent nested objects.")


# TODO 5:
# Complete the main function.
#
# Requirements:
# - Create at least one object from the parent class.
# - Create at least one object from the child class.
# - Demonstrate inheritance by calling methods.
# - Call your namespace demonstration function.
# - Call your copy demonstration function.

def main():
    print("=== Unit 1 OOP Assignment ===")

    # Parent object
    parent = ParentClass("Dana", 40)
    print("\nParent object info:")
    print(parent.info())

    # Child object
    child = ChildClass("Eli", 15, 10, ["Basketball"])
    print("\nChild object info:")
    print(child.info())

    # Demonstrate inheritance
    child.add_hobby("Music")
    print("Updated child info:", child.info())

    # Namespace demonstration
    demonstrate_namespaces()

    # Copy demonstration
    demonstrate_copying()

if __name__ == "__main__":
    main()
