# Basic password reset poisoning

## Lab URL:
https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-basic-password-reset-poisoning

## Summary:
This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives.

## Steps to Reproduce:
1. Go to `My account` and then click `Forgor password?`.
2. Enter the username `carlos` in the input field.
3. Click `submit` and intercept the request using `BurpSuite`.
4. Send the intercepted request to `Burp Repeater`.
5. In the request, modify the Host: header to use your exploit server's domain.
6. Click `Send`, then go to the `Access log` in the exploit server.
7. Search for the victim password reset token.
8. Write the following URL `https://LAB-ID.web-security-academy.net/forgot-password?temp-forgot-password-token=token_value` in the search bar and now you can change the password of the victim -> `carlos`.

## Explanation:
- This type of vulnerabilities allow the hacker to inject his exploiting website inside the forget password request in the `Host: ` request header.
- The hacker modifies the Host header to point to their own server.
- When the victim clicks the link the victim token is leaked via exploit server logs.
- once the token passed to the hacker, the hacker now can use this token to change the password.

## Recommendation:
- Validate host headers strictly.
- Only allow known, whitelisted `Host` headers, and reject any other `Host` values.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_six.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/HTTP_Host_header_attacks/report_one/report_images/image_seven.png)


