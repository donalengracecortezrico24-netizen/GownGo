# GownGo
Debugging Done!!

CONTEXT: 
    After the system defense last Tuesday (December 16), binigyan kami ni Sir ng debugging task to test our understanding of the system. The goal was to identify the root cause of the error, apply the proper fix, and ensure that the system would work correctly without recurring issues.
    Although challenging, the activity helped us better understand both the code and the troubleshooting process.

ObBSERVED SYSTEM ERROR: 
    At first, the system worked properly and we were able to check out items successfully. Pero nung inulit yung pagcheckout, the system failed and displayed the message:
        “Something went wrong. Please try again.”
    After improving the error handling, the actual error was revealed:
        “SQL ERROR: Duplicate entry '0' for key 'PRIMARY'”
    The error message did not indicate which table or column was causing the issue, making it more difficult to debug.

INITIAL STEPS/TRIES: 
    Initially, we focused on the orders and order_details tables since they are directly involved in the checkout process. While these tables are connected, they were not the main cause of the error.
    Eventually, we discovered that the real issue was located in the payments table. Specifically, the payment_id was not set to AUTO_INCREMENT, which caused MySQL to repeatedly insert a value of 0, leading to the duplicate primary key error.
    Even after fixing the database, the error kept returning because the root cause had not yet been fully addressed.
    With permission from Sir to use AI as a learning aid, we also discovered another issue:
        The order_type ENUM only allowed Rental and Purchase, but the code used the value Mixed, which caused silent failures during order insertion. 

FIXES AND SOLUTIONS:
    First, inalis nami yun corrupted data sa may payments table at inayos ang ID generation, pati yung auto increment inayos na rin.
    Next, the order_type ENUM ay dinagdagan na ng Mixed so as t avoid the silent failures during order insertion. 

FINAL REESULT: 
    After trial and error and applying all the fixes, checkout process works correctly, insertions to orders, order details, and payments goes succesfully and no more recurring SQL errors.

LESSON LEARNED:
    SQL error messages can be misleading and may not point sa actualy table, Database inspection is a must just like code inspection, finally, debugging is a process, not a single fix.

CONTRIBUTIONS:
    Batalla: Paghanap ng bug at pagfix ng system
    Juarez: Paghahanap ng error
    Lozano: Paghahanap ng error
    Rico: Paghanap ng error and pagidentify ng fix

SiIDE NOTE: 
    mahirap maghanap all the more satisfying kapag naayos na ^_^
    Thank you so much sir Reymar Llagas!!