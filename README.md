# WEB422-Assignment-3-solution

https://jarviscodinghub.com/assignment/web422-assignment-3-solution/

Email: jarviscodinghub@gmail.com

Objective:
To continue to work with our “Restaurants” API (from Assignment 1) on the client-side to produce a rich user
interface for accessing data. For this assignment, we will be leveraging our knowledge of React to create an
interface for viewing restaurants. Please Note: You’re free to style your app however you wish, however the
following specification outlines how we can use the React-Bootstrap Components (Bootstrap 4). If you wish to
add additional images, styles or functionality, please go ahead.
Sample Solution:
You can see a video of the solution running at the link below:

Video Player

00:00
00:45



Step 1: Creating a React App & Adding 3
rd Party Components
The first step is to create a new directory for your solution, open it in Visual Studio Code and open the
integrated terminal:
• Next, proceed to create a new react app by using “create-react-app” using the command “npx create-react-app”
followed by the identifier for your app, ie: “my-app”.
• Once the tool has finished creating your React App, be sure to “cd” into your new app directory and install the
following modules using npm:
o react-router-dom
o query-string
o react-bootstrap bootstrap@4.6.0
o react-router-bootstrap
o react-leaflet@3.1.0 @react-leaflet/core@1.0.2 leaflet
• To ensure that our newly-added Bootstrap components render properly, we must import the correct CSS file to
our “src/index.js” file, ie:
o import ‘bootstrap/dist/css/bootstrap.min.css’;
• Similarly, to ensure that our maps / markers are rendered correctly, we must include the leaflet CSS. This can be
done by adding the following line within the…element of our “public/index.html” file:
o
• Next, we must clear out (delete) the CSS content from both “App.css” and “index.css”, since we won’t be using
any of those rules within our new app. Once this is complete, place the following single line of css within the
“index.css” file (this will ensure that any table with class “table-hover” has the “Pointer” cursor:
.table-hover tr:hover{ cursor:pointer; }
Step 2: Route Component “Skeletons”
For the next part of the assignment, we’ll add all of the components that our routes will use as well as create a
navbar that persists across all routes to help the user navigate our app.
To Begin, add the following components in separate files (using the naming convention ComponentName.js)
within the “src” directory.
• Restaurants – outputs:

Restaurants query: query

where query is a value that we will retrieve by using
the “useLocation” hook
• Restaurant – outputs:

Restaurant id: id

where id is a value that we will retrieve by using the
“useParams” hook
• About – outputs

About

• NotFound – outputs

Not Found
We can’t find what you’re looking for…

(Note: please feel free to change this up to something more fun).
Step 3: App Component & NavBar
Before we add routing to our application, we must first do some work with the “App” component:
• To begin, add the following import statements
o import { Button, Col, Container, Form, FormControl, Nav, Navbar, Row } from ‘react-bootstrap’;
o import { Redirect, Route, Switch } from ‘react-router-dom’;
o import { LinkContainer } from ‘react-router-bootstrap’;
• Next, remove all of the contents from the return statement and instead simply return “null” (we will change this
soon)
• Next, delete the import for “logo” – we won’t be using the “logo” for our application.
o You can also delete the src/logo.svg file
• Now we must add the following “state” value to our App component:
o searchString / setSearchString – default value: “”
• Before we are done, we must add the following “handleSubmit(e)” function to the App component according
the following specification:
o Prevents the default action for the event (parameter e)
o Navigates to the route: /restaurants?borough=searchString where searchString is the value in the state
(above) – HINT: You can use the “useHistory” hook – see: “‘Redirecting’ to a Route”
https://web422.ca/notes/react-routing
o Resets the value of searchString to “”
This will enable us to filter our restaurants by a user-entered “borough” value.
• Finally, use the following JSX code to replace the return value of our App component. This will show a navbar
built using React-Bootstrap components.
<>
New York Restaurants

Full ListAbout
setSearchString(e.target.value)} />
Search
</>
Step 4: Adding Routes
With our Navbar in place and our App component all set up, we can now proceed to add the routes to our
application:
• In your src/index.js file, import the “BrowserRouter” component and use it to wrap the Component (ie:
the Component will be the only child of the Component
• Next, in the return value for the Component, add the following code beneath the navbar:

The above code simply sets up a Bootstrap grid with a single column
• Inside the

Component, add your Component as well as configuration for the
following routes:
o “/” – Redirects to the “/Restaurants” Route
o “/about” – Renders the Component
o “/Restaurants” – Renders the Component
o “/Restaurant/id” – Renders the Component
(note: id is a route parameter, used to specify a specific restaurant)
o (No Route) – Renders the Component
Step 5: “About” Component
The first of our “view” components is the “About” Component. For this component, we will simply display
information about the developer (you):
• Show a title for the page, ie:

This can be accomplished using the Card Component (https://react-bootstrapv4.netlify.app/components/cards/). However, feel free to use any other design elements, components from
react-bootstrap, etc. for your header.
NOTE: Whatever design you decide here, will be used throughout your application
• Place information that you wish to share about interesting projects you have completed / working on, your
academic career, development interests, etc.
Step 6: “Restaurants” Component
The next “view” component is the “Restaurants” Component. For this component to function properly, it
needs to adhere to the following specification:
• It must import the “useLocation” hook from “react-router-dom”
• It must also have following “state” values:
o restaurants / setRestaurants – default value: null
o page / setPage – default value: 1
• When the component is first mounted, location (from the useLocation hook) is changed, or the page “state”
value is changed, the following logic (ie: “effect”) should be performed:
o Execute a fetch request to the api/restaurants route of your Restaurant API on Heroku (from
“Assignment 1”) using the query parameters:
▪ page – the value of page in the “state”
▪ perPage – 10 (this can either be hardcoded in the request or added as a const at the top of the
component.
▪ Borough – the value of borough in the search property from location (from the useLocation hook).
This can be obtained by “parsing” the value of location.search. HINT: You can use the “query-string”
module – see: “Adding Query Parameters to our Routes” https://web422.ca/notes/react-routing
• NOTE: If the value of “borough” is undefined, in the query string, then do not include it in
the fetch request as a parameter
o When the fetch operation has completed (ie: once the result is obtained and the data is parsed), set the
value of restaurants in the “state” to the data returned
• A “previousPage()” utility function must be implemented such that:
o It decreases the value of page in the “state” by one (1), only if the current value is greater than zero (0)
• A “nextPage()” utility function must be implemented such that:
o It increases the value of page in the “state” by one (1).
• Next, we must modify the return value to provide a way for users to view and interact with the restaurants array
in the “state”.
First, we will need to display a header for the view (using the same design that you used for your “About”
component). This will simply be a static message reminding the users that they are viewing the full list of
restaurants, and that they can search by “borough”, ie:
Next, you’re free to use any method you wish to display the restaurants data. If you wish to try to duplicate the
demo video, a

…

was used, however there are other options as well,
such as: …, …, …, etc.
Whichever method you wish to show the values in the restaurants array, you must ensure that for each
restaurant, you show:
▪ name
▪ address building + address street
▪ borough
▪ cuisine
To navigate to a specific restaurant when an item is clicked the following code can be used:
onClick={()=>{ history.push(`/restaurant/${restaurant._id}`)}}
NOTE: This assumes that restaurant is the current “restaurant” object in the iteration used to display
restaurants and that you have added the “useHistory” hook – see: “‘Redirecting’ to a Route”
https://web422.ca/notes/react-routing
To enable paging, we can use the … component, specifically:
You will have to ensure that:
• when is clicked, the previousPage() method is invoked
• when is clicked, the nextPage() method is invoked
• the component contains the value for page in the “state”
• Finally, it is important to note that there are also some circumstances when you are unable to render the
restaurants data, such as:
o The request is still in progress (ie: restaurants is null)
o restaurants is not null, but it doesn’t contain any values (ie: it is an empty array)
In either case, render an appropriate message / indication to the user, ie:
or
Step 7: “Restaurant” Component
The second “view” component used to render data from our API is the “Restaurant” component. When
implementing this one, you will need to adhere to the following specification:
• The leaflet components must be imported, ie:
import { MapContainer, TileLayer, Marker } from ‘react-leaflet’;
• It must import the “useParams” hook from “react-router-dom”
• It must also have following “state” values:
o restaurant / setRestaurant – default value: null
o loading / setLoading – default value: true
• When the component is first mounted or when id (from the useParams hook) is changed, the following logic (ie:
“effect”) should be performed:
o Set the loading “state” value to true
o Execute a fetch request to the api/restaurant/id route of your Restaurant API on Heroku (from
“Assignment 1”), where id is the value of id (from the useLocation hook)
o When the fetch operation has completed (ie: once the result is obtained and the data is parsed), we
must:
▪ Set the loading “state” value to false
▪ Make the following check to ensure that the data that came back was indeed a restaurant
object and update the state accordingly, ie:
if(data.hasOwnProperty(“_id”)){
set the restaurant value in the “state” to data
}else{
set the restaurant value in the “state” to null
}
• Next, we must modify the return value to provide a way for users to view the restaurant object in the “state”.
First, we will need to display a header for the view (using the same design that you used for your “About”
component). This will contain the name of the restaurant as well as a combination of the address building and
address street values, ie:
Once this is complete, we will need get the map for the restaurant working. You may use the following code,
where restaurant address coordinate values should be replaced with values from the address coord array:

Next, we must display all of the “grades” for the restaurant, once again You’re free to use any method you wish
to display the grades data. If you wish to try to duplicate the demo video, a …
containing multiple … components was used.
Whichever method you wish to show the values in the grades array (for the specific restaurant object in the
“state”), you must ensure that for each grade, you show:
▪ grade
▪ date
• Finally, it is important to note that there are also some circumstances when you are unable to render the
restaurant data, such as:
o The request is still in progress (ie: loading is true)
o loading is no longer true, but the value of restaurant is null
In either case, render an appropriate message / indication to the user, ie:
or
Once you have updated this final component, your assignment should be complete. Please check it against
the sample video (top) and ensure that its functioning correctly before submitting.
Assignment Submission:
• For this assignment, you will be required to build your assignment before submitting. This will involve running
the command:
o npm run build
to create a “build” folder that you will include in your submission
• Next, add the following declaration at the top of your index.js file
/*********************************************************************************
* WEB422 – Assignment 3
* I declare that this assignment is my own work in accordance with Seneca Academic Policy.
* No part of this assignment has been copied manually or electronically from any other source
* (including web sites) or distributed to other students.
*
* Name: ______________________ Student ID: __________________ Date: ____________________
*
*
********************************************************************************/
• Compress (.zip) the files in your Visual Studio working directory without node_modules (this is the folder that
you opened in Visual Studio to create your client side code).
Important Note:
• NO LATE SUBMISSIONS for assignments. Late assignment submissions will not be accepted and will receive a
grade of zero (0).
• After the end (11:59PM) of the due date, the assignment submission link on My.Seneca will no longer be
available.
• Submitted assignments must run locally, ie: start up errors causing the assignment/app to fail on startup will
result in a grade of zero (0) for the assignment.
