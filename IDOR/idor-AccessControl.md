# IDOR ~ Insecure Direct Object References
IDOR happens when an application uses user input to access objects directly. This vulnerability can lead to unauthorized access, exposing sensitive data like personal details, financial information, or private messages. It's like accidentally getting a key to someone else's house!

### IDOR Violation:
Specifically targeting some type of identifier (like ID) that is used to pull a larger subset of data including sensitive data from the database. In many cases, a general user is able to see other user's information. Testing for IDOR requires two separate accounts with the same role.

# AC ~ Access Control
Access control ensures that users can only interact with the parts of an application they're permitted to. When testing for IDOR, you usually need two separate accounts with the same role to compare what each user can access. For access control bypass, it's about seeing if one account can see or do things it's not supposed to. Testing for AC bypass requires two or more separate accounts with different roles.

### AC Violation:
Access control violation happens if a user with a role other than admin is able to use the admin mechanisms/privileges to access admin dashboard and view sensitive user data. An example to AC violation is finding a way to bypass 403 HTTP response from the web application, meaning that the server understands the request but refuses to authorize it, so we manage to bypass it. <br>
1. Identify granular roles within an instance of a web application.
2. Enumerate mechanisms that a role should not have the ability to execute certain tasks.
3. Determine how that mechanism is actually executed with HTTP requests.
4. Execute the mechanisms the role should not be able to execute.


## Main Methodology
Find a complex application. Complex applications will have lots of endpoints and many different places to look for vulnerabilities. Make sure the application you're testing has some different roles, such as normal user, admin, audit role, and others. <br><br>
Try to identify ways to understand how the user data is displayed. Is it coming from the backend or some sort of API call is happening, or is there any other way? Then, understand how authentication and authorization is made within the application to understand how the website know that you are who you say you are. <br> <br>
If you are a beginner bug bounty hunter, you should choose programs that pay less than others. The ones that pay a lot of money for bugs are usually being tested by other experienced hunters, but the ones that pay lower aren't often tested as much as higher payout ones. 


## Questions to ask when approaching to the application
1. Role Validation: How is the application validating the role?
2. User Identification: How is the application identifying the user?
3. Permission Check: How is the application identifying what role is trying to perfom the operation, and should they be allowed to do that certain operation?

> [!TIP]
> `Create sections such as pointers and mechanisms.` **Pointers**: identify other point of areas that would lead to other types of attacks (it's not just about finding another vulnerability, but taking notes of the important indications of possible points of entry)<br><br>**Mechanisms**: try to identify CRUD mechanisms (create, read, update, delete). It's good to breakdown each mechanism to its HTTP methods and see what they do in the application so that you can understand the whole picture better and refer back to your notes if you're lost.

> [!TIP]
> `Obtain the objects.` Object is the response returning back from the response, like the objects returned with JSON (e.g. userId, objectId, date, email...) With the obtained objects, try to send requests with different user identifiers to see if any object violates the access control.<br><br>`Create multiple accounts.` + (plus notation) is a way to create multiple account under the same email, such as user@hackerone.com, user+admin@hackerone.com, user+developer@hackerone.com, and so on.  


### Things To Bear In Mind When Doing Bug Bounty
**Scope Awareness:** Be very careful with the scope of the application. If you're testing a website and the payment mechanism redirects you to a different domain, be aware of the domain change (it could redirect to a whole different application, especially for payment mechamisms).



<!--
##### THINGS TO LOOK UP
Learn what is DOM and how it is being used in the web context
What does it mean if a JWT token or any kind of token being used and validated, being used and not validated?
Learn what is the importance of CSRF cookie, what does it do, what is CSRF? 
-->