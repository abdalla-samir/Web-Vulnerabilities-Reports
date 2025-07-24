# DOM XSS in innerHTML sink using source location.search

## Summary:
-This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an innerHTML assignment, which changes the HTML contents of a div element, using data from location.search. 


## Steps to Reproduce:
1. In the search bar, enter the following payload: `<img src=x onerror=alert(1)>`.
2. Click `search` and the code will be excuted.

## Explanation:
-  Application reflects user input in the page using `innerHTML`
-  The input is inserted into the JavaScript code, manipulated, and then displayed in the span tag that shows the results.
-  The type of XSS is `DOM-based XSS`
-  Since innerHTML parses the input as HTML, and no proper sanitization is applied, any HTML/JavaScript tags (e.g., `<img>` with an `onerror` event) will be executed.
-  We try to put raw HTML tags, and if they are not properly sanitized, they will be inserted into the span and executed.
-  Using the right payload (e.g. `<img src=x onerro=alert(1>`) will be inserted inside span tag and will be excuted immediateley

## Recommendation:
- User inputs should be sanitized before inserting the inputs into the DOM, this will prevent the injection of malicious payloads.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_three/report_three_images/report_three_image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_three/report_three_images/report_three_image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_three/report_three_images/report_three_image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/XSS/report_three/report_three_images/report_three_image_four.png)
