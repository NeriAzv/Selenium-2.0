Element Manipulation
====================

The ``Elements`` class provides an intuitive and powerful way to manipulate web elements, significantly simplifying Selenium's native complexity. Below are comparisons showing the "before" (native Selenium) vs "after" (SeleniumTwo) for each function.

Finding Elements with Wait
--------------------------

**Before (Native Selenium)**:

.. code-block:: python

   from selenium.webdriver.common.by import By
   from selenium.webdriver.support.ui import WebDriverWait
   from selenium.webdriver.support import expected_conditions as EC
   
   # Complex and verbose
   try:
       element = WebDriverWait(driver, 10).until(
           EC.presence_of_element_located((By.XPATH, "//button[@id='submit']"))
       )
   except TimeoutException:
       print("Element not found")
   # Need to repeat this pattern for every element

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import find_element_with_wait
   
   # Simple one-liner
   element = find_element_with_wait("xpath", "//button[@id='submit']", timeout=10)

Waiting for Clickable Elements
------------------------------

**Before (Native Selenium)**:

.. code-block:: python

   from selenium.webdriver.support.ui import WebDriverWait
   from selenium.webdriver.support import expected_conditions as EC
   
   # Manual exception handling required
   try:
       element = WebDriverWait(driver, 10).until(
           EC.element_to_be_clickable((By.ID, "my-button"))
       )
       element.click()
   except ElementClickInterceptedException:
       # Handle interception manually
       driver.execute_script("arguments[0].click();", element)

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import wait_for_element_be_clickable
   
   # Automatic interception handling
   element = wait_for_element_be_clickable("id", "my-button", timeout=10)
   # Clicks automatically without interception issues

Intelligent Waiting System
--------------------------

**Before (Native Selenium)**:

.. code-block:: python

   import time
   from selenium.common.exceptions import NoSuchElementException
   
   # Manual polling with complex logic
   def wait_for_element(by, value, timeout=10):
       start_time = time.time()
       while time.time() - start_time < timeout:
           try:
               element = driver.find_element(by, value)
               if element.is_displayed():
                   return element
           except NoSuchElementException:
               pass
           time.sleep(0.5)
       raise NoSuchElementException(f"Element {value} not found")
   
   # Limited to element types only
   element = wait_for_element(By.XPATH, "//div[@class='loading']")

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import wait_for_element_appear, wait_for_element_disappear
   
   # Works with multiple object types
   element = wait_for_element_appear("//div[@class='success']", "elemento")
   text_found = wait_for_element_appear("Operation Completed", "texto")
   image_found = wait_for_element_appear("C:\\path\\image.png", "imagem")
   
   # Also supports waiting for disappearance
   wait_for_element_disappear("//div[@class='loading']", "elemento")

Smart Dropdown Selection
------------------------

**Before (Native Selenium)**:

.. code-block:: python

   from selenium.webdriver.support.ui import Select
   
   # Multiple steps for simple selection
   select_element = driver.find_element(By.ID, "country-select")
   select = Select(select_element)
   
   # Limited to exact matches
   select.select_by_visible_text("United States")
   # OR
   select.select_by_value("US")
   # OR  
   select.select_by_index(1)
   
   # No fuzzy matching or language variations

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import Select_element
   
   # Single function with multiple selection methods
   select_elm = find_element_with_wait("id", "country-select")
   
   # Multiple selection methods with language variations
   Select_element_func(select_element, "texto", "Estados Unidos")  # Portuguese
   Select_element_func(select_element, "value", "US")              # By value
   Select_element_func(select_element, "índice", 1)                # By index
   
   # Supports relative/fuzzy matching
   Select_element_func(select_element, "text", "United", relative=True)

Popup Handling
--------------

**Before (Native Selenium)**:

.. code-block:: python

   import time
   
   # Complex alert handling with manual waiting
   def handle_alert(timeout=10):
       for _ in range(timeout):
           try:
               alert = driver.switch_to.alert
               text = alert.text
               alert.accept()
               return text
           except:
               time.sleep(1)
       return None
   
   alert_text = handle_alert()

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import pop_up_extract
   
   # Simple one-liner with extraction and auto-accept
   alert_text = pop_up_extract(text=True, accept=True, timeout=10)

Mouse Movement Automation
-------------------------

**Before (Native Selenium)**:

.. code-block:: python

   from selenium.webdriver.common.action_chains import ActionChains
   
   # Basic movement without realism
   element = driver.find_element(By.ID, "button")
   actions = ActionChains(driver)
   actions.move_to_element(element).click().perform()
   
   # No smooth movement or human-like behavior

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import move_mouse_smoothly
   
   element = find_element_with_wait("id", "button")
   
   # Human-like smooth movement with optional click
   move_mouse_smoothly(element, click=True)
   
   # Configurable movement parameters
   move_mouse_smoothly(element, click=True, x_adittional=50, y_adittional=30)

Image-Based Interaction
-----------------------

**Before (Native Selenium)**:

.. code-block:: python

   # Selenium has no native image recognition
   # Requires additional libraries and complex setup
   import pyautogui
   import time
   
   # Manual image finding with error handling
   def click_image(image_path, timeout=10):
       for _ in range(timeout):
           try:
               location = pyautogui.locateOnScreen(image_path, confidence=0.8)
               if location:
                   center = pyautogui.center(location)
                   pyautogui.click(center)
                   return True
           except:
               time.sleep(1)
       return False

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import Elements
   
   elements = Elements(driver)
   
   # Built-in image recognition with multiple features
   elements.move_to_image(
       "C:\\path\\button.png",
       click_on_final=True,
       trail=True,           # Smooth movement to image
       tolerancia=0.8,       # Confidence level
       timeout=30,
       verify=False,
       repeat=False
   )

Multiple Elements Finding
-------------------------

**Before (Native Selenium)**:

.. code-block:: python

   from selenium.webdriver.support.ui import WebDriverWait
   from selenium.webdriver.support import expected_conditions as EC
   
   # Verbose syntax for multiple elements
   try:
       elements = WebDriverWait(driver, 10).until(
           EC.presence_of_all_elements_located((By.CLASS_NAME, "item"))
       )
   except TimeoutException:
       elements = []

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import find_elements_with_wait
   
   # Clean one-liner
   elements = find_elements_with_wait("class", "item", timeout=10)

Console Script Execution
------------------------

**Before (Native Selenium)**:

.. code-block:: python

   import time
   
   # Manual retry logic for script execution
   def execute_script_with_retry(script, timeout=10):
       start_time = time.time()
       while time.time() - start_time < timeout:
           try:
               driver.execute_script(script)
               return True
           except Exception:
               time.sleep(1)
       return False

**After (SeleniumTwo)**:

.. code-block:: python

   from SeleniumTwo import Elements
   
   elements = Elements(driver)
   
   # Built-in retry mechanism
   elements.script_console_with_wait(
       "console.log('Script executed')",
       timeout=10
   )

Key Advantages Summary
----------------------

- **Reduced Code**: 70-80% less code compared to native Selenium
- **Automatic Error Handling**: Built-in retry mechanisms and exception management
- **Multi-language Support**: Functions understand both Portuguese and English terms
- **Human-like Interactions**: Smooth mouse movements and realistic timing
- **Multiple Object Types**: Support for elements, text, images, and windows
- **Intelligent Waiting**: Smart detection of appearance/disappearance
- **Easy Configuration**: Simple parameters replace complex Selenium configurations

Example Workflow Comparison
---------------------------

**Before (Complex Selenium)**:

.. code-block:: python

   # Complex workflow with multiple try/except blocks
   try:
       WebDriverWait(driver, 10).until(
           EC.presence_of_element_located((By.ID, "form"))
       )
       select = Select(driver.find_element(By.ID, "country"))
       select.select_by_value("BR")
       driver.find_element(By.ID, "submit").click()
       WebDriverWait(driver, 10).until(
           EC.alert_is_present()
       )
       alert = driver.switch_to.alert
       alert.accept()
   except Exception as e:
       print(f"Error: {e}")

**After (Simple SeleniumTwo)**:

.. code-block:: python

   # Clean, readable workflow
   form = find_element_with_wait("id", "form")
   nr_library(form, "value", "BR")
   wait_for_element_be_clickable("id", "submit")
   pop_up_extract(accept=True)

The SeleniumTwo library transforms complex Selenium operations into simple, intuitive function calls while maintaining full functionality and adding advanced features not available in native Selenium.