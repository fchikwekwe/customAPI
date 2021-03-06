# FoodPrint Companion API

The documentation site for this API is available at: https://fchikwekwe.github.io/FoodPrintAPI/.

## API Proposal
This app stores food with their CO2e output so that users that track their intake of these foods and see how much CO2 each food produces. It fulfills the need for those who care about or want to learn more about their personal environmental impact when it comes to their food intake.

## What is FoodPrint?
This is a companion API to the FoodPrint app. If you would like to check out the current, live version of FoodPrint, go to https://know-your-foodprint.herokuapp.com/.

## Content
Have you ever wanted to improve your overall carbon output, but were not sure how to do it? Use the FoodPrint API! This API is a food tracker that tells your your carbon output based each food you have eaten.

## Who are you?
I'm Faith Chikwekwe 👋🏾, a back-end web developer learning and growing at Make School (Github@MakeSchool).

## Why did you make FoodPrint in the first place?
Food is a huge contributor to CO2 emissions and its also a very personal way to help prevent global warming. We feel that if people are aware of how much each individual food item contributes in CO2 output to climate change, they will be more able to make positive changes to their diet that help the environment.

## Back-End Design
This project was developed using MongoDB, Node.js and Express.js in the back-end. We used resourceful and RESTful routing throughout and integrated authentication concepts. It also has test coverage with Mocha and Chai.

## Running
This API can be accessed at http://localhost:3000/. To check it out, type the command 'npm start' into your console from the root folder.

If you would like to check out the current, live version of the original FoodPrint, go to https://know-your-foodprint.herokuapp.com/.

## Testing
We used Mocha and Chai for testing. Tests are stored in /test. To run tests for this project, clone the project and then type the command 'npm test' or 'mocha' into your console from the project root folder.

## Are there other ways to learn more about Foodprint?
Me (Github@fchikwekwe 👩🏾‍💻) and Javier Mendoza (Github@javiermms 👨🏽‍💻) were the developers on the original FoodPrint application from which this API is derived. We also published a blog series (https://bit.ly/2GaQSa1) about our development process on this app.

If you would like more insight on how the app that we developed works, you can see a live user demo here https://vimeo.com/305850006.

# Food Model

| Key | Type | Description |
|-----|-------|---------------------|
| name | String | The name of the food. |
| description | String | The description of the food, ideally including some nutritional info. |
| CO2e | Number | The estimated carbon equivalent output. |

# Profile Model
| Key | Type | Description |
|-----|------|-------|
| Username | String | This is a required field. The user's identifier. |
| Password | String | This is a required field. The user's authentication credentials. |
| Foods | Array | This is an embedded document with a list of foods that the user has eaten. |

# Endpoints

## Profiles

### "/" | GET/ROOT
- This route renders your main index template.

### "/profiles/profileId" | GET/SHOW
- This route shows the profile of one user. You can redirect to this route from the sign-up and login routes.

### "/profiles/profileId/edit" | GET/FOOD REMOVE INDEX
- This route shows the food edit index where the user can add remove foods from their profile.

### "/profiles/profileId" | PUT/UPDATE AND ADD FOOD
- This route updates the user's profile by adding a food to their array of foods.
- These foods are stored in the 'foods' collection. Each food has a name, a description and a CO2e (carbon equivalent) score.
- This route also redirects back to the user's profile.

### "/profiles/profileId/delete" | PUT/UPDATE AND REMOVE FOOD
- This route updates the user's profile by removing all foods of the same name from their array of foods.
- These foods are only removed from the user's profile and are not deleted from the 'foods' collection using this route.
- This route also redirects back to the user's profile.

### "/profiles/profileId" | DELETE
- This route deletes the user's profile. It also removes the JWT (nToken) and then redirects back to the root route.


## Foods

### "/profiles/profileId/foods" | GET/FOOD INDEX
- This route renders the food index, where the user can select foods to add to their profile.

### "/profiles/profileId/foods" | POST
- This route is used to create a new food and add it to the food collection. This route is NOT used to add a new food to the user's profile (see /profiles/profileId PUT/UPDATE AND ADD FOOD) It then redirects back to the user's profile.

## Authentication

### "/sign-up" | GET
- This route renders your sign-up template. Name your template "signup-form" and store it in the views folder.

### "/sign-up" | POST
- This route processes the sign-up request and creates and new profile. Please note that "username" and "password" fields are required to create a new profile. This will result in the creation of a JWT (nToken) for the session.

### "/login" | GET
- This route will render your login template. Name your template "login-form" and store it in the views folder.

### "/login" | POST
- This route processes the login request. It will return 200 (success) if the username and password match an existing user. This will result in the creation of a JWT (nToken) for the session. It will return 401 (unauthorized) if either the username or the password do not match. In this case, no JWT will be created. 

### "/logout" | GET
- This route processes a logout request of the profile. It will remove the JWT (nToken) for that session and redirect the user back to the root route.
