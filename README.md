**Purpose**  
The purpose of this document is to guide the development of the Couples Dinner Group Shuffler (CDGS) application for my senior thesis project.

**Scope**  
The scope of this document is to describe the CDGS in terms of its functional and non-functional requirements. It will give the development team a detailed overview of the needs and goals of the CDGS.

**System Overview**  
The Couples Dinner Group organizers meet quarterly with the purpose of allowing members to get to know each other in a small group setting over a meal. The meals take place in members' homes on a rotational basis. The organizers currently divide members into groups of 4 couples manually using index cards to keep track of historical information. This program will allow the organizers to efficiently set up these groups in a fraction of the time. The program will:

* Randomly put couples in groups of 4, while changing the couples that are put together each quarter.  
* Each group will contain 4 couples. If the number of couples is not divisible by 4, the program will allocate a fifth couple to certain groups.  
* Assign a host couple for each group, where the meal will take place. No couple will host more than once a year.  
* Each couple in each group, other than the host, will be assigned to bring either a salad, vegetable, or dessert. In the event that there are 5 couples, an appetizer will also be assigned. The host will be assigned the main course.  
* The program will retain the data from quarter to quarter so that it can accomplish the task of randomizing couples without repeating who is together.  
* The program will also allow the administrator to add new couples as they join the group, and delete couples as they leave the group.  
* The program will also allow the administrator to select which couples are participating each quarter.  
* Once the groups are shuffled, the administrator is allowed to edit the groups however they please before committing.

**References**  
N/A

**Definitions**  
Couple \- two people's names and their email addresses  
Group \- 4 couples, with a fifth couple added as needed

**Use Cases**

| Name | UC-1: Adding Couples |
| :---- | :---- |
| Summary | The ability to add couples to the program |
| Rationale | In order for groups to be formed, there must be couples to put into the groups. |
| Users | All users |
| Preconditions | A starting screen with any number of couples, an "Add" button, and a "Submit" button |
| Basic Course of Events | 1\. The user clicks the "Add" button to add a new couple. 2\. The user is brought to a screen where they are prompted to input information about the couple (i.e. names, email, etc.) 3\. The user types in the information into the specified text boxes. 4\. The user navigates to the "Add" button on the bottom of the screen, and clicks the button to add the new couple. |
| Alternative Paths |  |
| Postconditions | The same screen as mentioned in the Preconditions, but now there is a new couple added. |

| Name | UC-2: Selecting Participating Couples |
| :---- | :---- |
| Summary | The ability to remove couples from the current shuffle |
| Rationale | If a couple is unable to attend a group dinner, then the couple can be omitted from the shuffle. |
| Users | All users |
| Preconditions | Same as UC-1 |
| Basic Course of Events | 1\. The user finds the couple that they want to remove from the current shuffle. 2\. The user clicks on the checkbox, located to the left of the couple. |
| Alternative Paths |  |
| Postconditions | The checkbox is unchecked, and the couple is omitted from the current shuffle. |

| Name | UC-3: Deleting Couples |
| :---- | :---- |
| Summary | The ability to delete couples from the program |
| Rationale | If a couple leaves the dinner group program, the church, or is dead, the user can delete the couple and their group history. |
| Users | All users |
| Preconditions | Same as UC-1 |
| Basic Course of Events | 1\. The user finds the couple they want to delete. 2\. The user clicks on the trashcan icon, located to the right of the couple. 3\. A text box prompt saying "Are you sure?" pops up with the options of "Yes" and "No" 4\. The user clicks "Yes" and the couple is deleted from the program. |
| Alternative Paths | 4a. The user clicks "No" which cancels the deletion. |
| Postconditions | Same as the preconditions, but now a couple has been deleted from the program. |

| Name | UC-4: Shuffling Groups |
| :---- | :---- |
| Summary | The program shuffles couples into groups |
| Rationale | This is the main function of the program |
| Users | All users |
| Preconditions | Same preconditions as UC-1 |
| Basic Course of Events | 1\. The user checks to make sure all of the couples listed are correct before clicking the button labeled "Shuffle" 2\. After clicking "Shuffle", the program puts the couples into groups of 4\. 3\. The user clicks "Done" and the program saves the current groups in a database to be referenced later (details in UC-3) |
| Alternative Paths | 2a. After the program shuffles the couples, the user has the option to edit groups manually by clicking and dragging couples in and out of groups. |
| Postconditions | The groups are shuffled, saved in a database, and the groups are put into a PDF to be emailed to attending couples. |

| Name | UC-5: Editing Groups |
| :---- | :---- |
| Summary | The user can drag and drop couples from one group to another before committing. |
| Rationale | Give the user the ability to edit groups under special circumstances. |
| Users | All users |
| Preconditions | Postcondition from UC-4: Shuffling Groups |
| Basic Course of Events | 1\. The user identifies a change they want to make to the groups. 2\. The user clicks and drags a couple out of one group. 3\. The user drops the couple into the desired group. |
| Alternative Paths | 3a. If the desired group already has 5 members, the 5th member will change places with the other couple. |
| Postconditions | New group format has been made to the user's satisfaction. |

**Functional Requirements**

| Name | FR-1: Storing/Using Group Histories |
| :---- | :---- |
| Summary | The program saves group history in an SQL/SQLite database. The information in this database is used in the next shuffle |
| Rationale | Groups should be randomized so that one couple is not with 3 other couples too often |
| Requirements | When the user commits to a group set-up, the software must store the data in a database. The database will be in SQL/SQLite and will have two tables, couples, and group histories. Each couple will have their names and email addresses, along with an ID to identify them by. The group history will have the history of each group, with couples shown by their ID, and the date/quarter the group was made.  |
| References | UC-4: Shuffling Groups |

| Name | FR-2: Groups of Four/Five |
| :---- | :---- |
| Summary | The program will shuffle the couples into groups of 4 or 5\. |
| Rationale | This is what the program is meant to do. |
| Requirements | When the user shuffles the groups, the program will check the SQL/SQLite database, referenced in FR-1, and create the groups based on the data from the database.  |
| References | UC-4: Shuffling Groups |

| Name | FR-3: Assigning Host |
| :---- | :---- |
| Summary | The program will assign a different host each quarter. |
| Rationale | There needs to be a couple who host the dinner at their residence. |
| Requirements | When the user shuffles the groups, the software will choose a host based on who has already been host in the past 4 quarters. If everyone has already been a host in that time period, the program will start again and choose a host from the 4 couples. |
| References | UC-4: Shuffling Groups |

| Name | FR-4: Assigning Roles |
| :---- | :---- |
| Summary | Anyone who is not assigned the role of host is assigned one of 3 or 4 different roles: salad, vegetable, dessert, or appetizer if it's a group of 5\. |
| Rationale | The host is in charge of the main course, but everyone else must bring something to go along with the main course. The different roles allow a variety to be brought, instead of everyone bringing the same thing. |
| Requirements | When the user shuffles the couples, the program will look at the database to see who has been in what role over the past 4 quarters. Using that information, it will assign a role to each couple before shuffling the couples into groups. |
| References | UC-4: Shuffling Groups |

**Non-Functional Requirements**

| Name | NF-1: Accuracy of Shuffle |
| :---- | :---- |
| Summary | Once the user shuffles the couples, the program should be as accurate to the user's needs as possible, avoiding repetitive placement of couples and roles. |
| Rationale | If the program is too repetitive with couple placement and roles, the user will abandon the program due to lack of accuracy. |
| Requirements | The developer should force groups to be formed with couples who have never been together or have not been together for at least 1 year. |
| References | UC-4: Shuffling Groups |

| Name | NF-2: Speed of the Program |
| :---- | :---- |
| Summary | Once the program is initiated, the task will need to be done as efficiently as possible. |
| Rationale | The user will give up on the program if the task takes too long. |
| Requirements | In order to not slog down the program, it will only use the last 3 year's worth of data when making the groups. |
| References | UC-4: Shuffling Groups |

| Name | NF-3: Case Sensitivity |
| :---- | :---- |
| Summary | The program should not take case sensitivity into account, considering that the program is meant to shuffle groups. |
| Rationale | We want to make it as flexible as possible for the user to enter any information they need. |
| Requirements | The developer should keep in mind not to implement case sensitivity into the program. |
| References | UC-1: Adding Couples |

| Name | NF-4: Couple Management |
| :---- | :---- |
| Summary | The user is able to add and delete couples as they please, so the program needs to accommodate for this. |
| Rationale | If a couple joins or leaves the group, the program needs to adapt to this change. |
| Requirements | If a couple is added or deleted, the program will add or delete their names and email addresses from the database. |
| References | UC-1: Adding Couples, UC-3: Deleting Couples |
