# User ID controlled by request parameter 

## Lab URL:
https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter

## Summary
This lab has a horizontal privilege escalation vulnerability on the user account page, in user `id` parameter.

## Steps to Reproduce
1. Go to `My account`, sign in using `wiener:peter`.
2. In the URL, change the value of `id` parameter from `wiener` to `carlos`.
3. Copy the `API Key` and submit the value.

## Explanation
- This vulnerability is a type of `Broken Access Control` which can lead to horizontal/vertical privilege escalation.
- After signing in, in the `my-account` page, we will notice that there is `id` parameter in the URL.
- The value of the id parameter represents the username.
- By changing the value of the `id` parameter, we can gain access to other users' accounts.
- In this lab, we were able to access Carlos's data and retrieve his `API key`.

## Recommendation
- Do not rely on user input alone to determine access rights.
- Always verify that the logged-in user is authorized to access the resource using session or token-based identifiers.

## Screenshot
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_one/report_images/image_three.png)

