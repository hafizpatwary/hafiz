# Diet App

Website address: http://35.239.174.237:8001  (Currently offline)

Test coverage:   http://35.239.174.237:8001/coverage  (Currenlty offline)

Jenkins server:  http://34.76.132.65:8080  (Currently offline)

Presentations:   https://docs.google.com/presentation/d/1dxu-wNn20tZVPTJbh8eNdPEUXCw7bb71MUcYty7vHPQ/edit#slide=id.p










# Diet Plan

## Index
[Brief](#brief)
   * [Solution](#solution)

[Architecture](#architecture)
   * [Entity Relationship Diagrams](#erd)

[Risk Assessment](#risks)
   * [Risk Sssessment Table](#risks)
   * [Explanations](#risks_expl)

[User sotry](#user_sotry)
   * [Use case diagram](#use_case)

[Testing](#testing)


[Deployment](#depl)
   * [Technologies Used](#tech)


[Front End Design](#FE)

[Improvements for the Future](#improve)
   * Blue Print
   * Static and Ephermal IP
   * Functionalities
   * ERD

[Authors](#auth)

<a name="brief"></a>
## The Brief
To create a CRUD application with utilisation of supporting tools, methodologies and technologies that encapsulate all core modules covered during training.
<a name="solution"></a>
### Solution
My project focuses around health and lifestyle. The web appliation I created allow the user to vist the website and create diets that can be shared with the app's community.
The diets will consist of meals, that the user can create and add to their diet.

<a href="https://trello.com/b/Edpyk0uq/solo-project-qa" target="_blank">Project planning</a>

<a name="architecture"></a>
## Architecture
<a name="erd"></a>
### Entity Relationship Diagrams
#### Initial plan

<img src="/Documentation/ERD_Initial_Plan.png" alt="Initial ERD" width="60%" height="60%"/>

The initial plan for the ERD consisted in meeting the requirements set by the project brief,
 the application should have contained at least two tables with a relationship between them.
  As shown above the diet table has a one to many relationship with food table;
  meaning that diets can have multiple foods but not the other way round.


However, it is likely that different meals will be part of many diets. Hence, the delivered solution includes a secondary table that facilitate a many to many realtionship between food and diet.

#### Delivered solution
![Final ERD](/Documentation/ERD_Final.png)


In the final ERD as well as food and diet tables, a user table has been added. After completing the initial ERD tables, it made sense that different food can belong to different diets.
The user table was added so that a diet plan can only be modified or deleted by the owner of diet only.
The agile methodology enabled the addition of this features, i.e. once the minimum viable product was met (two relational tables), I was able improve the functionalties.

<a name="user_sotry"></a>
## Project planning and user stories
For the prject tracking a tool called Trello has been used. Trello is a free and easy to use platform, that allow to create Kanban boards.
For this project a kanban board was created, to keep track features as well as user stories.

<img src="/Documentation/trello.png" alt="Use case" width="100%" height="100%" border="5"/>

Detatiled history of how user stories were implemented can be found on Trello borad [here](https://trello.com/b/Edpyk0uq/solo-project-qa)

An overview of the use case:
<img src="/Documentation/usecase.png" alt="Use case" width="80%" height="80%" border="5"/>


<a name="risks" ></a>
## Risk Assessment

| Risks                            | Likelihood    | Impact       |    Explanation          |
| -------------------------------- |:-------------:| :-----------:| -----------------------:|
| Lack of clear planning           | Low           | High         | [1 Click here](#plan)
|  Jenkins server being hacked     | Medium        |   Medium     | [2 Click here](#auto)
| Automation causing issues        | Medium        |  High        | [3 Click here](#jenkins)
| Database's IP address, username and password up in GitHub  | High     |    High | [4 Click here](#database)
| Running out of GCP credit        |  Very Low     |    Low       | [5 Click here](#gcp)

<a name="risks_expl" ></a>
<a name="plan"></a>
#### Lack of clear planning
Building of web app can get complex down the line as the code source get larger, hence:
* Not having a clear blue print to manage the code can make debugging difficult
* Not prioritising the functionality to build for the website means slower delivery
Solution:
* Set deadline and checklist of work
* Plan the blue print of the application

<a name="jenkins"></a>
#### Jenkins server being hacked
Currenlty Jenkins server can be accessed anywhere by username and password:
* If someone other than the product owner knows the credentials, they can access the deployment server
 and get sensitive data such the environment variables for the database
Solution:
* Make a strong password for Jenkins account
* Possibly allow access from certain IP address only
* Change password often

<a name="database"></a>
#### Database's IP address, username and password up in GitHub
During development it is likely that I will be working on different machines, hence there will be a public Git repo. Hence, it is very likely that I may upload some credentils by mistake
Solution:
* Set enviornmental variables so that crednetials can be accesed by one person only
* Delete credentials if you know someone else might use the same machine

<a name="auto"></a>
#### Automation causing issues
Automation can save a lot of time and hussle if done right, however if not done properly it can:
* Slow down development time, if the script witten is full of bug. e.g. Jenkins script not cloning down the correct repo, might take time to debug the problem
Solution:
* Automate only repetitive tasks such as deployment
* Do not automate a task that is not repetitive, such as setting environmental variables

<a name="gcp"></a>
#### Running out of GCP credit
It is unlikely that I will run out of GCP credit for this project, however it is still a possibility if:
* Leaving multiple instance up and running
* Leaving multiple database open can eat credit very quickly
Solution:
* Stop or delte instances that are not required
* Do not leave autoscaling on any instance, as this might drain GCP credit very quickly if there is an increase in traffict to the website

## Testing

Testing has been done using pytest. The coverage report for the backend is 54%.
With pytest I was able to test functionality that did not require user login, as most functions in my app
requires user login. The coverage for testing could have been improved by using another tool called Selenium.

<img src="/Documentation/test_results.png" alt="Diet Page" width="100%" height="100%" border="5"/>

With pytest I was able to test **functionality that did not require user login**, as most functions in my app
requires user login, the coverage for **testing could have been improved** by **using the Selenium** tool.
However due to the time contraint this was not covered.

<img src="/Documentation/test_login.png" alt="Diet Page" width="80%" height="80%" border="5"/>
Code snippets higlited in red were not covered as they require a user to be logged in. Almost 70% of the application required user to be authenticated.

<a name="depl"></a>
## Deployment

The test and deployment process for the web app was automated using Jenkins, a CI server.
Jenkins run in a GCP instance that automatically deploys the webapp into deployment server, with a webhook to GitHub which is triggered with every push event.

Jenkins justification:
* Open source tool with great community support.
* Contains plugins to facilitate automation
* High customisation


![Deployment Pipeline](/Documentation/CI_pipeline.png)
<a name="tech"></a>
### Technologies Used

* Database: GCP SQL Server
* Programming language: Python
* Framework: Flask
* Deployment: Gunicorn
* CI Server: Jenkins
* Test Reporting: Pytest
* VCS: [Git](https://github.com/devops-cohort/hafiz)
* Project Tracking: [Trello](https://trello.com/b/Edpyk0uq/solo-project-qa)
* Live Environment: GCP


<a name="FE"></a>
## Front End Design

#### Diets page

<img src="/Documentation/diet_page.png" alt="Diet Page" width="80%" height="80%" border="5"/>

#### Add food to diet

<img src="/Documentation/addfood.png" alt="Add food to Diet" width="80%" height="80%" border="5"/>


#### Foods page

<img src="/Documentation/food_page.png" alt="Food Page" width="80%" height="80%" border="5"/>


<a name="improve"></a>
## Improvements for the Future

As development went by, the source code for routes, kept getting larger:
* Subdivide routes in their own catergory:
-- e.g. Registration, Login and account can have their own file
-- Diet, food and homepage can be in the same file


* Bear in mind that GCP only allows one static IP address **per region**. A problem encountered during development was getting internal server error. This was because SQL network was set to a ephermal IP address. This meant a lot of time lost figuring the issue. **Get different static IP address to save internal server errors.**


* Functionalities:
  * Add author name to the diet
  * Add total calories in diet card
  * Add functionality to make diet private or public
  * Search functionality as the food will increase
  * Most webiste are accessed my mobile devices, make the app mobile friendly

* ERD:
  * As the number of food get larger, I would implement each user to have their own food
  * A one to many relationship for users and food

<a name="auth"></a>
## Author

Hafiz Patwary





