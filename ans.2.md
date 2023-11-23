Q13. Write a program in PL/SQL to display a table based detail information for the employee of ID 149 from the employees/company table.

-- PL/SQL block to display employee details for ID 149

```
DECLARE
    v_employee_id NUMBER := 149;
    v_employee_name employees.company_name%TYPE;
    v_employee_job employees.job_title%TYPE;
    v_employee_salary employees.salary%TYPE;
BEGIN
    SELECT company_name, job_title, salary
    INTO v_employee_name, v_employee_job, v_employee_salary
    FROM employees
    WHERE employee_id = v_employee_id;

    -- Display the employee details
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_employee_id);
    DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_employee_name);
    DBMS_OUTPUT.PUT_LINE('Employee Job Title: ' || v_employee_job);
    DBMS_OUTPUT.PUT_LINE('Employee Salary: ' || v_employee_salary);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee with ID ' || v_employee_id || ' not found');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
/
```


Q14.Create a PL/SQL procedure that takes department as input from a user &amp; print
the number of employees working in that department in the same variable?

-- Create a PL/SQL procedure to count employees in a department
```
CREATE OR REPLACE PROCEDURE CountEmployeesInDepartment (
    p_department_name IN employees.department%TYPE,
    p_employee_count OUT NUMBER
)
IS
BEGIN
    -- Initialize the employee count to 0
    p_employee_count := 0;
    
    -- Cursor to fetch employees in the specified department
    FOR emp_rec IN (SELECT employee_id FROM employees WHERE department = p_department_name)
    LOOP
        -- Increment the employee count
        p_employee_count := p_employee_count + 1;
    END LOOP;
    
    -- Display the employee count
    DBMS_OUTPUT.PUT_LINE('Number of employees in ' || p_department_name || ': ' || p_employee_count);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Department ' || p_department_name || ' not found');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
/
```

Q15.Write a PL/SQL program using WHILE loop for calculating the average of
the numbers entered by user. Stop the entry of numbers whenever the user enters
the number 0.

-- Create a PL/SQL program to calculate the average of user-entered numbers
```
SET SERVEROUTPUT ON;

DECLARE
    v_total NUMBER := 0;     -- Initialize the total to 0
    v_count NUMBER := 0;     -- Initialize the count to 0
    v_number NUMBER;         -- Variable to store user input
    
BEGIN
    -- Prompt the user to enter numbers until 0 is entered
    DBMS_OUTPUT.PUT_LINE('Enter numbers (enter 0 to stop):');
    
    WHILE TRUE -- Infinite loop until user enters 0
    LOOP
        -- Read the user input
        DBMS_OUTPUT.PUT('Enter a number: ');
        v_number := TO_NUMBER(TO_CHAR(&v_number));

        -- Check if the entered number is 0, and if so, exit the loop
        IF v_number = 0 THEN
            EXIT;
        END IF;

        -- Add the entered number to the total and increment the count
        v_total := v_total + v_number;
        v_count := v_count + 1;
    END LOOP;

    -- Calculate and display the average
    IF v_count > 0 THEN
        DBMS_OUTPUT.PUT_LINE('Average of entered numbers: ' || (v_total / v_count));
    ELSE
        DBMS_OUTPUT.PUT_LINE('No numbers were entered.');
    END IF;
    
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
/
```


-- Create a PL/SQL block to check if a string is a palindrome
```
SET SERVEROUTPUT ON;
DECLARE
    v_input_string VARCHAR2(4000);
    v_is_palindrome BOOLEAN;
BEGIN
    v_input_string := 'racecar'; -- Replace with your string to check
    v_is_palindrome := IsPalindrome(v_input_string);

    IF v_is_palindrome THEN
        DBMS_OUTPUT.PUT_LINE(v_input_string || ' is a palindrome.');
    ELSE
        DBMS_OUTPUT.PUT_LINE(v_input_string || ' is not a palindrome.');
    END IF;
END;
/
```

Q17.Write PL/SQL program to find the sum of digits of a number.

-- Create a PL/SQL program to find the sum of digits of a number
```
SET SERVEROUTPUT ON;

DECLARE
    v_input_number NUMBER := 12345; -- Replace with your number
    v_number_copy NUMBER := v_input_number;
    v_sum_of_digits NUMBER := 0;
    v_digit NUMBER;
BEGIN
    -- Check if the input number is negative and make it positive
    IF v_input_number < 0 THEN
        v_input_number := -v_input_number;
    END IF;

    -- Extract and sum the digits
    WHILE v_input_number > 0
    LOOP
        v_digit := MOD(v_input_number, 10);
        v_sum_of_digits := v_sum_of_digits + v_digit;
        v_input_number := TRUNC(v_input_number / 10);
    END LOOP;

    -- Display the sum of digits
    DBMS_OUTPUT.PUT_LINE('Sum of digits in ' || v_number_copy || ' is: ' || v_sum_of_digits);
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;
/
```


Q18.Write a procedure to display the records from Manufacturing industry table.

-- Create a PL/SQL procedure to display records from the Manufacturing Industry table
```
CREATE OR REPLACE PROCEDURE DisplayManufacturingRecords AS
BEGIN
    -- Declare variables to store columns from the Manufacturing Industry table
    DECLARE
        v_company_name VARCHAR2(100);
        v_location VARCHAR2(100);
        v_product_name VARCHAR2(100);
        v_production_date DATE;
    BEGIN
        -- Cursor to fetch records from the Manufacturing Industry table
        FOR rec IN (SELECT company_name, location, product_name, production_date FROM Manufacturing_Industry)
        LOOP
            -- Assign values from the cursor to variables
            v_company_name := rec.company_name;
            v_location := rec.location;
            v_product_name := rec.product_name;
            v_production_date := rec.production_date;

            -- Display the record details
            DBMS_OUTPUT.PUT_LINE('Company Name: ' || v_company_name);
            DBMS_OUTPUT.PUT_LINE('Location: ' || v_location);
            DBMS_OUTPUT.PUT_LINE('Product Name: ' || v_product_name);
            DBMS_OUTPUT.PUT_LINE('Production Date: ' || TO_CHAR(v_production_date, 'DD-MON-YYYY'));
            DBMS_OUTPUT.PUT_LINE('-----------------------------------------');
        END LOOP;
    END;
END;
/
```

```
-- Execute the procedure to display Manufacturing Industry records
BEGIN
    DisplayManufacturingRecords;
END;
/
```


Q19.Write a procedure to display the records from Hospital table.

-- Create a PL/SQL procedure to display records from the Hospital table
```
CREATE OR REPLACE PROCEDURE DisplayHospitalRecords AS
BEGIN
    -- Declare variables to store columns from the Hospital table
    DECLARE
        v_hospital_name VARCHAR2(100);
        v_location VARCHAR2(100);
        v_specialty VARCHAR2(100);
    BEGIN
        -- Cursor to fetch records from the Hospital table
        FOR rec IN (SELECT hospital_name, location, specialty FROM Hospital)
        LOOP
            -- Assign values from the cursor to variables
            v_hospital_name := rec.hospital_name;
            v_location := rec.location;
            v_specialty := rec.specialty;

            -- Display the record details
            DBMS_OUTPUT.PUT_LINE('Hospital Name: ' || v_hospital_name);
            DBMS_OUTPUT.PUT_LINE('Location: ' || v_location);
            DBMS_OUTPUT.PUT_LINE('Specialty: ' || v_specialty);
            DBMS_OUTPUT.PUT_LINE('-----------------------------------------');
        END LOOP;
    END;
END;
/
```

```
-- Execute the procedure to display Hospital records
BEGIN
    DisplayHospitalRecords;
END;
/
```


Q20.Write a PL/SQL program to display the employee IDs, names, job titles, hire
dates, and salaries of all employees.
-- Create a PL/SQL program to display employee details
```
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id NUMBER;
    v_employee_name VARCHAR2(100);
    v_job_title VARCHAR2(100);
    v_hire_date DATE;
    v_salary NUMBER;
BEGIN
    -- Cursor to fetch employee details
    FOR emp_rec IN (SELECT employee_id, employee_name, job_title, hire_date, salary FROM employees)
    LOOP
        -- Assign values from the cursor to variables
        v_employee_id := emp_rec.employee_id;
        v_employee_name := emp_rec.employee_name;
        v_job_title := emp_rec.job_title;
        v_hire_date := emp_rec.hire_date;
        v_salary := emp_rec.salary;

        -- Display the employee details
        DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_employee_id);
        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_employee_name);
        DBMS_OUTPUT.PUT_LINE('Job Title: ' || v_job_title);
        DBMS_OUTPUT.PUT_LINE('Hire Date: ' || TO_CHAR(v_hire_date, 'DD-MON-YYYY'));
        DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
        DBMS_OUTPUT.PUT_LINE('-----------------------------------------');
    END LOOP;
END;
/
```

Q21.Write a PL/SQL program to display the names of all countries.
-- Create a PL/SQL program to display the names of all countries
```
SET SERVEROUTPUT ON;

DECLARE
    v_country_name VARCHAR2(100);
BEGIN
    -- Cursor to fetch country names
    FOR country_rec IN (SELECT country_name FROM countries)
    LOOP
        -- Assign the country name from the cursor to a variable
        v_country_name := country_rec.country_name;

        -- Display the country name
        DBMS_OUTPUT.PUT_LINE('Country Name: ' || v_country_name);
    END LOOP;
END;
/
```


Q22.Consider the Following schema
Emp (eno, ename, designation, salary, dno)
Dept (dno dname,dhod)
1. Increment the salary of all ‘comp’ dept employees with 10 %
2. Display the ename and designation if salary is above 35000 of dno 101
3. Create the trigger on emp Table: The deleted record from the emp table
should be insert in Dummy Table
Ans 1-
-- Update the salary of 'comp' department employees with a 10% raise
```
UPDATE Emp
SET salary = salary * 1.10
WHERE dno = 101 AND designation = 'comp';
```

Ans2-
-- Display ename and designation of employees in department 101 with salary > 35000
```
SELECT ename, designation
FROM Emp
WHERE dno = 101 AND salary > 35000;
```

Ans3-
-- Create a trigger to insert deleted records into a Dummy table
```
CREATE OR REPLACE TRIGGER DeleteTrigger
BEFORE DELETE
ON Emp
FOR EACH ROW
BEGIN
    INSERT INTO Dummy (eno, ename, designation, salary, dno)
    VALUES (:OLD.eno, :OLD.ename, :OLD.designation, :OLD.salary, :OLD.dno);
END;
/
```

Q23.Consider the Following schema
Boats(Bid, Name, Bcolor)
Sailors(Sid,Sname, Srating)
Reserves (Bid, Sid, Date of Reservation)
1. Create the trigger on Sailors Table: The Rating of the Sailor should get incremented by 1 once the sailor reserves a boat.
2. Create the Cursor which will Insert the Sid, Sname, Bid who reserved red color Boat in Red_Boats Table;

Ans1-
-- Create a trigger on the "Reserves" table to increment the sailor's rating
```
CREATE OR REPLACE TRIGGER IncrementSailorRating
AFTER INSERT
ON Reserves
FOR EACH ROW
BEGIN
    UPDATE Sailors
    SET Srating = Srating + 1
    WHERE Sid = :NEW.Sid;
END;
/
```

Ans2-
-- Create a cursor to insert sailors who reserved red boats into the "Red_Boats" table
```
DECLARE
    v_Sid Sailors.Sid%TYPE;
    v_Sname Sailors.Sname%TYPE;
    v_Bid Boats.Bid%TYPE;
    v_Bcolor Boats.Bcolor%TYPE;
    
    CURSOR RedBoatsCursor IS
        SELECT r.Sid, s.Sname, r.Bid, b.Bcolor
        FROM Reserves r
        JOIN Sailors s ON r.Sid = s.Sid
        JOIN Boats b ON r.Bid = b.Bid
        WHERE b.Bcolor = 'red';

BEGIN
    FOR RedBoatRec IN RedBoatsCursor
    LOOP
        v_Sid := RedBoatRec.Sid;
        v_Sname := RedBoatRec.Sname;
        v_Bid := RedBoatRec.Bid;
        v_Bcolor := RedBoatRec.Bcolor;

        -- Insert records into the "Red_Boats" table
        INSERT INTO Red_Boats (Sid, Sname, Bid, Bcolor)
        VALUES (v_Sid, v_Sname, v_Bid, v_Bcolor);
    END LOOP;
END;
/
```

Q24.Consider the Following schema
Books ( Sid, Bid, BName, BPrice )
Transactions (Sid,Bid, Date_Issue,Date_Return, Status)
Return_books (Sid,Bid, Fine_amout )
1. Create a trigger on Books Table such that insertion of Books details to insert
a record in Transaction table (Sid and Bid values should be Same, others
values can be Assumable )
2. Display the Book Names Issued to Sid ‘XXX’ using Cursor

Ans1-
-- Create a trigger on the "Books" table to insert a record into the "Transactions" table
```
CREATE OR REPLACE TRIGGER InsertTransaction
AFTER INSERT
ON Books
FOR EACH ROW
BEGIN
    INSERT INTO Transactions (Sid, Bid, Date_Issue, Date_Return, Status)
    VALUES (:NEW.Sid, :NEW.Bid, SYSDATE, NULL, 'Issued');
END;
/
```

Ans2-
-- Create a cursor to display book names issued to a specific Sid
```
DECLARE
    v_Sid Books.Sid%TYPE := 'XXX'; -- Replace 'XXX' with the desired Sid
    v_BName Books.BName%TYPE;

    CURSOR IssuedBooksCursor IS
        SELECT b.BName
        FROM Books b
        JOIN Transactions t ON b.Sid = t.Sid AND b.Bid = t.Bid
        WHERE t.Sid = v_Sid;

BEGIN
    OPEN IssuedBooksCursor;
    FETCH IssuedBooksCursor INTO v_BName;
    
    DBMS_OUTPUT.PUT_LINE('Books issued to Sid ' || v_Sid || ':');
    
    WHILE IssuedBooksCursor%FOUND
    LOOP
        DBMS_OUTPUT.PUT_LINE(v_BName);
        FETCH IssuedBooksCursor INTO v_BName;
    END LOOP;
    
    CLOSE IssuedBooksCursor;
END;
/
```

Q25.Consider the Following schema
Books ( Sid, Bid, BName, BPrice )
Transactions (Sid,Bid, Date_Issue,Date_Return, Status)
Return_books (Sid,Bid, Fine_amout )
1. Update the Date_Return of Sid ‘xxx’ . Then Create the Trigger to Update the
Status of Book to ‘Return’
2. Create a cursor which will calculate the Fine_Amount and insert the
‘Return’ Books in Return_books table.
Conditions:
If No of Days Between Date_Issue and Date_Return &gt; 15 Days,
Fine_amount is : 10 Rs Per Day
If No of Days Between Date_Issue and Date_Return &gt; 16 Days and &lt; 30
Days, Fine_amount is : 20 Rs Per Day
If No of Days Between Date_Issue and Date_Return &gt; 30 Days,
Fine_amount is : 30 Rs Per Day

Ans1-
-- Update the Date_Return of Sid 'xxx'
```
UPDATE Transactions
SET Date_Return = SYSDATE -- Replace SYSDATE with the desired return date
WHERE Sid = 'xxx';
```

Ans2-
-- Create a cursor to calculate Fine_Amount and insert records into Return_books
```
DECLARE
    CURSOR FineCursor IS
        SELECT t.Sid, t.Bid, t.Date_Issue, t.Date_Return
        FROM Transactions t
        WHERE t.Status = 'Return' AND t.Date_Return IS NOT NULL;

    v_Sid Transactions.Sid%TYPE;
    v_Bid Transactions.Bid%TYPE;
    v_Date_Issue Transactions.Date_Issue%TYPE;
    v_Date_Return Transactions.Date_Return%TYPE;
    v_Fine_Amount Return_books.Fine_amount%TYPE;
BEGIN
    OPEN FineCursor;
    
    LOOP
        FETCH FineCursor INTO v_Sid, v_Bid, v_Date_Issue, v_Date_Return;
        EXIT WHEN FineCursor%NOTFOUND;
        
        -- Calculate Fine_Amount based on specific conditions
        IF v_Date_Return - v_Date_Issue > 30 THEN
            v_Fine_Amount := 30 * (v_Date_Return - v_Date_Issue);
        ELSIF v_Date_Return - v_Date_Issue > 15 THEN
            v_Fine_Amount := 10 * (v_Date_Return - v_Date_Issue);
        ELSIF v_Date_Return - v_Date_Issue > 0 THEN
            v_Fine_Amount := 20 * (v_Date_Return - v_Date_Issue);
        END IF;
        
        -- Insert records into Return_books
        INSERT INTO Return_books (Sid, Bid, Fine_amount)
        VALUES (v_Sid, v_Bid, v_Fine_Amount);
    END LOOP;
    
    CLOSE FineCursor;
END;
/
```

Q26.Consider the Following schema
Books ( Sid, Bid, BName, BPrice )
Transactions (Sid,Bid, Date_Issue,Date_Return, Status)
Return_books (Sid,Bid, Fine_amout )

1. Create a trigger on Books Table such that insertion of Books details to insert
a record in Transaction table (Sid and Bid values should be Same, others
values can be Assumable )
2. Create a cursor which will calculate the Fine_Amount and insert the
‘Return’ Books in Return_books table.
Conditions:
If No of Days Between Date_Issue and Date_Return &gt; 15 Days,
Fine_amount is : 10 Rs Per Day
If No of Days Between Date_Issue and Date_Return &gt; 16 Days and &lt; 30
Days, Fine_amount is : 20 Rs Per Day
If No of Days Between Date_Issue and Date_Return &gt; 30 Days,
Fine_amount is : 30 Rs Per Day

Ans1-
-- Create a trigger on the "Books" table to insert a record into the "Transactions" table
```

CREATE OR REPLACE TRIGGER InsertTransaction
AFTER INSERT
ON Books
FOR EACH ROW
BEGIN
    INSERT INTO Transactions (Sid, Bid, Date_Issue, Date_Return, Status)
    VALUES (:NEW.Sid, :NEW.Bid, SYSDATE, NULL, 'Issued');
END;
/
```

Ans2-
-- Create a cursor to calculate Fine_Amount and insert records into Return_books
```
DECLARE
    CURSOR FineCursor IS
        SELECT t.Sid, t.Bid, t.Date_Issue, t.Date_Return
        FROM Transactions t
        WHERE t.Status = 'Issued' AND t.Date_Return IS NOT NULL;

    v_Sid Transactions.Sid%TYPE;
    v_Bid Transactions.Bid%TYPE;
    v_Date_Issue Transactions.Date_Issue%TYPE;
    v_Date_Return Transactions.Date_Return%TYPE;
    v_Fine_Amount Return_books.Fine_amout%TYPE;
BEGIN
    OPEN FineCursor;
    
    LOOP
        FETCH FineCursor INTO v_Sid, v_Bid, v_Date_Issue, v_Date_Return;
        EXIT WHEN FineCursor%NOTFOUND;
        
        -- Calculate Fine_Amount based on specific conditions
        IF v_Date_Return - v_Date_Issue > 30 THEN
            v_Fine_Amount := 30 * (v_Date_Return - v_Date_Issue);
        ELSIF v_Date_Return - v_Date_Issue > 15 THEN
            v_Fine_Amount := 20 * (v_Date_Return - v_Date_Issue);
        ELSIF v_Date_Return - v_Date_Issue > 0 THEN
            v_Fine_Amount := 10 * (v_Date_Return - v_Date_Issue);
        END IF;
        
        -- Insert records into Return_books
        INSERT INTO Return_books (Sid, Bid, Fine_amout)
        VALUES (v_Sid, v_Bid, v_Fine_Amount);
    END LOOP;
    
    CLOSE FineCursor;
END;
/
```

Q27.Perform the CRUD Operations in MongoDB
// Example: Connecting to a MongoDB database
// Replace 'yourMongoDBConnectionURL' with your actual MongoDB connection URL
```
const mongoClient = new MongoClient('yourMongoDBConnectionURL', { useNewUrlParser: true });

// Connecting to the database
mongoClient.connect(function(err, client) {
    if (err) {
        console.error('Error connecting to the database:', err);
        return;
    }

    // Access the database and collection
    const db = client.db('yourDatabaseName');
    const collection = db.collection('yourCollectionName');

    // Create (Insert) Documents
    collection.insertOne({
        key1: 'value1',
        key2: 'value2'
    });

    collection.insertMany([
        { key1: 'value1', key2: 'value2' },
        { key1: 'value3', key2: 'value4' }
    ]);

    // Read (Query) Documents
    // Find all documents in the collection
    collection.find().toArray(function(err, docs) {
        if (err) {
            console.error('Error reading documents:', err);
        } else {
            console.log('All Documents:', docs);
        }
    });

    // Find documents with specific criteria
    collection.find({ key: 'value' }).toArray(function(err, docs) {
        if (err) {
            console.error('Error reading documents:', err);
        } else {
            console.log('Documents with specific criteria:', docs);
        }
    });

    // Update Documents
    // Update a single document
    collection.updateOne(
        { key: 'value' },  // Filter criteria
        { $set: { newKey: 'newValue' } }  // Update action
    );

    // Update multiple documents
    collection.updateMany(
        { key: 'value' },  // Filter criteria
        { $set: { newKey: 'newValue' } }  // Update action
    );

    // Delete Documents
    // Delete a single document
    collection.deleteOne({ key: 'value' });

    // Delete multiple documents
    collection.deleteMany({ key: 'value' });

    // Close the database connection
    client.close();
});
```
