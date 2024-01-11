# QA---Assignment-



package app_test;

import java.net.URL;


import io.appium.java_client.android.AndroidDriver;

import io.appium.java_client.android.options.UiAutomator2Options;
import junit.framework.Assert;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class MobileAppLoginTest {

    private AndroidDriver driver;

    @BeforeMethod
    public void setUp() throws Exception {
        UiAutomator2Options options = new UiAutomator2Options();
        options.setDeviceName("Set Device name");
        options.setApp("Apllication build path.apk");
        driver = new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"), options);
        Thread.sleep(2000);
        
    }

    @Test
    public void SuccessfulLogin() {
        // Test Case 1: Verify that a user with valid credentials can successfully log in.
     //   login("valid_username", "valid_password");
        driver.findElement(By.xpath("Xpath of username")).sendKeys("subhash123@gmail.com");
        driver.findElement(By.xpath("Xpath of password")).sendKeys("@subhash");
        driver.findElement(By.xpath("Xpath of login btn")).click();
		
        
		//Get any text from next page  Ex. Homepage
		String text=driver.findElement(By.xpath("Xpath of HomePage text")).getText();
		String expected="Homepage";
		
		Assert.assertEquals(text, expected);
		
        
    }

    @Test
    public void InvalidLogin() {
        // Test Case 2: Validate that an error message is displayed with invalid credentials.
    	driver.findElement(By.xpath("Xpath of username")).sendKeys("subhash1@gmail.com");
        driver.findElement(By.xpath("Xpath of password")).sendKeys("@subhash1");
        driver.findElement(By.xpath("Xpath of login btn")).click();
        WebElement invalidtext=driver.findElement(By.xpath("Xpath of Error Message Displayed"));
        if (invalidtext.isDisplayed()) {
        	System.out.println(invalidtext.getText());
        }else {
        	System.out.println("Sucessfully Logged In");
        }
    }

    @Test
    public void RetainFieldsAfterFailedLogin() {
        // Test Case 3: Ensure that the login page retains the entered username and password after a failed login.
        
    	WebElement username = driver.findElement(By.xpath("Xpath of username"));
       WebElement password =  driver.findElement(By.xpath("Xpath of password"));
        WebElement loginbtn = driver.findElement(By.xpath("Xpath of login btn")); 	
       WebElement errormassage =  driver.findElement(By.xpath("Xpath of error massege"));
       username.sendKeys("subhash123@gmail.com");
       password.sendKeys("@subhash");
       
       
       loginbtn.click();
       
       String expectedErrorMessage = "Invalid credentials. Please try again.";
       Assert.assertEquals(errormassage.getText(), expectedErrorMessage, "Error message should be displayed");
       
       String retainedUsername = username.getText();
       String retainedPassword = password.getText();
       Assert.assertEquals(retainedUsername, "your_username", "Username should be retained");
       Assert.assertEquals(retainedPassword, "your_password", "Password should be retained");
         
        
        // Add assertions to confirm the retained values.
    }

    @Test
    public void DisabledLoginButtonEmptyFields() {
        // Test Case 4: Test that the 'Login' button is disabled when both fields are empty.
        // Add assertions to confirm the 'Login' button state.
        WebElement loginbtn=driver.findElement(By.xpath("Xpath of login btn"));
        if(loginbtn.isEnabled()) {
        	loginbtn.click();
        }else {
        	System.out.println("Login button is not clickable");
        }
    }

    @Test
    public void EnabledLoginButtonValidInput() {
        // Test Case 5: Confirm that the 'Login' button is enabled only with valid input.
        driver.findElement(By.xpath("Xpath of username")).sendKeys("subhash123@gmail.com");
        driver.findElement(By.xpath("Xpath of password")).sendKeys("@subhash");
        WebElement loginbtn =   driver.findElement(By.xpath("Xpath of login btn"));
     // Check if the 'Login' button is enabled
        boolean isLoginButtonEnabled = loginbtn.isEnabled();
       
    	
     // Assert that the 'Login' button is enabled with valid input
       
    	   Assert.assertTrue(isLoginButtonEnabled);
       
    }

    @Test
    public void ForgotPasswordRedirect() {
        // Test Case 6: Verify that clicking the 'Forgot Password' link redirects to the password recovery page.
        
    	  WebElement forgotpass =driver.findElement(By.xpath("Xpath_of_forgot_password"));
    	  
    	  forgotpass.click();
    	  
    	  String recoveryPage =driver.findElement(By.xpath("Xpath_of_recovery_page_title")).getText();
    	  
    	  Assert.assertEquals(recoveryPage, "tital of recovery page");
    }

    @Test
    public void PasswordRecoveryFunctionality() {
        // Test Case 7: Validate password recovery functionality.
       
        WebElement forgotpasslink =driver.findElement(By.xpath("Xpath_of_forgot_password_link"));
        WebElement emailinput =driver.findElement(By.xpath("Xpath_of_emailinput"));
        WebElement recoverybtn =driver.findElement(By.xpath("Xpath_recovery_btn"));
        
        forgotpasslink .click();
        emailinput.sendKeys("subhash123@gmail.com");   //registered Email_id
        
        recoverybtn.click();
        
        String SuccessMassege =driver.findElement(By.xpath("Xpath_of_success_Massege")).getText();
  	  
  	  Assert.assertEquals(SuccessMassege, "password recovery should be successful");
        
    }

    @Test
    public void PaginationOnLoginPage() {
        // Test Case 8: Account for pagination on the login page.
    	
    	  driver.findElement(By.xpath("Xpath of username")).sendKeys("subhash123@gmail.com");
          driver.findElement(By.xpath("Xpath of password")).sendKeys("@subhash");
          WebElement nextbtn= driver.findElement(By.xpath("Xpath_OF_Next_btn"));
         WebElement loginBtn= driver.findElement(By.xpath("Xpath of login btn"));
         
         nextbtn.click();
         
         WebElement additionalInput=driver.findElement(By.xpath("Xpath_of_additional_input_filed"));
         additionalInput.sendKeys("additional_info");
         
         loginBtn.click();
         
         String SuccessMassege =driver.findElement(By.xpath("Xpath_of_success_Massege")).getText();
     	  
     	  Assert.assertEquals(SuccessMassege, "login should be successful");
           
    }

    @Test
    public void CheckPasswordStrength() {
        // Test Case 9: Check password strength and validation messages.
    	
    	  WebElement passinput =driver.findElement(By.xpath("Xpath_of_password_input"));
    	  
    	  WebElement strengthindicater =driver.findElement(By.xpath("Xpath_of_strenghtindicater"));
    	  
    	  WebElement validationmassege =driver.findElement(By.xpath("Xpath_of_Valoidation_massege"));
    	  
    	  
    	  passinput .sendKeys("weakpassword");
    	  
    	  String weakStrength =strengthindicater.getText();
    	  String Weakvalidationmassege =validationmassege.getText();
    	  
    	  Assert.assertEquals(weakStrength, "Weak", "Weak password strength indicator should be displayed");
    	    Assert.assertEquals(validationmassege.equals("weak"), "Weak password validation message should be displayed");
    	    // Clear the password input
    	    passinput.clear();
    	    // Test a strong password
    	    passinput.sendKeys("StrongPassword123!");
    	    
    	    String StrongStrength =strengthindicater.getText();
      	  String Strongvalidationmassege =validationmassege.getText();
      	  
      	 Assert.assertEquals(StrongStrength, "Strong", "Strong password strength indicator should be displayed");
         Assert.assertEquals(Strongvalidationmassege.contains("strong"), "Strong password validation message should be displayed");
      	 
    }

    @AfterMethod
    public void tearDown() {
        // Close the WebDriver
        if (driver != null) {
            driver.quit();
        }
    }

    
}

