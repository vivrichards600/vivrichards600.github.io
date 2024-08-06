---
layout: post
title: Unlocking the Potential of ChatGPT for Software Testing with C.L.E.A.R Prompts
description:
headline:
modified: 2024-08-06
category: AI
tags: [AI, Software Testing, Tools, ChatGpt, Prompts]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

As a software tester, I'm always on the lookout for new tools and methods to enhance my testing processes. [I’ve been using ChatGPT on and off](https://vivrichards.co.uk/ai/using-chatgpt-to-assist-testing) for a while and found it really useful for generating test ideas for both static and dynamic testing. Recently, I stumbled upon [an AI-Assisted Testing video featuring Mark Winteringham](https://youtu.be/ozqffT6ZF24?feature=shared), where he demonstrated how to use ChatGPT more effectively by crafting better prompts.

## C.L.E.A.R  

Inspired by his approach, I began experimenting with different ways to structure my prompts and eventually came up with the C.L.E.A.R acronym, which stands for Context, Lead Instructions, Examples, Assumptions, and Review. This method has proven so far to be a useful way to structure prompts, ensuring that ChatGPT provides more relevant and useful responses.

It's worth noting though, using C.L.E.A.R is still something I’m experimenting with. I wanted to write and share this approach to see if it was useful for others but also to get feedback and iterate on the idea to make using ChatGPT more useful to assist people.

Here's a breakdown of the C.L.E.A.R approach and why it might be a good idea to start using it when generating test ideas with ChatGPT:

## C - Context
Providing context helps ChatGPT understand the background and the role it needs to assume. For example:

Prompt without context:
> "Write automation code for the contact form."

Prompt with context:
> "As a test automation engineer, write Selenium Page Object Model code for the contact form."

## L - Lead Instructions
Clear instructions guide ChatGPT to perform the specific action you need, avoiding ambiguous responses.

Prompt without lead instructions:
> "Write a script for the contact form."

Prompt with lead instructions:
> "Write a Selenium WebDriver script to automate the contact form."

## E - Examples
Including examples guides ChatGPT in understanding the format and level of detail expected.

Prompt without examples:
> "Create a test script for the form on website example.com/contact"

Prompt with examples:
> "Create a Selenium WebDriver script to automate the contact form. Refer to the example format delimited by three back quotes:
> ``````
> ```
> driver.find_element_by_id('name').send_keys('John Doe')driver.
> find_element_by_id('email').send_keys('john.doe@example.com')
> driver.find_element_by_id('message').send_keys('This is a test message.')
> driver.find_element_by_xpath('//button[@type="submit"]').click()```
> ```

## A - Assumptions
Stating assumptions clarifies any underlying details that might not be immediately obvious, ensuring that ChatGPT’s response aligns with your needs.

Prompt without assumptions:
> "Write a script to fill out the form."

Prompt with assumptions:
> "Assume the form has standard HTML5 input types and include error handling in the script."

## R - Review
Requesting a review prompts ChatGPT to include validation steps or checks to ensure the output meets your requirements.

Prompt without review:
> "Write a script to submit the form."

Prompt with review:
> "Write a script to submit the form and include validation to check for successful submission."

## Example Comparison
### Without Using CLEAR
Prompt:
> "Write automation code for this contact form."
> ``````
> driver.find_element_by_id('name').send_keys('John Doe')driver.
> find_element_by_id('email').send_keys('john.doe@example.com')
> driver.find_element_by_id('message').send_keys('This is a test message.')
> driver.find_element_by_xpath('//button[@type="submit"]').click()```

Response:
> ``````
> from selenium import webdriver
> driver = webdriver.Chrome()
> driver.get('URL_OF_THE_PAGE_WITH_FORM')
>
> driver.find_element_by_id('name').send_keys('John Doe')
> driver.find_element_by_id('email').send_keys('john.doe@example.com')
> driver.find_element_by_id('message').send_keys('This is a test message.')
> driver.find_element_by_xpath('//button[@type="submit"]').click()
>
> driver.quit()

### Using CLEAR
Prompt:
>"As a test automation engineer, write a Selenium WebDriver script to automate the contact form using the following HTML snippet delimited by three back quotes. Assume the form requires standard HTML5 input handling and that you need to include methods for interacting with the form elements as well as validation for successful submission. Review the script to ensure it correctly interacts with the form and checks for submission success."

> ``````
> <form id="contact-form">
>     <label for="name">Name:</label>
>     <input type="text" id="name" name="name" required>
>
>     <label for="email">Email:</label>
>     <input type="email" id="email" name="email" required>
>
>     <label for="message">Message:</label>
>     <textarea id="message" name="message" required></textarea>
>
>     <button type="submit">Submit</button>
> </form>

Response:
> ``````
> from selenium.webdriver.common.by import By
> from selenium.webdriver.support.ui import WebDriverWait
> from selenium.webdriver.support import expected_conditions as EC
>
> class ContactFormPage:
> def __init__(self, driver):
> self.driver = driver
> self.wait = WebDriverWait(driver, 10)
> self.name_field = (By.ID, 'name')
> self.email_field = (By.ID, 'email')
> self.message_field = (By.ID, 'message')
> self.submit_button = (By.XPATH, '//button[@type="submit"]')
> self.success_message = (By.ID, 'success-message')  # Adjust based on > actual success message
>
>     def enter_name(self, name):
>         element = self.wait.until(EC.visibility_of_element_located(self.name_field))
>         element.send_keys(name)
>
>     def enter_email(self, email):
>         element = self.wait.until(EC.visibility_of_element_located(self.email_field))
>         element.send_keys(email)
>
>     def enter_message(self, message):
>         element = self.wait.until(EC.visibility_of_element_located(self.message_field))
>         element.send_keys(message)
>
>     def submit_form(self):
>         element = self.wait.until(EC.element_to_be_clickable(self.submit_button))
>         element.click()
>
>     def verify_success(self):
>         success_element = self.wait.until(EC.visibility_of_element_located(self.success_message))
>         assert success_element.is_displayed(), "Form submission failed."

The C.L.E.A.R approach has so far proven to be really useful for me, but it's not something that will just work for anyone. You need to evaluate, iterate, and refine your prompts based on the responses you get back. This isn't a one-size-fits-all method where following C.L.E.A.R guarantees the exact response you want. Also, the output from ChatGPT can be really useful to assist you, not to replace your expertise.

Any tool without proper knowledge can be a hindrance. For example, while generating an automation script with ChatGPT might seem great, you still need the knowledge of what has been generated, including boilerplate code, how to refactor for re-use, and maintainability etc.

I encourage you to give the C.L.E.A.R approach a try and see how it can enhance your use of ChatGPT for generating test ideas, automation scripts, and more. Feel free to share your experiences and any improvements you discover along the way!

Happy testing!
