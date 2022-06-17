# CI/CD with Jenkins
CI/CD (continuous integration/continuous delivery) is a method to frequently deliver apps to customers by introducing automation into the stages of app development. 

## what are the benefits of CI/CD pipeline
Developers merge/commit code to master branch multiple times a day, fully automated build and test process which gives feedback within few minutes

Continuous Delivery - release new changes to your customers quickly in a sustainable way


## What is the difference between CD & CDE use cases?
The main difference is the deployment step, in continuous delivery the deployment is done manually and in continuous deployment it happens automatically.

## What is Jenkins
- Jenkins is an automation server
- Jenkins is used for continuous integration
- Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build.

## What are the other tools available for CICD pipeline - Why Jenkins

![tools.png](/tools.png)

Why Jenkins? Because it is opensources, meaning that there are a tonne of documentations and plugins avalible helping in its functionality.
Other advatanges inclide:

- Easy installation 
- User-friendly interface
- Accessable environment configuration 
- Supports distributed builds with master-slave architecture.

## Setting up a Job in Jenkins 
 
**Step 1: Create new item**
- On the left you should see `New item`, select that. 

**Step 2: Create job**
- Under `Enter an item name` write the appropriate name for your job 


## SSH Connection Between Github and Jenkins 

![ssh.png](/ssh.png)

**Step 1: Generate a new key**
- Generate a new ssh key in your localhost and name is syed-jenkins. 

#### Step 2: Generate ssh key 
You must generate a ssh key to use for authentication. 

1. Open the terminal 
   
2. Create a .ssh directory `mkdir .ssh` then open the directory `cd .ssh`

3. Now, paste the text below, ensuring to use the email associated with you Github account.

   `$ ssh-keygen -t rsa -b 4096 -C "zahir.hamza688@gmail.com"`
 

   The Following prompts will appear. For each of these prompts  press enter
   This should generate a public and private key pair 
   
> Enter a file in which to save the key (~/.ssh/): [eng114]

> Enter passphrase (empty for no passphrase): [Type a passphrase]

> Enter same passphrase again: [Type passphrase again]

4. Copy the `.pub` then open Github

5. When on Github, open `Settings` then `SSH and GPG keys` then click `New SSH key` . Now paste here

#### Step 3: Initializing a repo

- `git pull`

- `git status` To ensure only required files are added to be sent

- `git add .` To add git all files or `git add 'name_of_the_file'`

- `git commit -m "message"` To save changes 

- `git push -u'` To push changes to Github 

**Clone a specific remote branch**
- `git clone git@github.com:Syed-Hamza-Zahir/eng114_devops.git`

**Step 2: Copy Key into Github**
- Go into your repo and select `Settings`
- Select `Deploy Keys` and select `Add deploy key`
- Copy the public ssh key into `key` and title syed-jenkins 
- Now select `Add key`

**Step 3: Connect to Jenckins**
- Create a new Jenkins item and select `Freestyle Project`
-
- Set up the following configurations:

- **Discard old builds**: 3
- **Github project**: Insert GitHub HTTPS repo link 
- **Restrict where this project can be run**: `sparta-ubuntu-node`
- **Git**:
    - **Repository URL**: Insert GitHub SSH repo link 
    - **Credential**: Add -> Jenkins -> Key -> Insert private ssh key 
- **Branches to build**: */main
- **Github hook trigger for GITScm polling**: check this option 
- **Execute code**:
  cd app
  npm install
  npm test

## Setting Up a Webhook
Setting up the webhook allows GitHub to trigger Jenkins to start a new build whenever a new commit is pushed.

- In the GitHub repository that is to be linked to Jenkins, create a new Webhook (Settings-->Webhooks-->Add webhook)

- Payload URL: Add the URL (usually specified with ip and port) with /github-webhook/ appended at the end

- Content type: Select application/json

- Any new pushes to the repository should now trigger a new build, shown in 

- Build History where the Console Output can be read for each individual build

## Setting up a second job to merge dev and main branch upon test success 
- Set up the following configurations:

- **Discard old builds**: 3
- **Github project**: Insert GitHub HTTPS repo link 
- **Restrict where this project can be run**: `sparta-ubuntu-node`
- **Git**:
    - **Repository URL**: Insert GitHub SSH repo link 
    - **Credential**: Add -> Jenkins -> Key -> Insert private ssh key 
- **Branches to build**: */dev3
- **Github hook trigger for GITScm polling**: check this option
- - **Execute code**:
  cd app
  npm install
  npm test
- - **Post build actions**:
- match configuration as so and click save:
- ![conf.png](/conf.png)
  
