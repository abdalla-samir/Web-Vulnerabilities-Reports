# User role controlled by request parameter

## Lab URL:
https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter

## Summary:
This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie. 

## Steps to Reproduce:
1. In the main page, enter the path `/admin` and intercept the request using `Burpsuite`.
2. Send the request to `Burp Repeater`.
3. Change the path to `/admin/delete?username=carlos` and modify the `Admin` cookie value from `false` to `true`.
4. Send the modified request to delete the user.

## Explanation:
- The request contains a session cookie with an `Admin:` flag, which indicates administrative privileges and it's value is `false`.
- This vulnerability allows verticle privilege escalation by changing the value of `Admin:` from `false` to `true`.
- After modifying the value, we gained access to the admin panel, which allowed us to delete any user on the application.
- With admin privileges, Sending a request to `/admin/delete?username=carlos` will delete the account.

## Recommendation:
- Use secure session management, where user roles and privileges are stored securely on the server and are not modifiable by the client.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_two/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_two/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_two/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_two/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/IDOR/report_two/report_images/image_five.png)


