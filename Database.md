[Home](README.md) - [Code Review](CodeReview.md) - [Software Engineering and Design](SoftwareEngineering_Design.md) - [Data Structures and Algorithms](DataStructures_Algorithms.md) - [Databases](Database.md)

# Inventory App (Back-end)

### Narrative
Th same as [artifact 1](SoftwareEngineering_Design.md), it's an inventory application created in CS-360 Mobile development. I created it 2 terms ago. It is an application to keep track of inventory. It contains a login screen, and the ability to add and delete items from your inventory list. You can adjust counts for each item and get notified when the count is low.

The existing issues with this application that apply directly to the database were serious. Any user could log into the application because the validation was broken. Also, there was no logic to differenciate between users so all users were essentially using the same data. This involved added an authentication class, as well as updating APIs to check for indicators in the database before performing functions. 

[This link](InventoryApp_Original.zip) goes to the original inventory project, before the enhancements were made. 

### Enhancements
The enhancements made really brought this application together. It fixed a lot of issues with saving and displaying data correctly. I also moved files around for better organization. I added indicators to the database tables. Then I updated the API calls to the database and fixed the issues with logging in. Lastly, I added checks and some input validation for improved security. This is the inventory database after adding the indicator(username) to the table.


```
      private static final class InventoryTable {
        private static final String TABLE = "inventory";
        private static final String COL_USERNAME = "username";
        private static final String COL_ID = "_id";
        private static final String COL_NAME = "name";
        private static final String COL_DESCRIPTION = "description";
        private static final String COL_QUANTITY = "quantity";
      }
```        

This is the AuthenticationManager class that controlled the instance of user. When you saved or altered data, it would return the current user instance. Fixing this allowed the application to differentiate between users and securely provide checks before data alteration. 

```
    //============================================================================
    // Name        : AuthenticationManager.java
    // Author      : Phillip Cabaniss
    // Version     : 1.0
    // Copyright   : Copyright © 2024 SNHU COCE
    // Description : Class that controls the functionality for authenticating the user and setting the instance. Also returns instance
    //               through AuthenticatedUser.java to keep variables private.
    //============================================================================

    package com.zybooks.mainproject;

    // Controls authentication of user and instances
    public class AuthenticationManager {

    private AuthenticatedUser user;
    private static AuthenticationManager instance;

    private AuthenticationManager() {

    }

    /**
     * Get instance of user for database
     * @return
     */
    public static AuthenticationManager getInstance() {
        if (instance == null) {
            instance = new AuthenticationManager();
        }

        return instance;
    }

    public AuthenticatedUser getUser() {
        return user;
    }

    public void setUser(AuthenticatedUser user) {
        this.user = user;
    }
    }
```
This artifact showcases my understanding of databse concepts and design. It clearly conveys my grasp and execution of the final course outcomes: 
•	Demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals.
•	Develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources.  
