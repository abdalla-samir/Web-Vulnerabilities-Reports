# CSRF vulnerability with no defenses

## Lab URL:
https://portswigger.net/web-security/csrf/lab-no-defenses

## Summary:
This lab's email change functionality is vulnerable to CSRF. 

## Steps to Reproduce:
1. Go to `My Account` page
2. Sign in using weiner:peter
3. Use `BurpSuite` to intercept the requests
4. In the email field, write the attacker's gmail -> `hacker@gmail.com`
5. Use `BurpSuite`to intercept the request and then send it to `Burp Repeater`
6. In `Burp Repeater`, 'right click' -> `Engagement Tools` -> `Generate CSRF PoC`
7. This will generate an HTML Code containing the malicious behaviour
8. Host the html file on your own server and send the link to the victim
9. Once the victim clicks the link, the request will be sent and the malicious behaviour will be executed


## Explanation:
-  This type of vulnerability allows the victim's browser to make a request configured by the attacker.
-  The request is configured by the attacker to perform a malicious behaviour which in this lab updating the victim's email
-  When the attacker sends the link to the victim and the victim clicks it, the victim's browser sends a request to the vulnerable website, as a result the email will be updated from victim's email to the attacker's gmail
-  The attacker now can take over the victim's account
-  Note: the victim must be logged in to the vulnerable website.

## Recommendation:
- Apply csrf token which prevent these types of attacks

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/CSRF/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/CSRF/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/CSRF/report_one/report_images/image_three.png)
