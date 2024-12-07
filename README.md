# Screenshot-at-various-Resolutions
To capture a screenshot of a webpage at various resolutions (including mobile to large screen monitors), you can use Selenium WebDriver with Python. Selenium allows you to control a web browser programmatically and capture screenshots of web pages at different screen sizes.

Here's how you can set up the script to capture screenshots at different resolutions:
Step 1: Install Dependencies

Ensure you have the necessary libraries installed. You will need:

    Selenium for web automation and capturing screenshots.
    WebDriver (e.g., ChromeDriver or GeckoDriver) to interact with browsers.

To install Selenium:

pip install selenium

Download the appropriate WebDriver for your browser:

    ChromeDriver: https://sites.google.com/a/chromium.org/chromedriver/downloads
    GeckoDriver (for Firefox): https://github.com/mozilla/geckodriver/releases

Step 2: Python Code for Capturing Screenshots at Various Resolutions

The script below will:

    Open the target webpage.
    Capture screenshots at different screen resolutions (e.g., mobile, tablet, desktop).
    Save each screenshot with the resolution as part of the filename.

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options
import time

# Initialize the WebDriver (Use Chrome for this example)
def init_driver():
    # Setup Chrome options (headless mode for non-interactive)
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    chrome_options.add_argument("--no-sandbox")
    chrome_options.add_argument("--disable-dev-shm-usage")
    
    # Create the driver object (adjust path to ChromeDriver)
    driver = webdriver.Chrome(executable_path='/path/to/chromedriver', options=chrome_options)
    return driver

# Capture screenshot at a specific resolution
def capture_screenshot(url, resolution, driver):
    # Set browser window size
    driver.set_window_size(resolution[0], resolution[1])
    
    # Open the webpage
    driver.get(url)
    
    # Wait for the page to load completely
    time.sleep(3)  # Adjust this time if needed
    
    # Save the screenshot with the resolution in the filename
    screenshot_filename = f"screenshot_{resolution[0]}x{resolution[1]}.png"
    driver.save_screenshot(screenshot_filename)
    print(f"Screenshot saved: {screenshot_filename}")

# Main function to capture screenshots at different resolutions
def capture_screenshots(url):
    driver = init_driver()
    
    # Resolutions to capture (mobile, tablet, desktop)
    resolutions = [
        (360, 640),  # Mobile (small screen)
        (768, 1280), # Tablet (medium screen)
        (1366, 768), # Small Desktop (standard laptop resolution)
        (1920, 1080), # Full HD Desktop (standard monitor resolution)
        (2560, 1440), # 2K resolution
        (3840, 2160)  # 4K resolution
    ]
    
    for resolution in resolutions:
        capture_screenshot(url, resolution, driver)
    
    # Close the driver after capturing all screenshots
    driver.quit()

# Example usage
url = "https://example.com"  # Change this to the webpage URL you want to capture
capture_screenshots(url)

Step 3: Explanation of Code

    init_driver: Initializes the Selenium WebDriver with Chrome, using headless mode to run without opening the browser window.
    capture_screenshot: Takes a screenshot after adjusting the window size to the given resolution.
    capture_screenshots: Defines multiple screen resolutions (from mobile to large monitor) and calls capture_screenshot for each resolution.
    time.sleep(3): Pauses the script for a few seconds to ensure the webpage is fully loaded before taking the screenshot.

Step 4: Resolution Sizes

Here are the common resolutions used for various devices:

    Mobile: (360, 640) (Small mobile devices).
    Tablet: (768, 1280) (Common tablet resolution).
    Laptop: (1366, 768) (Standard laptop resolution).
    Full HD: (1920, 1080) (Standard desktop monitor resolution).
    2K: (2560, 1440) (Higher resolution for modern monitors).
    4K: (3840, 2160) (Ultra-high resolution for large screens).

You can customize this list of resolutions based on the devices you want to target.
Step 5: Running the Script

    Download and set up the appropriate WebDriver (e.g., chromedriver for Chrome or geckodriver for Firefox).
    Replace '/path/to/chromedriver' with the path to your WebDriver executable.
    Replace "https://example.com" with the URL of the webpage you want to capture.
    Run the script, and it will save screenshots for each resolution in the working directory.

Conclusion

This Python script captures a webpage screenshot at various screen resolutions using Selenium. It handles mobile, tablet, and desktop resolutions, providing you with screenshots tailored to different screen sizes. You can adjust the resolutions as per your requirements and also add more if necessary.
