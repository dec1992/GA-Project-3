## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) General Assembly, Software Engineering Immersive
# Project #3: A MERN Stack App
## Overview

We were asked to build a MERN stack app, in groups of 4 students and 7 days. test

### Technical Requirements

* Work in a team, using **git to code collaboratively**.
* **Build a full-stack application** by making your own backend and your own front-end
* **Use an Express API** to serve your data from a Mongo database
* **Consume your API with a separate front-end** built with React
* **Be a complete product** which most likely means multiple relationships and CRUD functionality for at least a couple of models
* **Implement thoughtful user stories/wireframes** that are significant enough to help you know which features are core MVP and which you can cut
* **Have a visually impressive design** to kick your portfolio up a notch and have something to wow future clients & employers. **ALLOW** time for this.
* **Be deployed online** so it's publicly accessible.

### Concept 
We chose to build a platform to help you live a greener life: ***GreenWorld***. The idea was to enable users to **easily find local businesses and services that lower the carbon footprint** (Vegan/vegetarian restaurants, cycling shops, ethical groceries, EV charging stations, repair shops, charity shops etc.).

### Key features:
* A map with pins for all 'green' locations in the UK
* "Use my location" button to capture browser location of user
* List of all locations, with search by name and filter by categry
* Pages for each location with location details, comments and ratings
* User accounts and profiles
* Ability for users to comment and rate locations
* Ability for users to add and edit locations
* Responsive design

### Wireframes
![Wireframes](frontend/styles/readme_images/project-3-wireframes.png)

## Technologies

* HTML
* CSS / SASS
* Bulma
* JavaScript (ES6)
* React
* Git and GitHub
* MongoDB
* Express
* Node.js
* Ziteboard
* APIs
	* [Yelp](https://www.yelp.com/developers/documentation/v3)
	* [mapbox](https://docs.mapbox.com/api/)
* [Cloudinary](https://cloudinary.com/)

## Approach
### AddLocation
The AddLocation page is a form that captures each keystroke in a `const` via `useState`.
```
const [formData, updateFormData] = useState({
  category: [],
  address: '',
  name: '',
  timings: '',
  [...]
})

function handleChange(event) {
  const data = {
    ...formData,
    [event.target.name]: event.target.value
  }
  updateFormData(data)
  }
```

For the category selection we used a the `react-select` library. And for the image upload we used *Cloudinary*.

When the user clicks the 'Submit' button, the postcode gets sent to the geocoding endpoint of the *mapbox* API. 
```
function handleSubmit(event) {
  event.preventDefault()
[...]
  }
  Axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${formData.postcode}.json?access_token=${process.env.MapBoxKey}`)
    .then(resp => {
      const data = {
        ...formData,
        longitude: resp.data.features[0].center[0],
        latitude: resp.data.features[0].center[1]
      }
      updateFormData(data)
[...]
```
This returns the corresponding coordinates and is necessary for us to place a pin on the map for this location.
The complete information typed in the form and returned from the *mapbox* API is then stored in our database.

```
[...]
return Axios.post('/api/locations', data, {
  headers: { Authorization: `Bearer ${token}` }
})
  .then((resp) => {
    if (resp.data.errors) {
      updateErrors(resp.data.errors)
    } else {
      props.history.push('/locations')
    }
  })
[...]
```

### (Navbar)
### Seed.js
Find coordinates for our own seed data
get yelp data and match with ours
  loop to get all the data

## Challenges
Parse the yelp categories
How often to run the code

## Improvements

## Screenshots

## Contributors
- Baltasar Romero
- Dec Burns
- Florian Wilisch
- James Bolton