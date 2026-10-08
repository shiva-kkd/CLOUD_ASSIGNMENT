# Experiment 4: Develop a Simple Application Using Apex Programming Language of Salesforce.com

## Aim
To develop a simple custom application using the Apex programming language on the Salesforce cloud platform.

## Prerequisites
- A Salesforce Developer Org (free)
- A web browser with internet access

## Procedure

### Step 1: Sign up for a Salesforce Developer Org
If you don't have one, sign up for a free developer account on the Salesforce Developer Signup page.

### Step 2: Log in to your Developer Org
Access your Salesforce instance using your credentials.

### Step 3: Open the Developer Console
Click the **gear icon** (Setup) in the top-right corner (Salesforce Classic) or top-left (Lightning Experience), then select **Developer Console**.

### Step 4: Create a new Apex class
1. In the Developer Console, go to **File** > **New** > **Apex Class**.
2. Enter a class name (e.g., `HelloWorldApp`) and click **OK**.

### Step 5: Write the Apex code
```apex
public class HelloWorldApp {

    public static void sayHello() {
        System.debug('WELCOME TO APEX PROGRAMMING');
    }

}
```
Click **File** > **Save** to save the class.

### Step 6: Execute the Apex code
1. In the Developer Console, click the **Debug** menu and select **Open Execute Anonymous Window**.
2. Enter the following code:
```apex
   HelloWorldApp.sayHello();
```
3. Make sure the **Open Log** checkbox is selected, then click **Execute**.

### Step 7: View the output
The execution log opens automatically. To see only your message, select the **Debug Only** checkbox in the log inspector.

## Output
```
WELCOME TO APEX PROGRAMMING
```

## Result
A simple Apex application was successfully developed and executed on the Salesforce cloud platform, and the expected message was displayed in the debug log.
<img width="1920" height="1080" alt="Screenshot 2026-10-07 232839" src="https://github.com/user-attachments/assets/4d3da9ab-19a6-4217-8a44-6cae759948c4" />

<img width="1920" height="1080" alt="Screenshot 2026-10-07 233209" src="https://github.com/user-attachments/assets/b8ecf6c3-0a96-46bb-9d5e-42a315f252cb" />

