App Engine application for the Udacity training course.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

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


Query Question

The problem is that we cannot have an inequality filter on more than property. Assuming there is a finite set of session types, we could obtain a list of those types excluding the workshop type. Then when we apply the filters we only accept the results that are of a type within that set. We have avoided the inequality filter on the workshop session type.

In order to implement this easily, we would replace the inequality filters with an equality filter that checks to see if the session type is in the list. We could get this list of types by specifying the list in the application and changing the typeOfSession field to a dropdown that only shows types in the list. We could also get the list by checking the list everytime a new session is added. If the new session has a type that is not in the list, it is added to the list.

Query 1

I created a new endpoints method called getSessionsByDuration. This query functions similarly to the query for get SessionsBySpeaker in that we are retrieving results from the entire set of Sessions.

Query 2

I created a new endpoints method called getSessionsByType. This query also functions similarly to the query for get SessionsBySpeaker. It does the same thing as getConferenceSessionsByType except it also retrieves results from the entire set.