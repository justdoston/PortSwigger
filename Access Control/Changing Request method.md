# Method-based access control can be circumvented

## Solution
Log in using the admin credentials.<br>
Browse to the admin panel, promote carlos, and send the HTTP request to Burp Repeater.<br>
Open a private/incognito browser window, and log in with the non-admin credentials.<br>
Attempt to re-promote carlos with the non-admin user by copying that user's session cookie into the existing 
Burp Repeater request, and observe that the response says "Unauthorized".<br>
Change the method from POST to POSTX and observe that the response changes to "missing parameter".<br>
Convert the request to use the GET method by right-clicking and selecting "Change request method".<br>
Change the username parameter to your username and resend the request.

## You tube best explanation
https://youtu.be/0mWVYM_dqIg
