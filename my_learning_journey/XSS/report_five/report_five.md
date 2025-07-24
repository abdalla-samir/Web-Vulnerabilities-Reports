# DOM XSS in `document.write` sink using source `location.search`

## Lab URL
https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink

## Summary:
This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search, which you can control using the website URL. 

## Steps to Reproduce:
1. In the search bar, enter the following payload: `"><script>alert(1)</script>');//`.
2. Click `search`, an alert will popup.

## Explanation:
- First, enter any initial value in the search bar and click `search`.
- `Right Click` -> `View Page Source`.
- The page source code contains javascript codes that deals with HTML -> `DOM`
- The JS code take the input from search bar and include it in `document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');`.
- So, we can use `">` to close the `img` tag and then inject `<script>alert(1)</script>` and finally close the `document.write` with `');`.
- This will inject both `<img>` and `<script>` tags inside HTML, and then the browser will execute the code inside the `<script>` tag.

## Recommendation:
- Avoid using document.write() to dynamically insert untrusted data into the DOM.
- Sanitize and validate any data from location.search or other URL-based sources before rendering.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_five/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_five/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_five/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_five/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_five/report_images/image_five.png)

