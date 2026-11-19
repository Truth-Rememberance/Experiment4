# Experiment4
Experiment4: cloning

Remote changes for Experiment 5


7. A company maintains details of its employees for administrative and payroll 
purposes. Each employee record contains the following fields: SSN, Name, Department, 
Designation, Salary, and Phone Number. Since employees may frequently join, leave, or 
change positions, a Doubly Linked List (DLL) provides a flexible way to manage these 
records efficiently in both directions. 
To simulate this process, design and implement a menu-driven C program that 
performs the following operations on the employee database: 
5. Create a Doubly Linked List of N employee records using end insertion. 
6. Display all employee records and count the total number of nodes. 
7. Insert or delete an employee record at the end of the list. 
8. Insert or delete an employee record at the front of the list. 
Demonstrate how the DLL can be used as a Double Ended Queue (Deque). 
#include <stdio.h> 
#include <stdlib.h> 
// Structure for employee 
struct Employee { 
 char ssn[20];
 char name[50];
 char dept[30];
 char designation[30];
 float salary;
 char phone[15];
 struct Employee* prev;
 struct Employee* next;
};
// Create a new employee node 
struct Employee* createEmployee() 
{ 
 struct Employee* newEmployee;
 newEmployee = (struct Employee*)malloc(sizeof(struct Employee));
 if (newEmployee == NULL) { 
 printf("Memory allocation failed!\n");
 exit(1);
 } printf("Enter SSN: ");
 scanf("%25s", newEmployee->ssn);
 printf("Enter Name: ");
 scanf(" %25[^\n]", newEmployee->name);
 printf("Enter Department: ");
 scanf(" %25[^\n]", newEmployee->dept);
 printf("Enter Designation: ");
 scanf(" %25[^\n]", newEmployee->designation);
 printf("Enter Salary: ");
 scanf("%f", &newEmployee->salary);
 printf("Enter Phone Number: ");
 scanf("%14s", newEmployee->phone);
 newEmployee->prev = NULL;
 newEmployee->next = NULL;
 return newEmployee;
} 
// Insert employee at front 
struct Employee* insertFront(struct Employee* head) 
{ 
 struct Employee* newEmployee = createEmployee();
 if (head == NULL) { 
 head = newEmployee;
 } 
 else { 
 newEmployee->next = head;
 head->prev = newEmployee;
 head = newEmployee;
 } 
 printf("Employee inserted at front successfully.\n");
 return head;
} // Insert employee at end 
struct Employee* insertEnd(struct Employee* head) 
{ 
 struct Employee* newEmployee = createEmployee();
 if (head == NULL) { 
 head = newEmployee;
 } 
 else { 
 struct Employee* temp = head;
 while (temp->next != NULL) { 
 temp = temp->next;
 } 
 temp->next = newEmployee;
 newEmployee->prev = temp;
 } 
 printf("Employee inserted at end successfully.\n");
 return head;
} 
// Delete employee from front 
struct Employee* deleteFront(struct Employee* head) 
{ 
 if (head == NULL) { 
 printf("List is empty. Nothing to delete.\n");
 } 
 else { 
 struct Employee* temp = head;
 printf("Deleted employee: %s\n", temp->name);
 head = head->next;
 if (head != NULL) { 
 head->prev = NULL;
 } 
 free(temp); } 
 return head;
} 
// Delete employee from end 
struct Employee* deleteEnd(struct Employee* head) 
{ 
 if (head == NULL) { 
 printf("List is empty. Nothing to delete.\n");
 } 
 else if (head->next == NULL) { 
 printf("Deleted employee: %s\n", head->name);
 free(head);
 head = NULL;
 } 
 else { 
 struct Employee* temp = head;
 while (temp->next != NULL) { 
 temp = temp->next;
 } 
 printf("Deleted employee: %s\n", temp->name);
 temp->prev->next = NULL;
 free(temp);
 } 
 return head;
} 
// Display all employees and count nodes 
void display(struct Employee* head) 
{ 
 struct Employee* temp = head;
 int count = 0;
 if (head == NULL) { 
 printf("Employee database is empty.\n");
 printf("Total number of employees: 0\n"); return;
 } 
 printf("\n------ Employee Records ------\n");
 while (temp != NULL) { 
 printf("\nSSN: %s", temp->ssn);
 printf("\nName: %s", temp->name);
 printf("\nDepartment: %s", temp->dept);
 printf("\nDesignation: %s", temp->designation);
 printf("\nSalary: %.2f", temp->salary);
 printf("\nPhone Number: %s\n", temp->phone);
 count++;
 temp = temp->next;
 } 
 printf("\n------------------------------\n");
 printf("Total number of employees: %d\n", count);
} 
// Main function 
int main() 
{ 
 struct Employee* head = NULL;
 int choice, n, i;
 do { 
 printf("\n===== EMPLOYEE DATABASE USING DLL =====\n");
 printf("1. Create DLL of N Employees\n");
 printf("2. Display Employees and Count Nodes\n");
 printf("3. Insert Employee at End\n");
 printf("4. Delete Employee from End\n");
 printf("5. Insert Employee at Front\n");
 printf("6. Delete Employee from Front\n");
 printf("7. Exit\n");
 printf("Enter your choice: ");
 scanf("%d", &choice);
 switch (choice) { case 1: 
 printf("Enter number of employees: ");
 scanf("%d", &n);
 if (n <= 0) { 
 printf("Enter a valid number of employees.\n");
 break;
 } 
 for (i = 0; i < n; i++) {
 printf("\nEnter details of employee %d:\n", i + 1);
 head = insertEnd(head);
 } 
 break;
 case 2: 
 display(head);
 break;
 case 3: 
 head = insertEnd(head);
 break;
 case 4: 
 head = deleteEnd(head);
 break;
 case 5: 
 head = insertFront(head);
 break;
 case 6: 
 head = deleteFront(head);
 break;
 case 7: 
 printf("Exiting Employee Database...\n");
 break;
 default: 
 printf("Invalid choice. Try again.\n");
 } } while (choice != 7);
 // Free all remaining nodes
 while (head != NULL) {
 struct Employee* temp = head;
 head = head->next;
 free(temp);
 }
 return 0;
}
 Sample Output
