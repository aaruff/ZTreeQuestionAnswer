The below instructions illustrate and describe what is required to display a list of buttons,
and record the order in which they are selected.

Create a Custom Table
============================================
To store the order in which the buttons were clicked, and any other
additional data associated with it, you will have to create your own custom
table. In the example code I have already created a custom table named 
ButtonSelectionHistoryTable. All of the button selection history data will
be stored in this table.


Creating Buttons 
=============
To record the order in which buttons are selected you'll first need some buttons.
In this exaple I have created a set of buttons in the Button Selection stage, and
placed them in a gridbox. You don't have to put the buttons in a gridbox to make
this work, I just did so for convenience. 


Attaching Subject.do Programs to the Buttons
====================================
To record the click actions you will have to attach a subjects.do program to each button. 
Doing so will run the attached program every time a button is clicked.


Recording Button Selections
=======================

Adding a row to the custom table when the button is selected
------------------------------------------------------------------------------------------------
To add a record to a custom table a new row data declaration must
be placed in each button's subject.do program. In this case we would
like to add a new record to the ButtonSelectionHistoryTable. To do so
the following declaration is added to each subject.do program:

```c
    ButtonSelectionHistoryTable.new {
        // row data is added here later....
    }
```

The above essentially tells Z-Tree to put whater declarations are inside of it
into a new row residing in the ButtonSelectionHistoryTable.

Adding row data to the custom table
----------------------------------------------------------
Now that we have declared that row data is to be added to the ButtonSelectionHistoryTable
every time a button is selected, all that remains is to tell Z-Tree what data do add to
the row. In order to do so you will have to declare a new table variable and assign the
value you want to record to it. For example if you would like to record the subject that
clicked on the button you would write the following:

```c
    ButtonSelectionHistoryTable.new {
        subject = :Subject;
    }
```

In the above example, I am declaring a new variable subject and placing the subject ID (Subject)
in it. Since the above ButtonSelectionHistoryTable.new program is running inside of the
subjects.do program it can access the subject variables by prefixing it with a colon (:). 
The colon operator essentially means, use the variable associated with the program running
this one, in this case the subjects.do program.

Adding all of the data to the custom table
-----------------------------------------------------------------
Now you should know enough to understand the button programs:

```c
    subjects.do {  // Gives the ButtonSelectionHistoryTable.new program access to subject variables like Subject.

        ButtonSelectionHistoryTable.new {  // Tells Z-Tree to create a new row in the ButtonSelectionHistoryTable every time this runs
            subject = :Subject;           // Puts the subject ID in the subject column of the new row
            period = :Period;              // Puts the current period number into the period column of the new row
            buttonId = 1;                   // Puts the button 1 in the buttonId column of the new row
        }
    }
```

Adding more buttons
---------------------------------
To add more buttons copy and paste a button containing the button program and increment the buttonId by 1 (e.g. buttonId = 2, or buttonId = 3, etc.)


Displaying The History
=================
To display the table history you can use the contracts list box. To use the contracts table in your program you can use the samples implementation as an
example.


Watching the Program In Action
==========================
To watch the button data get added to the ButtonSelectionHistoryTable as each button is selected:
Run the Treatment, select Run, all tables, and select the ButtonSelectionHistoryTable. You should now be able
to see the record data as it is added to the table when each button is selected.

