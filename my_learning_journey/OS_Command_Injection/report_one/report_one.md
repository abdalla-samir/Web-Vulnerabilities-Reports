# Blind OS command injection with time delays

## Lab URL:
https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays

## Summary:
This lab contains a blind OS command injection vulnerability in the feedback function.

## Steps to Reproduce:
1. On the main page, Click on `Submit feedback`.
2. On the feedback page, enter a testing value in each field.
3. Click `Submit feedback` and intercept the request using `BurpSuite`.
4. Send the request to `Burp Repeater`.
5. Change the value of the email to `%26ping%20-c%2010%20127.0.0.1%26`.
6. Send the request and you will notice that the response was delayed for about ten seconds, this means that the injected command `ping%20-c%2010%20127.0.0.1` executed successfully.

## Explanation:
- This type of vulnerability allows an attacker to execute OS commands on the server that is running an application.
- In this lab if we injected normal command it will not appear in the response.
- But that doesn't mean that the application isn't vulnerable.
- We can use other techniques that allow us to detect if it is Blind or not, like injecting command to trigger a time delay like `ping` command. 
- So we can use a command like this `ping -c 10 127.0.0.1` to see if the response will be delayed for ten seconds or will display the response without any delay.
- By encoding the payload, it becomes ping%20-c%2010%20127.0.0.1`.
- We should use `shell metacharacters` before and after the command to separate the command `ping -c 10 127.0.0.1` from other commands that will be sent to the server.
- We can use `&` character to make this function, which by encoding will convert into `%26`.
- So the full command will be `%26ping%20-c%2010%20127.0.0.1%26`.
- This cause the response to be delayed for ten seconds, which indicates that there is a `Blind OS command injection Vulnerability`.

## Recommendation:
- Validating that the input should only be numbers.
- Validating that the input should be alphanumeric, no other syntax.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/OS_Command_Injection/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/OS_Command_Injection/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/OS_Command_Injection/report_one/report_images/image_three.png)

