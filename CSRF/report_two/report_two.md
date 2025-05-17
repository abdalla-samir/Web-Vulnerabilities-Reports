# CSRF where Referer validation depends on header being present.

## Lab URL:
https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-depends-on-header-being-present

## Summary:
This lab's email change functionality is vulnerable to CSRF. It attempts to block cross domain requests but has an insecure fallback, it validate the referer based on it's present, which means if the referer is absent the request will be accepted.

## Steps to Reproduce:
1. Go to the `My Account page`.
2. Enter the attacker's email (e.g., `hacker@gmail.com`) and Use `BurpSuite` to intercept the request before sending it.
3. Click `Update email` intercept the request in the `BurpSuite`.
4. Send the request to `Repeater`.
5. In `Repeater`, do the following: 'right click' -> `Engagement Tools` -> `Generate CSRF PoC`.
6. add the following tag inside the `<head>` tag of the generated HTML: `<meta name="referrer" content="no-referrer">`.
7. Copy The Code and host it on your own server (in this lab, use the PortSwigger exploit server).
8. Send the link to the victim.
9. when the victim visit the site, the malicious behaviour will be excuted, and the victim's email will be changed to the attacker's email.

## Explanation:
- This type of vulnerability allows the victim's browser to make a request configured by the attacker.
- Normally, the request would be rejected because the server validates the `referer`header.
- But the server only validated the referer if it is present.
- This means that if the referer is removed, the request will be accepted by the server.
- So when the `CSRF PoC` generated, the following tag will be added in the `<head>` tag: `<meta name="referrer" content="no-referrer">`.
- This tag will remove the referer from the request header, as a result the validation is bypassed and the attack successed.

## Recommendation:
- Apply strict validation of the Referer.
- CSRF tokens must be included in the requests.
- Apply SameSite cookies like `SameSite=Lax` or `SameSite=strict` to limit cross-site request risks.


## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/CSRF/report_two/report_images/image_one.png).
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/CSRF/report_two/report_images/image_two.png).
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/CSRF/report_two/report_images/image_three.png).
