## About
This is the app engine project for the conference organization application


## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool


## HOW TO RUN
Please follow the setup instructions to run locally and test endpoint methods with the api tool.

## Answers

Design Decisions

I implemented the Speaker simply as a StringProperty of a Session. I thought it might make sense down the line to create a Speaker entity but right now the functionality of the application and API simply doesn't require it. 

Sessions are their own entity and speaker is just a property of a Session. Session entities are a descendent of Conference entities. I added a wishlist property to the Profile entity as well that stores a list of session keys. 

Most of the properties of a Session entity are string properties. The ones that are strings are strings because they come from user defined text. The ones that are not strings are duration, date, and startTime. Duration is a length in minutes so I made that an integer property. Date comes from specially formatted text that presumably would come from a date picker in the application. Time would also presumably be specially formatted by the application once the user picks the time from a drop down menu. Since date and time need to maintain a specific format, they are both respectively DateProperty and TimeProperty.

