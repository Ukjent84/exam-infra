Devops Continious delivery and automation with Councourse  and Terraform 




### System
The purpose of this application is to create a system that makes 
you control and manage projects for development in a safer and easier way 
using Terraform for configuration files and Concourse to create a pipeline 
connecting things together and giving you and your team a visual overview 
and  status of the system before staging and deploying a finished product.
 
In this pipeline you will see a basic infrastructure of a pipeline which will 
build a Springboot application docker image container and deploy it to a 
Heroku cloud service container-registry before creating -ci -staging and -production 
with statuscake monitoring it. The application contains a basic REST API using swagger 
as a tool with a few working tests.

The pipeline will automatically detect and update the CI everytime there is a change in the application 
after it has been commited and pushed to master and give a warning if tests or anything else fails.


###Install and instructions 

####Tools needed

Git account

git bash or a similar CLI

Docker

fly CLI

Heroku CLI


####Instruction
Before starting you need some pre-knowledge of Concourse, Docker and Heroku.
Once  you have installed everything follow the concourse tutorial:
https://concoursetutorial.com/

Once you have some overview lets start with running our pipeline. 
But before we do that we need to add and do some terraform config changes in our infrastructure (exam-infra). 

First you need to fork and then clone exam-app and exam-infra from your on repositroy and make it your own. 

1. In root folder of exam-Infra rename Credentials_example.yaml file to 
credentials.yaml
2. In your new credentials.yaml file replace content as follows:
   
   -Create private and public keys for app and infra by opening up a CLI (like git bash) and
   type 'ssh-keygen'. Then choose a suitable name like 'sshKeyApp' and press anter 3 times. Do the same again for exam-app.
   You have now created a public key and private key. Take good care of these and dont EVER push these public on github or anywhere else.
   
   -Then type 'cat <your sshkey name' and copy the output of the private key (not the one that ends with .pub) and  replace with the one in  credentials.yaml,
    appkey under app and infrakey under infra. Make sure they are EXACTLY positioned as the examples. 
   
   -Now you need to add the public keys to your github repositories. appkey.pub to your exam-app repo and opposite for exam-infra . 
   Type 'cat <sshKeynameApp.pub>  and copy this key. in your app repo click on settings---> deploy keys ---> add deploy key and paste 
   the key in there but remember to click "allow write access" right below it.  do the same again for exam-infra.
  
   -Create a Heroku account and add your heroku email, Heroku app name, and Heroku API key inside   in credentials.yaml 

   -Create a StatusCake account and add statuscake_api_key in credentials.yml
   
   -Create a github token by selecting the settings inside your profile. Click on 'developer settings' ----> then 'personal access token'. 
   and then 'generate new token'. copy and paste the token inside credentials.yaml

3.  Next we need to add these two new repositiories to your pipeline.
    Navigate to your Infra repository and copy your ssh uri. In your cloned exam-infra folder navigate 
    to concourse/ and open pipeline.yml in a editor. paste your copied ssh uri infra under resources:  name: exam-infra  uri: <your uri here> and do the same thing for 
    exam app.
    
4. Navigate to exam-infra/terraform/ and open provider_heroku-tf and add your Heroku email.

5. In same folder open up statuscake.tf and add username. Username is defined in 'userdetail' inside profile settings' 
in your account. commit and push everything to github ones again and remember to delete .tfState if any inside /terraform/

Now you can followw the concourse tutorial again, but make sure you run Docker compose up -d inside exam-app. Then Wget and fly commands inside exam-infra.
 
Start with running the Infra pipeline first and then app  ones infra turns green.

Check your heroku ci to verify it has been created.


###Run Rest applicaion
You can run the REST Api application locally with heroku cli installed by opening up the cli , navigate to root of exam-app and run 'heroku local'
or by this tutorial: https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku

Application will then be available at http://localhost:<portnumber>/movierest/api/swagger-ui.html
