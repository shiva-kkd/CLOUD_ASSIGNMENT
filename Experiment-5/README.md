# Experiment 5: Implement a Mailing Service Using Apex Programming Language of Salesforce.com

## Aim
To implement a mailing service using the Apex programming language on the Salesforce cloud platform.

## Prerequisites
- A Salesforce Developer Org (free)
- A web browser with internet access
- A valid email address to receive the test mail

## Procedure

### Step 1: Open the Developer Console
Click on **Your Name** or the quick access menu (**Setup gear icon**) in the top-right corner of the Salesforce page, then select **Developer Console**.

### Step 2: Create a new Apex class
Click **File** > **New** > **Apex Class**. Enter `EmailManager` as the class name and click **OK**.

### Step 3: Replace the default class body
```apex
public class EmailManager {

    // Public method
    public void sendMail(String address, String subject, String body) {
        // Create an email message object
        Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
        String[] toAddresses = new String[] {address};
        mail.setToAddresses(toAddresses);
        mail.setSubject(subject);
        mail.setPlainTextBody(body);

        // Pass this email message to the built-in sendEmail method
        // of the Messaging class
        Messaging.SendEmailResult[] results = Messaging.sendEmail(
                                 new Messaging.SingleEmailMessage[] { mail });

        // Call a helper method to inspect the returned results
        inspectResults(results);
    }

    // Helper method
    private static Boolean inspectResults(Messaging.SendEmailResult[] results) {
        Boolean sendResult = true;

        // sendEmail returns an array of result objects.
        // Iterate through the list to inspect results.
        // In this class, the methods send only one email,
        // so we should have only one result.
        for (Messaging.SendEmailResult res : results) {
            if (res.isSuccess()) {
                System.debug('Email sent successfully');
            }
            else {
                sendResult = false;
                System.debug('The following errors occurred: ' + res.getErrors());
            }
        }

        return sendResult;
    }
}
```

### Step 4: Save the class
Click **File** > **Save**.

### Step 5: Test the output
1. Click **Debug** > **Open Execute Anonymous Window**.
2. Enter the following code, replacing `'Your email address'` with your own email address:
```apex
   EmailManager em = new EmailManager();
   em.sendMail('Your email address', 'Email Subject', 'Email Body');
```
3. Click **Execute**, then check your inbox.

### Optional: Calling the method without `new`
Declare the method with the `static` keyword:
```apex
public static void sendMail(String address, String subject, String body) {
    ...
}
```
Then call it as:
```apex
EmailManager.sendMail('Your email address', 'Email Subject', 'Email Body');
```

## Output
- The debug log shows `Email sent successfully`.
- The email with the given subject and body arrives in the recipient's inbox.

## Result
A mailing service was successfully implemented using Apex on the Salesforce platform, and a test email was sent and received.

<img width="1917" height="868" alt="Screenshot 2026-07-21 194517" src="https://github.com/user-attachments/assets/a7a3f101-6db7-4de7-a552-da97beac4980" />

<img width="1897" height="870" alt="Screenshot 2026-07-21 194532" src="https://github.com/user-attachments/assets/2523ec57-1ad7-4dc5-97b6-cee62767db3c" />

