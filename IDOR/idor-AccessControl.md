# IDOR ~ Insecure Direct Object References
Use another unique identifier to access a data set that the attacker should not have access to 

### IDOR Violation:
Specifically targeting some type of identifies (like ID) that is used to pull a larger subset of data including sensitive data from the database. 
In many cases, a general user is able to see other user's information


# AC ~ Access Control
Testing for IDOR requires two separate accounts w/ the same role.
testing for AC bypass requires two or more separate accounts w/ different roles

### AC violation:
If a user with a role other than Admin is able to use the admin mechanism to read sensitive data about other users. An example to AC violation is finding a way to bypass 403 response from the web application. <br>
1. identify granular Roles within an instance of a web application
2. enumerate mechanisms that Role should not have the ability to execute
3. determine how that mechanism is actually executed w/ HTTP requests
4. execute the mechanisms the Role should not be able to execute


## Main methodology
Find a complex application. Complex applications will have lots of endpoints and many different places to look for vulnerabilities. Make sure the application you're testing has some different Roles, such as normal user, admin, audit role, and others.
If you are a beginner bug bounty hunter, tend to choose programs that pay less than others. The ones that pay a lot of money for bugs are usually being tested by other experienced hunters, but the ones that pay lower aren't often tested as much as higher payout ones.
Try to identify ways to understand how the user data is displayed, is it coming from the backend or some sort of API call is happening, or any other ways?
Then understand how authentication and authorization is made, this is to understand how the website know that you are you. 

## Questions to ask when approaching to the application
1. how is the application validating the role?
2. how is the application identifying the user?
3. how is the application identifying what role is trying to perfom the operation, and should they be allowed to do that certain operation?

> [!TIP]
> `Try to create sections`: 1. Pointers: identify other point of areas that would lead to other types of attacks (it is not just about finding another vulnerability, but take note of the important indication of possible idor or anything like that )
> 2. Mechanisms: try to idenntify CRUD mechanisms (create, read, update, delete), its good to breakdown each mechanism to its HTTP methods and what they do in the application so that you can see the whole picture better and refer back to your notes if you're lost.

> [!TIP]
> `Obtain the objects`: its the response returning back, like the objects returned with JSON (e.g.  userId, objectId, date, email...)
> `Creating multiple accounts`: + (plus notation) is a way to create multiple account under the same email, such as user@bugcrowdninja.com, user+admin@bugcrowdninja.com, user+developer@bugcrowdninja.com, and so on.  


##### THINGS TO BEAR IN MIND WHEN DOING BugBounty
Be very careful with the scope of the application, if you're testing a website and the payment mechanism redirects you to a different domain, be aware of the domain change. (it could redirect to a whole different application, especially for payment stuff )




##### THINGS TO LOOK UP
Learn what is DOM and how it is being used in the web context
What does it mean if a JWT token or any kind of token being used and validated, being used and not validated?
Learn what is the importance of CSRF cookie, what does it do, what is CSRF? 