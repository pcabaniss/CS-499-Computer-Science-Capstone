[Home](README.md) - [Code Review](CodeReview.md) - [Software Engineering and Design](SoftwareEngineering_Design.md) - [Data Structures and Algorithms](DataStructures_Algorithms.md) - [Databases](Database.md)

# Binary Search Tree Algorithm

### Narrative
This artifact was originally made in CS-260: Data Structures and Algorithms about 5 months ago. It is a program in C++ that implements a binary search tree algorithm, allowing the user to perform tasks.  The program allows the user to:
- Load the bids using a .csv parser
- Display all the nodes in the tree
- Search for a specific node by ID
- Display the results of the speed when searching or loading information.
- Delete a certain node based on the ID
While this is the main functionality of the program, many methods are operating on the back end. The artifact I chose implements all the same functionality but in the Java language.

[This link](BinarySearchTreeC++.zip) goes to the original Binary Search Tree project.

Original C++ main function:

    int main(int argc, char* argv[]) {

    // process command line arguments
    string csvPath, bidKey;
    switch (argc) {
    case 2:
        csvPath = argv[1];
        bidKey = "98129";
        break;
    case 3:
        csvPath = argv[1];
        bidKey = argv[2];
        break;
    default:
        csvPath = "eBid_Monthly_Sales_Dec_2016.csv";
        bidKey = "98129";
    }

    // Define a timer variable
    clock_t ticks;

    // Define a binary search tree to hold all bids
    BinarySearchTree* bst;
    bst = new BinarySearchTree();
    Bid bid;

    int choice = 0;
    while (choice != 9) {
        cout << "Menu:" << endl;
        cout << "  1. Load Bids" << endl;
        cout << "  2. Display All Bids" << endl;
        cout << "  3. Find Bid" << endl;
        cout << "  4. Remove Bid" << endl;
        cout << "  9. Exit" << endl;
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {

        case 1:
            // Initialize a timer variable before loading bids
            ticks = clock();

            // Complete the method call to load the bids
            loadBids(csvPath, bst);

            //cout << " bids read" << endl;

            // Calculate elapsed time and display result
            ticks = clock() - ticks; // current clock ticks minus starting clock ticks
            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;
            break;

        case 2:
            bst->InOrder();
            break;

        case 3:
            ticks = clock();

            bid = bst->Search(bidKey);

            ticks = clock() - ticks; // current clock ticks minus starting clock ticks

            if (!bid.bidId.empty()) {
                displayBid(bid);
            } else {
            	cout << "Bid Id " << bidKey << " not found." << endl;
            }

            cout << "time: " << ticks << " clock ticks" << endl;
            cout << "time: " << ticks * 1.0 / CLOCKS_PER_SEC << " seconds" << endl;

            break;

        case 4:
            bst->Remove(bidKey);
            break;
        }
    }

    cout << "Good bye." << endl;

	return 0;
    }
### Enhancements
The enhancement planned was to build the exact program in the Java language. This came with its own issues. For example, the .csv parser in C++ was provided by the instructor of the course when it was made. In Java, there is a CSVParser class that I implemented to parse and sort the .csv file. This sorted list could then be interacted with using the terminal. All of the functionality in the C++ version was implemented in the Java version. I made a few enhancements to the code structure as well. I put the binary search tree in its own file for better organization and less clutter on the main. This artifact showcases my understanding of both C++ and the Java language and structure. 

[This link](Artifact2.zip) goes to the original Binary Search Tree project.


    //============================================================================
    // Name        : Main.java
    // Author      : Phillip Cabaniss
    // Version     : 1.0
    // Copyright   : Copyright © 2024 SNHU COCE
    // Description : A file that controls the flow of the program by using the methods within the
    // BinarySearchTree.java file.
    //============================================================================

    package org.example;

    import java.time.Clock;
    import java.time.Duration;
    import java.util.Scanner;

    public class Main {
        public static void main(String[] args) {


        // File path
        String csvPath = "eBid_Monthly_Sales.csv";

        // Scanner for reading user input
        Scanner scanner = new Scanner(System.in);

        // Instantiate binary search tree
        BinarySearchTree bst;
        bst = new BinarySearchTree();

        long startTime;
        long stopTime;
        double ticks;

        int choice = 0;

        // While loop to control the UI.
        while (choice != 9) {
            System.out.println("Menu: ");
            System.out.println("    1. Load Bids ");
            System.out.println("    2. Display All Bids");
            System.out.println("    3. Find Bid");
            System.out.println("    4. Remove Bid");
            System.out.println("    9. Exit");
            System.out.println("Enter Choice: ");
            int input = Integer.parseInt(scanner.nextLine());


            switch (input) {

                // Load the bids into the tree and display the time elapsed
                case 1:
                    startTime = System.currentTimeMillis();
                    bst.loadBids(csvPath, bst);
                    stopTime = System.currentTimeMillis();

                    ticks = ((stopTime - startTime));
                    System.out.println("Time: " + ticks + " ticks.");
                    System.out.println("Elapsed time was " + (ticks * 1.0 / 100000) + " seconds.");
                    break;

                // Display the bids in order from the ID
                case 2:
                    try{
                        bst.inOrder();
                    }
                    catch (Error e) {
                        System.out.println("Cannot display more, file is too long.");
                    }
                    break;

                // Search for bid by ID and display the details and display the time elapsed.
                case 3:
                    System.out.println("Please enter a valid Bid ID");

                    // Improvement from C++ version, now searches by input instead of hardcoded string
                    // Get user input
                    String findBid = scanner.nextLine();

                    startTime = System.currentTimeMillis();
                    Bid found = bst.Search(findBid);
                    if (found != null) {
                        bst.displayBid(found);
                    }
                    else {
                        System.out.println("There was an issue finding the bid, please try again.");
                    }
                    stopTime = System.currentTimeMillis();

                    ticks = ((stopTime - startTime));
                    System.out.println("Time: " + ticks + " ticks.");
                    System.out.println("Elapsed time was " + (ticks * 1.0 / 100000) + " seconds.");

                    break;

                // Remove a bid by searching for it by ID.
                case 4:
                    System.out.println("Please enter a valid Bid ID");

                    // Improvement from C++ version, now removes by input instead of hardcoded string
                    // Get user input
                    String bidID = scanner.nextLine();
                    Bid check = bst.Search(bidID);
                    if (check != null) {
                        bst.Remove(bidID);
                    }
                    else {
                        System.out.println("There was an issue finding the bid, please try again.");
                    }
                    break;

                // Catch wrong input
                default:
                    System.out.println("Please make sure you put in  a valid number and try again. ");


            }
        }

        System.out.println("Good bye.");

    }

    }


This enhancement is a clear indicator of my understanding of 2 more of the course outcomes. 
- Design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution while managing the trade-offs involved in design choices.
- Demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals.
