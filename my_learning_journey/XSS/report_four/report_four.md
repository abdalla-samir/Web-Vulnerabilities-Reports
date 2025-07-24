# Reflected XSS into a JavaScript string with single quote and backslash escaped

## Lab URL:
https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped

## Summary:
This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped.

## Steps to Reproduce:
1. Go to the Search bar and enter the following payload: `</script> <svg onload=alert(1)>`
2. Click `Search` and an alert box will appear

## Explanation:
- First, we perform an initial test to see where the user input is reflected. For examble enter the following payload: `<\'test\'>`.
- When we view the page source we find that the input is reflected in both `<h1>` tag and inside the javascript code.
- We notice that in `<h1>` tag, angle brackets are encoded. but in the javascript code, they are not.
- This allow us to inject `</script>` to break the current `<script>` tag and insert a new HTML tag
- So the final payload is: `</script><svg onload=alert(1)>`.
- This successfully closes the `<script>` tag and trigger the XSS by injecting a new tag into HTML code.

## Recommendations:
- Sanitize and encode user inputs before reflecting it into the page.
- Avoid reflecting user input into the javascript code directly without strict validation.

## Screenshots:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_four/report_images/image_six.png)

