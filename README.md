# Register_Vikunja
Autotest that creates an account with a username having 2 characters using Unit Test Framework.(Along with the step explanation).

import unittest
from selenium import webdriver
from selenium.webdriver.common.by import By
import time


class MyTestCase(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Chrome()
        self.driver.maximize_window()
        self.driver.implicitly_wait(10)

    def test_create_account(self):
        self.driver.get("https://try.vikunja.io/register")
        print(self.driver.title)
        self.assertIn("Vikunja", self.driver.title)

    def test_enter_credentials(self):
        # Navigate to the registration page
        self.driver.get("https://try.vikunja.io/register")

        # Locate the username field by its ID and enter the username "RJ"
        username_field = self.driver.find_element(By.ID, "username")
        username_field.send_keys("RJ")

        # Locate the email address field by its ID and enter the email address
        email_address_field = self.driver.find_element(By.ID, "email")
        email_address_field.send_keys("abdulsabir00024@gmail.com")

        # Locate the password field by its ID and enter the password
        password_field = self.driver.find_element(By.ID, "password")
        password_field.send_keys("F1rewall@")

        # Locate and click the submit button by its ID
        submit_button = self.driver.find_element(By.ID, "register-submit")
        submit_button.click()

        # Assert that the value entered is "RJ"
        entered_username = username_field.get_attribute("value")
        self.assertEqual("RJ", entered_username)

        # Assert that the value entered is the correct email address
        entered_email_address = email_address_field.get_attribute("value")
        self.assertEqual("abdulsabir00024@gmail.com", entered_email_address)

        # Example of finding a success message and verifying it
        try:
            success_message = self.driver.find_element(By.CSS_SELECTOR, ".alert-success").text
            self.assertIn("registration successful", success_message.lower())

        except Exception as e:
            self.fail(f"Registration failed or success message not found: {str(e)}")

        # Optional: Pause to keep the browser open for 60 seconds for observation
        time.sleep(60)

    def tearDown(self):
        # Close the browser after the test
        self.driver.quit()

if __name__ == "__main__":
    unittest.main()


Step-by-Step Instructions:
Set Up Python Environment:

Ensure you have Python installed on your machine. You can check this by running python --version in your command prompt or terminal.
Install the necessary libraries. You need selenium and unittest. You can install Selenium by running:
pip install selenium
Download the WebDriver:
Download the appropriate WebDriver for the browser you intend to use (e.g., ChromeDriver for Google Chrome).
Ensure that the WebDriver is compatible with your browser version.
Add the WebDriver to your system’s PATH or place it in the same directory as your Python script.
Save the Script:

Copy the provided Python script into a new .py file. For example, name it test_vikunja_registration.py.
Run the Script:
Open a command prompt or terminal.
Navigate to the directory where your test_vikunja_registration.py file is saved.
Run the script by executing:
python test_vikunja_registration.py
