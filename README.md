# Assignment 3 - Matthew Spofford

<https://cs4241-a3-MatthewSpofford.herokuapp.com>

## MyAgenda - *A simple homework agenda*

- what CSS framework you used and why
  - include any modifications to the CSS framework you made via custom CSS you authored

My project is a homework todo list web application. The user can add multiple homework assignments with various properties such as the assignment name, course, and due date. The users are also capable of completing assignments (which removes it from the server), as well as editing assignments (which directly modifies the on server data).

Currently there are some minor issues with the date handling, since it is using JavaScripts built in Date object. Due to the default timezone that the built-in Date object uses, the due dates occasionally appear off by a day, depending on what time the assignment was created (since there is currently no way of entering time easily on the due date form). This could be a fix for the future.

I faced many challenges during the creation of this application, especially with OAuth. For many hours I was implementing OAuth incorrectly without realizing it. When attempting
to redirect the user to GitHub so that they could accomplish the authentication, I first had them get sent to the apps OAuth redirect page. However, I mistakenly was having the
backend redirect the user to GitHub, before they had even reached the redirect page. This caused some issues with CORS because it could never reach the destination of the
redirect page. It took me multiple days to actually catch this problem, and I wish I had noticed it sooner. Other than this main issue, it was pretty much smooth sailing.

**Authentication Strategy**:

I chose OAuth as my authentication strategy. I chose this mainly because I wanted to challenge myself and learn something knew, but also because I know that
this form of authentication is widely used across web applications for authentication. While I definitely am not using OAuth in the most secure means possible
(since the authentication token is being saved in a session key), I have definitely thought about how I could improve my usage of OAuth.

These improvements would most likely involve creating a separate collection on the database for correlating user session ID information with their GitHub account ID.
This means that whenever a user successfully authenticated and retrieved an access token, the backend would then handle that correlation process. It would then connect
the access token to the user ID, and this setup would be much more secure. From there, whenever the user wanted to access the agenda, they would no longer be using
their access token directly, and would instead by going through their session IDs.

**Selected CSS Framework**:

**Express Middleware**:

- Express.static = Provides retrieval of static files whenever a get request for public files is requested.
- Body-parser = Parses JSON and url encoding when necessary.
- Cookie-parser = Handles creating and parsing cookies so that the backend can determine if the user is authenticated with an access token.
- PassportJS (OAuth2) = Used for establishing OAuth2 authentication for GitHub.
- CORS = Used to remove Same Origin Policy errors when redirecting to GitHub for OAuth.
- Custom MongoDB Middleware = determines if mongodb server could not establish a connection, and then outputs a 503 error code if it is down.
- Custom Redirect Middleware = Redirect to home page if a user is not logged in (determined by if a cookie exists) and is attempting to view their agenda.
                               Also redirects to the agenda if the user attempts to login but already has.


## Technical Achievements

- **Setup OAuth for Login**: I used PassportJS to create OAuth authentication with GitHub. This used the *passport-github2* Passport strategy available through NPM.
This module enabled all of the necessary core functionality for establishing a successful OAuth2 transaction with GitHub. I could then use it to save the
access token that was given for later usage by the user, allowing me to retrieve information such as their name so that it could be displayed on the agenda page.

- **Using Heroku for Hosting**: I decided to use Heroku for hosting my application. The main benefits of Heroku that I have noticed is that there seems to be little to no
downtime for starting the web backend. The major benefit that I really loved was the fact that it could automatically deploy a new version of the app once there were any
updates to the GitHub repository that I linked to it. Some slight cons however is that the logging capabilities seemed to be lacking slightly, and it was less convenient
trying to run commands directly on the VM that it was using.

### Design Achievements
