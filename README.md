# Elite Lab 8: Deployment

## Intro
Congrats on getting this far!

Today we will be taking our web apps (which have been running locally on our computers), and deploying them to online web servers.
Now you will be able to share your site with others on the public internet.

## Privacy
Before we move further, I would like to warn you all about posting information online. Even though these websites are not likely to be found on the open internet by randoms, you should be very careful about what kind of information you choose to display publicly.

YOU ARE NOT REQUIRED TO POST ANY INFORMATION ABOUT YOURSELF IN THIS COURSE. Feel free to personalize your site to your own content.

My two cents as a working professional:\
It is a great boost to your own image during college/job recruitment to have a personal website. Especially if you are able to showcase your past experience/projects.\
I would suggest leaving enough information on your site to highlight your past achievements, but don't leave any information that can tie you personally to your personal life/social media.

### I would suggest including this information:
* Your name (especially if you wish to use this site for college/job)
* A SEPARATE email that you use for professional purposes (notice I have a separate dev email). Do NOT use your school email.
* Your Github profile (please make sure that content from your github can't be traced to your personal social media accounts)

### I am neutral including this information:
* A general location you are based in (California, SoCal, greater LA area, etc)
* A LinkedIn profile (once again, as long as your linkedin does not point to your personal social media)
* A phone number that is linked to a Google Phone number and NOT your personal

### I would caution you against including this information:
* Your personal Facebook profile
* Your personal Instagram
* A phone number associated to you personally (home or cell)
* Your personal email
* Your mailing address

Please think critically about how much information about yourself you would want to display on the open internet.


## Objective
### Task
By the end of this lab, you should have your final project (from last week's lab) available on the open internet.

Lab is considered complete when you have successfully deployed your code to Heroku and are able to access it via URL.

### Context
We will be using Heroku to deploy and host your websites. Heroku is a service for managed web platforms. You do not need to know the details of your deployment or server, Heroku will just do it for you.

Our usage of Heroku will be under the free version. You will need to create an account, but will NOT need payment info.

There is no starter code for this week. Instead you will be using the code from last week.

## Lab Steps

### Prepping our web code
    
* Prior to deployment, we must include a Procfile. This gives Heroku some instructions that will be necessary for us to manage our web app.
  * Create a file at the root of your project (top folder) called `Procfile`. Your Procfile should be next the the `README.md` and `lab-app.py` files.
  * Copy paste this text into the Procfile:
    ```
    web: gunicorn lab-app:app
    init: FLASK_APP=lab-app.py python3 -m flask db init
    migrate: FLASK_APP=lab-app.py python3 -m flask db migrate
    upgrade: FLASK_APP=lab-app.py python3 -m flask db upgrade
    ```
    
* Commit all your changes and send it to your remote repo
  ```
  git add -A
  git commit -m "prep for deployment
  git push
  ```
    
### Deploying to Heroku
* First, we need to [create a Heroku account]
[create a Heroku account]: https://signup.heroku.com/

* Follow the steps on that page and validate your email

* Once you are able to login and access the dashboard, go to the top right hand, and select `New -> Create new app`

* Choose a name for your application (it will be in your raw URL)

* Select United States as the region

* Download the Heroku CLI
  * https://devcenter.heroku.com/articles/heroku-cli
  * For Windows users, your system is using Ubuntu for dev purposes.\
  Try using this:\
  `sudo snap install --classic heroku`\
  If that doesn't work, try this:\
  `curl https://cli-assets.heroku.com/install-ubuntu.sh | sh`
  
* Login with the Heroku CLI by running this command in your terminal\
  `heroku login -i`
  
* Add your repository to the remote one:\
  `heroku git:remote -a {your-project-name}`\
  Make sure to replace {your-project-name} with the application name you gave in heroku. (You can also copy paste the command in the heroku dashboard
  
* Start your first deployment by running this command.\
  `git push heroku master`
  
* This should spit out a bunch of logs to your terminal. At the very end there should be a link looking like this:\
  `https://{your-project-name}.herokuapp.com/`
  
* Follow that link, and you should see your website available!

* Hold on, we are not done yet though, we need to set up our database.

* Run this command in your terminal:\
  `heroku addons:add heroku-postgresql:hobby-dev`
  
* This will tell heroku to add a postgre database to your hosting set

* Next run these commands to start and migrate that database
  ```
  heroku run init
  heroku run migrate
  heroku run upgrade
  ```
  
* Afterwards, you should be good to go! Go validate the features on your website.

## Supplemental

### New Deployments
If you wish to make further deployments to your code, follow these steps
* Make your changes inside your project
* Add and commit those changes to git
  ```
  git add -A
  git commit -m "my message"
  ```
* Push your changes to your remote repo\
  `git push`
* Deploy to heroku with:\
  `git push heroku master`
  
### Adding a custom domain name
Obviously you might not be happy with having herokuapp inside of your website. If you want to add a custom domain name, you will first need to buy one. 

I recommend these sites:
* https://domains.google/
* https://www.domain.com/
* https://www.godaddy.com/offers/domains

These will usually be about $5 - $50 a year.

After you have bought and validate ownership of your domain, follow the instructions are either of these links:
* https://devcenter.heroku.com/articles/custom-domains
* https://imranhsayed.medium.com/adding-your-custom-domain-to-heroku-app-cdd68d2db67f

The terms here are pretty confusing, but the gist is that you want to have Heroku recognize your domain, and validate that you own the domain.
You must also indicate that you want your domain to point to your website.

If you want to add your custom domain and are having trouble following these links (even after this class is over) feel completely free to contact me.
