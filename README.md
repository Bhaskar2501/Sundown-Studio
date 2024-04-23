import pytest
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

class TestWynkMusicTest():
    def setup_method(self, method):
        self.driver = webdriver.Chrome()
        self.driver.maximize_window()  # Maximize the browser window
        self.wait = WebDriverWait(self.driver, 10)  # Use WebDriverWait for better element waiting

    def teardown_method(self, method):
        self.driver.quit()

    def test_wynk_music(self):
        self.driver.get("https://wynk.in/music")

        # Click on the sign in button
        sign_in_button = self.wait.until(EC.element_to_be_clickable(("xpath", "/html/body/div[1]/header/section[1]/div[2]/span/div")))
        sign_in_button.click()

        # Enter phone number
        phone_input = self.wait.until(EC.element_to_be_clickable(("xpath", "/html/body/div[3]/div/div/div/div/div[2]/div/div[2]/div[2]/form/div[1]/input")))
        phone_input.send_keys("8960044221")  # Replace with your phone number

        # Click on the continue button
        continue_button = self.driver.find_element("xpath", "/html/body/div[3]/div/div/div/div/div[2]/div/div[2]/div[2]/form/div[2]/button[2]")
        continue_button.click()

        # Wait for OTP input field to be visible
        otp_input = self.wait.until(EC.visibility_of_element_located(("xpath", "/html/body/div[3]/div/div/div/div/div[2]/div/div[2]/div[2]/form/div[1]/input")))

        # Enter OTP
        otp_input.send_keys("")  # Replace with your OTP

        # Click on the submit button
        submit_button = self.driver.find_element("xpath", "/html/body/div[3]/div/div/div/div/div[2]/div/div[2]/div[2]/form/div[2]/button")
        submit_button.click()

        # Wait for login to complete (you may need to add more explicit waits depending on the actual login flow)
        time.sleep(15)

        # Now you should be logged in and can proceed with your test steps
        # For example, you can search for a song and click on it
        search_box = self.wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR, ".placeholder-elipsis")))
        search_box.click()
        search_input = self.driver.find_element(By.CSS_SELECTOR, ".dark\\3Aplaceholder\\3Atext-wynk-gray1")
        search_input.send_keys("one love")
        first_result = self.wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR, ".flex:nth-child(4) .text-left:nth-child(1)")))
        first_result.click()

        time.sleep(30)
        # Continue with the rest of your test steps
