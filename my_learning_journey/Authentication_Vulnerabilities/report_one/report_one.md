# 2FA simple bypass

## Lab URL:
https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass

## Summary:
This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code.

## Steps to Reproduce:
1. Go to `My account`, then login with `carlos:montoya`.
2. Change the URL path from `/login2` to `/my-account?id=carlos`.
3. Visit the link, and the 2FA is bypassed successfully.

## Explanation:
-  This vulnerability occurs because the server does not properly enforce the second step of the two-factor authentication process.
- The authentication process goes through two steps
	- login with `username:password`.
	- Submitting the 2FA code.
- After that, the application redirects to the `/my-account?id=username` successfully when the 2FA code is submitted.
- So due to the bad implementation of the authentication process, the attacker can skip the second process of the authenication by changing the path from `/login2` to `/my-account?id=username`.

## Recommendation:
- Enforce 2FA step: The server must track whether a user has successfully completed the 2FA step before being sent to the next step or not.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_six.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_seven.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_eight.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/Authentication_Vulnerabilities/report_one/report_images/image_nine.png)



