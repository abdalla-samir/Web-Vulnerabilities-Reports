# Basic SSRF against another back-end system

## Lab URL:
https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-backend-system

## Summary:
This lab has a stock check feature which fetches data from an internal system, so we can exploit this to gain access to internal server through the external one.

## Steps to Reproduce:
1. On the main page, go to any product and click `View details`
2. Click on `Check stock` and intercept the request using `BurpSuite`
3. Send the request to `Repeater`,then change the `stockApi` url to `http://192.168.0.178:8080/admin/delete?username=wiener`
4. Click `Send` and the account will be deleted


## Explanation:
- This type of vulnerability allows an attacker to access internal servers and systems and fetch sensitive data through a server-side request that the application makes on behalf of the user
- When `Check stock` is clicked, the application sends a request to the application's server
- `stockApi` parameter instructs the server send a request to the internal stock server to check the stock.
- An attacker can exploit this by writing the value of `stockApi` parameter with a common names of the server (e.g, `localhost` or `127.0.0.1`) to point to internal recource
- In this lab, we discovered the internal server IP is `192.168.0.178` on port `8080`, using Burp Intruder to fuzz the last octet.
- Once the valid IP was found, sending a request to `http://192.168.0.178:8080/admin` revealed the admin panel
- Click send and look for the response and it show us the admin panel, with user accounts
- Attacker now can delete users using the crafted URLs.

## Recommendation:
- Sanitize all user-controlled inputs that is used in server-side requests
- Implement allow-lists to restrict the domains, and just trust the in-list domains.

## Screenshots:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_six.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_seven.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/SSRF/report_one/report_images/image_eight.png)
