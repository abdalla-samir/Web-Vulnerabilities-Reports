# Reflected XSS into a JavaScript string (HTML encoded angle brackets)

## Summary:
This lab demonstrates a reflected XSS vulnerability where the payload is reflected inside a JavaScript string, and angle brackets are HTML encoded.

## Steps to Reproduce:
1. In the search input, write the following payload: `'; alert() //`.

## Explanation:
- At first, we make initial test by writing the following input: `<'test'>`
- Click `Search` and write click then click `View Page Source`
- In the source code of the site, the input is reflected inside both `javascript variable` and `<h1>`
- The angle brackets (`<`, `>`) are HTML encoded, but single quotes are not encoded
- This allow us to write the payload `'; alert() //` in the `javascript variable` and it will be excuted successfully.


## Recommendation:
- User input should be sanitized so it prevents the attacker from injecting the payload.
- Prefer using frameworks that automatically handle context-aware encoding.

## Screenshots:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_one/report_one_images/report_one_image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_one/report_one_images/report_one_image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_one/report_one_images/report_one_image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_one/report_one_images/report_one_image_four.png)
