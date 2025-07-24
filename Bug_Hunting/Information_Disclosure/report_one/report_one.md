## Exposed Google Maps API Key, Firebase Key, and Other Sensitive Tokens on vayama.com

## Summary
During testing on `vayama.com` (part of the `trip.com` group), several sensitive API keys and tokens were identified being exposed within a publicly accessible JavaScript file. The exposed items include:
- **Google Maps API Key**
- **Matomo Analytics Token**
- **Generic API Secret**
- **Firebase API Key**

These keys and tokens were discovered hardcoded inside the following file: `https://***-***.vayama.com/***/***-*******.js`

## Steps To Reproduce

1. Visit the following URL (redacted for security):  `https://***-***.vayama.com/***/***-*******.js`  

2. Search for the following keywords individually:  
   - **VITE_GOOGLE_MAPS_API_KEY: "REDACTED_API_KEY"**  
   - **VITE_MATOMO_TOKEN: "REDACTED_MATOMO_TOKEN"**  
   - **VITE_API_KEYS_SECRET: "REDACTED_SECRET"**  
   - **VITE_FIREBASE_API_KEY: "REDACTED_FIREBASE_KEY"**  

3. The corresponding API keys and tokens will be visible hardcoded in the file.

## Impact
The exposure of these API keys and tokens introduces multiple risks:
- **Google Maps API Key**: Allows unauthorized Geocoding API usage, leading to potential billing abuse and information disclosure.
- **Matomo Analytics Token**: May allow unauthorized access to analytics data or manipulation of tracking configurations, depending on token permissions.
- **Generic API Secret**: May enable unauthorized access to backend APIs or services, depending on configuration.
- **Firebase API Key**: If not properly restricted, can be abused to access Firebase project resources.

Overall, this reflects a Security Misconfiguration and Information Disclosure, violating key management best practices.

## screenshot
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/Bug_Hunting/Information_Disclosure/report_one/report_images/image_one.png)


## Disclaimer
This report is shared as part of my portfolio to demonstrate my web security skills. No valid secrets or sensitive details are included. The vulnerability was responsibly reported to the `Trip.com` security team, who confirmed it had been previously submitted by another researcher.


