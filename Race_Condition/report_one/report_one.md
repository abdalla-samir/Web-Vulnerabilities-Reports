# Limit overrun race conditions

## Lab URL:
https://portswigger.net/web-security/race-conditions/lab-race-conditions-limit-overrun

## Summary:
This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price. 

## Steps to Reproduce:
1. Go to `My account`, then sign in with the credentials `wiener:peter`.
2. On the main page, select the `Lightweight L33t Leather Jacket` and add it to the cart.
3. Enter `PROMO20` in the `Coupon` input field.
4. Click `Apply`, then Intercept the request using `BurpSuite` and send it to `Turbo Intruder`.
5. Use the `race-single-packet-attack.py` script and start the attack.
6. After the attack completes, go to the cart page and the now the jacket available for a significantly reduced price.

## Explanation:
- This type of vulnerabilities allows mutiple requests to be sent in parallel (at the same time).
- The misconfigured server will be confused and will processes all the requests that are sent in parallel by `Turbo Intruder`.
- As a result, the `coupon` code is applied multiple times, leading to a large discount.

## Recommendation:
- Make sure that the coupon can only be used once per cart by associating a "used" flag with the cart.
- Make sure that all coupon logic and total price calculations are validated on the server side, just before checkout.

## Screenshot:
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Race_Condition/report_one/report_images/image_six.png)
