# ai-tester-learning
AI testing tasks using anti-hallucination protocols
Login Page Test Case Generation Using Anti-Hallucination Protocol

**PRD Used for All LLMs:**

**Application:** Login Page

**Features mentioned:**
1. User can enter username or email
2. User can enter password
3. User can click on Login button
4. System authenticates the user and logs them in

**LLMs Evaluated:**
1. LLaMA 3.2 (3B – local)
2. DeepSeek
3. QWEN3-MAX

**Task Description:**
As part of the AI Tester Blueprint task, I generated test cases for a generic login page using the Anti-Hallucination Protocol.
The same PRD was provided to all LLMs without any modification.
The PRD was intentionally kept generic and incomplete to evaluate how different LLMs behave when required to rely strictly on provided information and avoid assumptions.

**Observations:**

**LLaMA 3.2:**
- Correctly extracted verifiable facts and listed missing information.
- Generated test cases for invalid username and invalid password even though authentication failure behavior was not defined in the PRD.
- Self-check incorrectly reported no hallucination, indicating weak self-validation.

  
![LLaMA 3.2 Output Screenshot](https://github.com/user-attachments/assets/6a8e0bb5-f394-4ee3-ae87-ba433e9a6986)




**Let's start by extracting verifiable facts from the PRD:**

Verifiable Facts:
- User can enter username or email
- User can enter password
- User can click on Login button
- System authenticates the user and logs them in
   
**Missing/Clearly Unclear Information:**
- Password rules
- Error messages
- Account lockout
- CAPTCHA
- Rate limiting
- Forgot password flow
- Validation messages
- Security behavior
    
Now, let's generate test cases strictly from the verifiable facts:

**Test Case 1: Valid Login**

**Test Case ID:** TC_001

**Scenario:** User enters valid credentials and logs in successfully.

**Steps:**

1. Enter a valid username or email.
2. Enter a valid password.
3. Click on the Login button.
   
**Expected Result:** The system authenticates the user and logs them in successfully.

**Evidence Source:** PRD, Feature 4: System authenticates the user and logs them in

**Test Case 2: Invalid Username/Email**

**Test Case ID: TC_002**

**Scenario:** User enters an invalid username or email and clicks on Login button.

**Steps:**
1. Enter an invalid username or email.
2. Enter a valid password.
3. Click on the Login button.

**Expected Result:** The system does not authenticate the user and stays in the login page (Not specified in PRD).

**Evidence Source:** N/A

**Test Case 3: Invalid Password**

**Test Case ID:** TC_003

**Scenario:** User enters an invalid password and clicks on Login button.

**Steps:**

1. Enter a valid username or email.

2. Enter an invalid password.

3. Click on the Login button.

**Expected Result:** The system does not authenticate the user and stays in the login page (Not specified in PRD).

**Evidence Source:** N/A

**Self-check for hallucinations:** None found

**DeepSeek:**

- Demonstrated better structure and clearer separation between verified facts and missing details.

- Generated UI-level test cases correctly based on the PRD.

- Introduced subtle assumptions by generating authentication scenarios using valid credentials, which were not explicitly defined.

- Self-check did not flag this assumption.


<img width="1666" height="674" alt="SS_2deepseek" src="https://github.com/user-attachments/assets/fbafe123-28d4-411f-8991-d086de74a693" />


**Step 1: Extract only verifiable facts from PRD**

1. The page is a "Login Page."

2. There is a field where a user "can enter username or email." This is treated as a single entry field for a credential.

3. There is a field where a user "can enter password."

4. There is a "Login button" a user can click.

5. Upon clicking the login button, the "System authenticates the user and logs them in."

**Step 2: Identify missing or unclear information**

1. Unclear: The exact label or placeholder for the credential field is not specified (e.g., "Username or Email").

2. Missing: Behavior for empty credentials.

3. Missing: Behavior for incorrect credentials.

4. Missing: Behavior for correct credentials (specifics of "logs them in" - e.g., redirect URL, session creation).

5. Missing: Existence or behavior of a "Remember Me" checkbox.

6. Missing: Existence of a "Sign Up" or "Register" link.

7. Missing: Existence of a "Forgot Password" link.

8. Missing: Any UI/UX specifications (layout, colors, responsiveness).

9. Missing: Supported browsers or devices.

**Step 3 & 4: Generate test cases strictly from Step 1 and Self-check**

**TC-LOGIN-001**

**Scenario:** Verify the presence of all specified input fields and button on the Login Page.

**Steps:**

1. Navigate to the Login Page.

2. Observe the page.

**Expected Result:**

The page contains:

*   One input field for entering a username or email.

*   One input field for entering a password.

*   One clickable button labeled "Login".

**Evidence Source:** PRD Features 1, 2, 3.

**TC-LOGIN-002**

**Scenario:** Verify a user can enter text into the 'username or email' field.

**Steps:**

1. Navigate to the Login Page.

2. Click into the field intended for username/email.

3. Type a string (e.g., "test_user" or "user@example.com").

**Expected Result:**

The typed characters appear in the field.

**Evidence Source:** PRD Feature 1.

**TC-LOGIN-003**

**Scenario:** Verify a user can enter text into the 'password' field.

**Steps:**

1. Navigate to the Login Page.

2. Click into the field intended for the password.

3. Type a string (e.g., "mypass123").

**Expected Result:**

The typed characters appear in the field (visibility masked or not is not specified).

**Evidence Source:** PRD Feature 2.

**TC-LOGIN-004**

S**cenario:** Verify the Login button is clickable.

**Steps:**

1. Navigate to the Login Page.

2. Click on the Login button.

**Expected Result:**

The button registers the click event (the system proceeds with its authentication action, even if no credentials are provided).

**Evidence Source:** PRD Feature 3.

**TC-LOGIN-005**

**Scenario:** Verify system attempts authentication when Login is clicked with entered credentials.

**Steps:**

1. Navigate to the Login Page.

2. Enter a valid username/email into the first field.

3. Enter the corresponding valid password into the second field.

4. Click the Login button.

**Expected Result:**

The system processes the entered credentials for authentication. The specific result of successful login (e.g., page redirect) is Not specified in PRD.

Evidence Source: PRD Feature 4. (Note: PRD does not define "valid," so this test assumes the existence of a known valid account. The expected result is limited to the system attempting the action).

**QWEN3-MAX:**

- Showed the strongest adherence to the anti-hallucination rules.

- Generated test cases strictly from explicitly stated PRD features.

- Avoided assumptions related to validations, error handling, security mechanisms, and UI behavior.

- Self-check clearly documented excluded assumptions and maintained consistency.

- Only minimal and debatable assumptions were observed around credential validity, without adding unsupported behavior.

  


<img width="1042" height="721" alt="SS_1Qwen-Max" 
src="https://github.com/user-attachments/assets/636926be-b0c8-4ea2-98a1-63ccb6e615ca" />



**Test Case ID: LOGIN_UI_01**  

**Scenario:** Verify presence of username/email input field  

**Steps:**  

1. Navigate to the login page.  

**Expected Result:** Username/email input field is present on the page.  

**Evidence Source:** PRD feature 1 ("User can enter username or email")  

**Test Case ID:** LOGIN_UI_02  

**Scenario:** Verify username/email field accepts input  

**Steps:**  

1. Navigate to the login page.  

2. Enter text into the username/email field.  

**Expected Result:** Input field accepts and registers the entered text.  

**Evidence Source:** PRD feature 1 ("User can enter username or email")  

**Test Case ID:** LOGIN_UI_03  

**Scenario:** Verify presence of password input field  

**Steps:**  

1. Navigate to the login page.  

**Expected Result:** Password input field is present on the page.  

**Evidence Source:** PRD feature 2 ("User can enter password")  

**Test Case ID:** LOGIN_UI_04  

**Scenario:** Verify password field accepts input  

**Steps:**  

1. Navigate to the login page.  

2. Enter text into the password field.  

**Expected Result:** Input field accepts and registers the entered text.  

**Evidence Source:** PRD feature 2 ("User can enter password")  

**Test Case ID:** LOGIN_UI_05  

**Scenario:** Verify presence of Login button  

**Steps:**  

1. Navigate to the login page.  

**Expected Result:** Login button is present on the page.  

**Evidence Source:** PRD feature 3 ("User can click on Login button")  

**Test Case ID:** LOGIN_FUNC_01  

**Scenario:** Successful authentication flow using valid credentials (username format)  

**Steps:**  

1. Navigate to the login page.  

2. Enter a valid username in the username/email field.  

3. Enter the corresponding valid password.  

4. Click the Login button.  

**Expected Result:** System authenticates the user and logs them in.  

**Evidence Source:** PRD feature 4 ("System authenticates the user and logs them in")  

**Test Case ID:** LOGIN_FUNC_02  

**Scenario:** Successful authentication flow using valid credentials (email format)  

**Steps:**  

1. Navigate to the login page.  

2. Enter a valid email in the username/email field.  

3. Enter the corresponding valid password.  

4. Click the Login button.  

**Expected Result:** System authenticates the user and logs them in.  

**Evidence Source:** PRD feature 4 ("System authenticates the user and logs them in")  

**Self-Check Verification ** 

✅ All test cases derived only from explicit PRD features (1–4).  

✅ Zero assumptions about:  

   - Credential format/validation (e.g., "valid" refers only to system-recognized credentials implied by authentication capability)  

   - Post-login behavior (redirection, session, UI changes)  

   - Field masking, placeholders, labels, or visual states  

   - Button enabled/disabled states  

   - Error handling, messages, or failure flows  

   - Security mechanisms (CAPTCHA, rate limits, etc.)  

✅ "Valid credentials" phrasing strictly reflects PRD feature 4’s authentication capability without inventing examples or rules.  

✅ All "Not Mentioned" items (password rules, errors, lockout, etc.) intentionally excluded.  

✅ No UI details (colors, positions, icons) added beyond presence/functionality explicitly stated in PRD.


Conclusion:

This exercise demonstrated that different LLMs follow anti-hallucination rules with varying levels of discipline.

While QWEN3-MAX showed the highest compliance, all models still required human QA review to detect assumptions and prevent hallucinated test cases.

Key Learning:

- Better models hallucinate less, but none hallucinate zero.

- Anti-hallucination protocols are effective only when outputs are reviewed critically.

- AI testing requires evaluating model behavior, not just generated test cases.

 #AI Tester   #Task 🚀 Task #1 | Research about the Foundation Model 

