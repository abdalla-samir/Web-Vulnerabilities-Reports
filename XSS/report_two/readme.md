# Stored XSS into anchor href attribute with double quotes HTML-encoded

## Lab URL:
https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded

## Summary:
This lab contains a stored cross-site scripting vulnerability in the comment functionality.

## Steps to Reproduce:
1. Go to any post in the page.
2. Scroll down to the comment section.
3. In `Website` input field, write the following payload: `javascript:alert(document.cookie)`.
4. Submit the comment
4. The payload will excute when any user clicks on the link associated with the comment.

## Explanation:
- First, identify all possible entry points that might be vulnerable to `Stored XSS`  
- Go to any post, and in the comment section, perform an initial test by writing generic values in all input fields.
- In `View Page Source`, observe the reflection points, which are inside the `<p>` and `<a>` tags, specifically in the `href` attribute. 
- You will notice that characters such as `'`, `"`, `<`, and `>` are encoded in both `<p>` and `<a>` so injecting payloads in those tags will not affect.
- However, the `href` attribute does not require a protocol like `http` or `https`, and therefore accepts a `javascript:` scheme.
- This allow us to inject the following payload: `javascript:alert(document.cookie)`.
- Once the link is clicked, the payload executes.

## Recommendation:
- Prevent dangerous URL schemes such as `javascript:` and only allow schemes like `http`, `https`.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_two/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_two/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_two/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_two/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/XSS/report_two/report_images/image_five.png)


