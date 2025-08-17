# 8x8 summary
We resolved an issue where a Google Maps API key allowed potential unauthorized access to some Google Maps services. While the API key was intentionally included in client-side code, it lacked proper restrictions to prevent abuse of paid services. The potential impact could theoretically lead to API quota consumption and related billing concerns, though actual impact was limited as no evidence of exploitation was found. Our team promptly validated and addressed the report by implementing appropriate API key restrictions where feasible, while accepting other known limitations.

# Summary
A Google Maps API key was discovered in a public-facing JavaScript request, accessible to any user without authentication. The key is valid and allows access to a wide range of paid APIs, including Directions, Distance Matrix, Elevation, Timezone, and Places Search APIs.
This kind of key exposure violates the principle of least privilege and allows attackers to abuse the key for unauthorized API usage, potentially incurring financial charges for the organization.

# Steps to reproduce
1- Visit the following URL: `https://(redecated)/index.js`

2- Search for the following pattern in the code: `key=${`

3- Copy the value of the exposed API key found in the JavaScript file.

4- Use the key to test multiple Google Maps API endpoints by replacing api_key in the URLs below:
```
https://maps.googleapis.com/maps/api/geocode/json?address=New+York&key=api_key

https://maps.googleapis.com/maps/api/directions/json?origin=New+York&destination=Boston&key=api_key

https://maps.googleapis.com/maps/api/distancematrix/json?origins=Seattle&destinations=San+Francisco&key=api_key

https://maps.googleapis.com/maps/api/elevation/json?locations=40.714224,-73.961452&key=api_key

https://maps.googleapis.com/maps/api/timezone/json?location=39.6034810,-119.6822510&timestamp=1331161200&key=api_key

https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=40.748817,-73.985428&radius=1500&type=restaurant&key=api_key

https://maps.googleapis.com/maps/api/place/textsearch/json?query=hotels+in+paris&key=api_key

https://maps.googleapis.com/maps/api/staticmap?center=New+York&zoom=13&size=600x300&maptype=roadmap&key=api_key

https://maps.googleapis.com/maps/api/streetview?size=600x300&location=40.720032,-73.988354&key=api_key
```
5- All the above endpoints return valid data, confirming that the exposed key grants access to multiple Google Maps APIs — including several paid services.

# impact
The exposed Google Maps API key grants unauthenticated access to multiple paid APIs, including Directions, Distance Matrix, Elevation, Timezone, Places, Static Maps, and Street View.

if the attacker found the key:

- Consume API quota or exceed free tier limits, leading to:
    - Unexpected billing charges to the organization’s Google Cloud account.
    - Service disruption if the key's usage quota is exhausted, affecting legitimate application users.
- Use the APIs for malicious automation, such as:
    - Mass geolocation lookups
    - Scraping business/location data from the Places API
    - Abuse of routing or time/distance queries
        
This exposure creates a financial risk and can result in reputational damage if abused at scale. Since no IP or referrer restrictions are enforced, anyone can exploit the key without authentication.

# Recommendation
Implement IP restriction when using GoogleMap API keys to prevent unauthorized access to this keys

# Screenshots
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/directions-api-valid-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/distance-matrix-api-valid-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/elevation-api-valid-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/geocoding-api-valid-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/staticmap-api-image-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/timezone-api-valid-response.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/report_one/report_images/streetview-api-image-response.png)
