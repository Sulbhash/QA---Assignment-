# QA---Assignment-
"Develop a robust test automation script to thoroughly validate the login functionality and password recovery features of a mobile application's login page. Assume that the login page contains two input fields for username and password, a 'Login' button, and a 'Forgot Password' link.

The script should cover the following test cases :-

1. Verify that a user with valid credentials can successfully log in and access the system.

2. Validate that an error message is displayed when attempting to log in with invalid credentials.

3. Ensure that the login page retains the entered username and password fields' values after a failed login attempt.

4. Test that the 'Login' button is disabled when both username and password fields are empty.

5. Confirm that the 'Login' button is enabled only when both username and password fields are filled with valid input.

6. Verify that clicking the 'Forgot Password' link redirects the user to the password recovery page.

7. Validate the password recovery functionality by following these steps:
    a. Click the 'Forgot Password' link.
    b. Enter a registered email address in the provided field.
    c. Click the 'Recover Password' button.
    d. Verify that a success message is displayed indicating that an email with password recovery instructions          has been sent.
    e. Simulate the password recovery process by accessing the provided email or using a test email account.
    f. Retrieve the recovery instructions and follow the specified steps to reset the password.
    g. Ensure that after successfully resetting the password, the user is redirected to the login page.
    h. Validate that the user can log in with the new password.

8. Account for pagination on the login page and the script to automatically navigate through multiple pages, ensuring that all relevant data is captured.

9. Check the strength of the password and validation messages for the same.
