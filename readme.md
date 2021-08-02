# SimpleERP Application

This repository represents the final project for the course CST 338: Software Design. The project summary and spec sheet are present within the documentation below.

---

## Table of Contents

1. [Overview](#overview)
1. [UML](#uml)
1. [Menus](#menus)
1. [Output](#output)
1. [Implementation](#implementation)
1. [Testing](#testing)
---

## Overview

---

SimpleERP is a console application built using the Model View Controller design pattern. It contains
three modules that allow a single user to manage their staff roster, update and remove an employee’s
sales information and to view a comprehensive sales report. The application is composed of 7 classes:
Main, Model, View, Controller, Employee, SalesRecord and Sales.

[Return to Top](#table-of-contents)

---

## UML

---

![uml](/documentation/Shum_Assig8_FinalProject_UML.jpg)

[Return to Top](#table-of-contents)

---


## Menus

---

### _Main Menu_

![picture](/documentation/img/p1.png)

The Main Menu is the first menu that the user will see. It allows the user to reach each of the three
modules.

### _Manage Employees Menu_
![picture](/documentation/img/p2.png)

The Manage Employee Menu allows the user to add and remove employees from their staff list as well
as sort the list for readability. Adding and removing the employees will also add and remove their
associated sales from the Model.

### _Manage Employee Sales Menu_

![picture](/documentation/img/p3.png)

The Manage Employee Sales Menu allows a user to select an employee and view their sales history.

### _Employee Sales History Menu_

![picture](/documentation/img/p4.png)

A submenu for Manage Employee Sales, the Employee Sales History Menu allows a user to add and
remove sales entries from an employee’s sales history. It also allows them to sort the entries for
readability.

### _Master Sales Record Menu_

![picture](/documentation/img/p5.png)

The Master Sales record Menu allows a user to view a comprehensive report on the sales totals for the organization. Sales entries are displayed with Sale ID as their identifier, rather than employee ID.

[Return to Top](#table-of-contents)

---

## Output

---

The application will perform validation and confirm and selection choices for all user input. Non-
exhaustive examples below.

### _Invalid Menu Selection_

![picture](/documentation/img/p6.png)

### _Invalid Option Selection_

![picture](/documentation/img/p7.png)

### _Adding/Removing Employees_

![picture](/documentation/img/p8.png)

### _Adding/Removing Sales_

![picture](/documentation/img/p9.png)

### _Quitting the Application_

![picture](/documentation/img/p10.png)

[Return to Top](#table-of-contents)

---

## Implementation

---

### _Overview_

The application is built using the Model View Controller design pattern. The main will call the Model,
View and Controller objects. Controller will interact directly with Model and View. View and Model are
separated by Controller. Model will interact with the Sale, SalesRecord and Employee classes.
Specifically, Model holds a SalesRecord object and an Employee[] object and Employee holds a Sale[]
object.

All classes that are part of the model: Model, Sale, SalesRecord and Employee should have accessors,
mutators, copy constructors and toString methods as well.

For all entries, please reference the UML for a list of methods/variables and the Javadoc for
documentation.

---

### _Main_

The Main exists simply to call the Model, View and Controller constructors.

---

### _Controller_

The Controller takes user input and uses its logic to update Model through its accessors and mutators. It
calls methods from View to provide a representation of the current state of Model.

---

### _View_

The View is composed of methods to display the menu, options and errors to the user. It takes
formatted Strings, passed by Controller and incorporates them as the body for these menus. It does not
hold any instance variables and does not interact with Model. It is reliant on Controller to pass
processed String objects to display the state of Model.

---

### _Model_

The Model holds the data of the application, as well as accessors and mutators used by Controller for
manipulation. Model holds the representation of the organization: its staff list and Master Sales Record.
In order to maintain its staff and sales arrays, Model will interact with 3 objects: Employee, SalesRecord
and Sales.

#### **_Sale_**

The Sale class represents an individual employee’s total revenue generated in a single day. It holds a
LocalDate variable of the date that the sale was made. It also holds salesAmount, an integer value
(whole numbers only) that represents the total value of the revenue generated on that day. It also holds
the Sale ID of the object, which is a unique identifier used to identify individual sales.

Sale also holds a static method for sorting incoming Sale[].

#### **_SalesRecord_**

The SalesRecord class holds an array of Sale objects as well as the current number of Sale objects held in
the array. The class is responsible for maintaining an accurate representation of the array with its
methods. It must be self-contained, meaning that external validation and filtering of parameters can be
performed but is unnecessary.

#### **_Employee_**

The Employee class represents and employee of the organization that is using SimpleERP. The class
holds a SalesRecord object, which represents the employee’s complete sales history. It also holds
identifying information, such as the employee’s name and ID.

Employee also holds a static method for sorting incoming Employee[].

---

### _UML_

Has been attached for convenience and will also be present in the project upload. 

### _Javadoc_

The Javadoc will be present in the upload for reference. It can also be generated by running the
command on the source code, also included in the project upload.

[Return to Top](#table-of-contents)

---

## Testing

---

### _Overview_

Methods for all classes should be unit tested. Methods should be decomposed to help do so. There
should be an attempt to adhere to this rule of thumb: a method should do one thing well.

For all classes with arrays, accessors and mutators should ensure that there are no privacy leaks.
Methods involving arrays should never throw NullPointerException or ArrayIndexOutOfBounds
exceptions. Testing should be done to ensure this is the case.

For classes that take user input, input must be validated and filtered before passing as a parameter to
any classes in the model. This should be done even if the model classes are designed to filter for bad
values. As such, input validation should be tested for all methods that make use of it.

For any classes with mutators and accessors, testing should be done to ensure that the proper values
are being set or returned.

For the View class, testing should be done to ensure that formatting is correct on displayed messages.

For the Controller class, testing should be done to ensure that the application logic is function correctly.
For example, option selections should take the user to the correct menu. Properly formatted input
should pass validation and improperly formatted input should be rejected. There should be no infinite
loops that the user is unable to exit.

[Return to Top](#table-of-contents)

---

## Known Issues

---

### _Design_

These are issues with the application design that are currently unresolved but would be addressed if this
project had another phase for implementation.

1. Application only allows for one concurrent user. To allow for more than one user, array
   operations need to be placed in a thread that performs synchronized calls.
2. SaleID is not truly unique. It is currently the concatenation of EmployeeID and the index of the
   element on the saleHistory array. This is fine for day to day operations, but in a real organization
   with need to reference sales over the course of months and years, a truly unique identifier
   should be generated.
3. EmployeeID functions like an IP address block. EmployeeIDs are granted from a block of integer
   values, recovered when an employee is removed and redistributed when a new employee is
   onboarded. In a real organization, old IDs may be maintained for a certain period for the
   purpose of record keeping.

### _Bugs_

These are bugs that are currently unaddressed but would be addressed if this project had another phase
for implementation.

1. User input returns multiple words for a single line – Unaddressed because input validation
   occurs for each returned word and user is prompted to confirm if choices are correct.
2. It is possible to select the option to add/remove employees/sales from an empty/full array –
   unaddressed because the classes prevent the user from actually adding/removing these objects
   to a full/empty array. However, the user should not have the option to initiate these method
   calls.

[Return to Top](#table-of-contents)