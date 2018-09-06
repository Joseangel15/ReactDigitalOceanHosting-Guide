# Guide - React Project Hosting with Digital Ocean(HTTPS)
### Hosting a React website(HTTPS) with Digital Ocean

## About
<details> 
<summary>A guide for hosting a ReactJS project using Digital Ocean services. In this guide users will learn:</summary> 

- how to find/create an SSH key 
- prepare your React project for hosting
- create a Digital Ocean droplet
- connect to and access the droplet
- how to install node in your droplet for a server
- how to install pm2 in your droplet to let your server run automatically
- create and edit environment variables on the drople
- create a virtual projects and build folder to run as your hosted site

#### *As a Bonus Section I will continue to add relevant content. Currently I have add *How to Update Your Live Website* and I am working on *Adding a Domain Name to Your Website*.
</details>

## Table of Contents
###### Hosting a project
- Sign Up for a Digital Ocean account
- Create a Digital Ocean project & droplet
- Create a SSH key & Add to Droplet
- Check/Install proper software to droplet
- Prep project folders & files
- Create a clone of project
- Install npm & add environment variables on droplet
- Create a build folder
- Configure pm2
##### Bonus - Updating & Domain Names
- How to update content on your live website
- How to replace your IP address with a domain name

***

## Digital Ocean Sign Up(skip if already have)

###### Have credit card/payment details ready

1. Navigation to www.digitalocean.com
1. Enter an email & password OR follow the prompt and sign up with Google
1. From your email account, confirm your new Digital Ocean account
1. Enter in your payment method(Either CC or PayPal)
1. After a payment method is entered, you should be automatically navigated to you Digital Ocean control panel
1. If you screen matches the image below you are ready to move on to the next step

##### Digital Ocean Control Panel:
![alt text](https://i.imgur.com/sZ6eOsL.png)

***

## Create a project & droplet with Digital Ocean

1. On the left-hand side of the screen click on: + New Project
2. Fill out the input(Name, Description, Purpose) and click Create Project
3. If prompted to Move Resources into project, click Skip For Now
4. Click on the name of your new project on the top left-hand side of the control panel
5. Now click on the Create drop down button on at the very top of your screen(on the right-hand-ish side) and select Droplets
6. Leave the Choose an image option as the default(Ubuntu), scroll down and choose your desired size

##### Default image Ubuntu:
![alt text](https://i.imgur.com/zpC9ejm.png)

7. Next scroll down some more to the Choose a datacenter region section and choose the best location for you
8. Finally, scroll down a little more to Add your SSH keys and stop here. We will leave this open and finish in in the next section

##### Add your SSH Keys, stopping point:
![alt text](https://i.imgur.com/OKHFmxg.png)


***

## Create a SSH Key & Add to Droplet

##### SSH Keys are generated once per computer, only create one if you've never have before or had a key you know needs to be replaced

1. Open up your Git terminal
1. Check first if you have a key:
```
cd ~/.ssh
ls
```

1. Look for id_rsa.pub OR id_dsa.pub. If you do not see either, continue to the next step to create one.
1. Using your Git/GitHub email address type the following command(caps not necessary):
```
ssh-keygen -t rsa -C "YOUREMAILADDRESSHERE@email.com"
```

1. You will be prompted to add a password or not. If you choose a password, it is important you do not forget this!!
1. Once you have finshed creating your SSH key and password, try typing the first command below & second if the first does not work:
```
cat ~/.ssh/id_rsa.pub
```

OR

```
cat ~/.ssh/id_dsa.pub
```

1. In your terminal a long key will appear, copy your SSH key starting at ssh- and ending with the email address

##### Example:
```
ssh-rsa XXXXZ3NzaC1yc2EAAAADAQABAAABAQDlVwQDt4O7Hy4jyc2Yg5usW0kat5wsOoz9tZXUef
rv2CSsnqUOypWH3k8MPDPhgmVLmvSUP8dNfeiMjAQ+Bs/7b9Uwt2B1rkHcIyPI1F1+5Ajc/PWeHWGM
foJZhMV/BprXwOAiAP/bMztHGTOyctsEW1fwBfcjO8lWJQ9Yf2xsZWpeuzwSHW9WMqrrN57DX2dfrC
8L8C/3uBhMeoM9O54vpQm4XxPggBXK01yQdj6zcnUJDigEanxNi4lHva0qRmc5+ZWrlk4t3IROpqOW
Zfe3Yvr9qagmSYMfnf/ YOUREMAILLADDRESS@gmail.com
```

1. Now open up the Digital Ocean control panel and click on the New SSH Key button
1. Paste in your key and give it a name
1. Make sure only 1 Droplet is selected below, give droplet a name, select the project created earlier and then click Create
1. On the Digital Ocean control panel, your project should be select and you should see your droplet name and an IP address
1. Copy the IP address and move on to the next section

##### Example IP address:
![alt text](https://i.imgur.com/PgW4Qoc.png)


## Installing the proper software in droplet

1. Open your Git terminal back up and type `ssh root@YOURIPADDRESSHERE`:
```
ssh root@YOURIPADDRESSHERE
```
1. Enter your password when prompted
1. Now we will install the needed software which can be done in very quickly one step() or you can follow along with the *breakdown*
1. For a quick copy and paste:
```
touch /swapfile;fallocate -l 1G /swapfile;chmod 600 /swapfile;mkswap /swapfile;swapon /swapfile;sudo add-apt-repository ppa:certbot/certbot -y;apt-get update -y && apt-get dist-upgrade -y; sudo apt-get install python-certbot-nginx -y; apt-get install nodejs -y;apt-get install npm -y;npm i -g n;n stable;npm i -g npm;npm i -g pm2;apt-get install nginx -y;npm i -g yarn;
```

1. To follow the *breakdown*:

##### Installation Breakdown
***

## - Create and set up a swapfile:
##### Helps extend your project's memory through the swapping of temp files

```
touch /swapfile
fallocate -l 1G /swapfile;
chmod 600 /swapfile;
mkswap /swapfile;
swapon /swapfile;
````

1. If a *fallocate* error occurred, turn the swapfile off then on and try entering in the previous commands starting with `fallocate -l 1G /swapfile;` 
1. You can turn your swapfile on or off using either of the following commands
```
swapoff /swapfile
swapon /swapfile
```

## Install Node:

1. Update the software with the commands: `apt-get update && apt-get dist-upgrade`
1. Install Node using: `apt-get install nodejs -y; apt-get install npm -y;`
1. Globally install n: `npm i -g n;`
1. Update to latest stable version: `n stable;`
1. Install lastest version of Node: `npm i -g npm;`

## Add Certbot

##### Helps automate certficates - makes droplet HTTPS

1. Type in these two commands in order:
```
sudo add-apt-repository ppa:certbot/certbot -y
sudo apt-get install python-certbot-nginx-y
```

## Install pm2

##### pm2 is a program that keeps your website's server continuously running

1. Type in your terminal: `npm i -g pm2`

## Install nginx

##### Helps configure what domains and ports match up on your server

1. Type in the command: `apt-get install nginx -y`

### *To exit the droplet press `Ctrl + d`

***

## Prepare project folder & files

1. In your package.json file if there is a *homepage* value, remove it
1. Replace any absolute paths with environment variables.
##### Example: `src="http://localhost:3000/information"` ===> `src={process.env.REACT_APP_SITE_INFO}`
1. When I create a React project, one of the first things I do is remove the *registerServiceWorker()*
##### If you haven't already, remove any *registerServiceWorker()* and delete the actual service worker file:
![alt text](https://i.imgur.com/MPbZcxN.png)
1. Make sure all the correct files/folders are in your gitignore, save everything, commit and push any new changes to GitHub
1. Now that everything is up to date, make sure you project still works locally(yarn start, npm start)
1. If everything is good, shut down your local server and create a build folder: `npm run build OR yarn run build`
1. Open your server file, copy & paste the code below to tell Express to point to the build folder when running your project:
```
app.use( express.static( `${__dirname}/../build` ) );
```
##### If you are using React Router paste in the code below(towards the top of the file) to ensure everything runs properly:
```
const path = require('path'); 

app.get('*', (req, res)=>{
    res.sendFile(path.join(__dirname, '../build/index.html'));
});
```
![alt text](https://i.imgur.com/dbvxoFi.png)


***

## Clone project
##### Double check to make sure your project is saved and up to date on GitHub

1. Open your terminal back up and if it isn't already open type: `ssh root@YOURIPADDRESSHERE` to reconnect to your droplet
1. Install Git: `sudo apt-get install git`
1. Now clone your project with Git: `git clone URLTOYOURGITHUBPROJECT`

##### Example URL for a GitHub project:
![alt text](https://i.imgur.com/NOUSZqP.png)

***

## Install npm & add .env
1. Type `ls` to see if your project folder is there, if it is `cd` into it
1. Now install npm: `npm install`
1. Create environment variables: 
- Create an .env file: `touch .env` 
- Edit your .env file: `nano .env`
1. Open open your project and copy the contents from your .env file and paste it into your terminal
##### If you are using any `http://localhost:3000/WHATEVER/ELSE` replace with relative paths: `/WHATEVER/ELSE`
##### I like to have a port for my local project and my hosted project. It's totally option but I like to add either a port or change the name in my droplet's env file. 
    - Ex) `HOST_PORT=80`

- Press *Ctrl + x* to exit the .env file, *y* or *yes* to save and press Enter to exit  

***

## Create a build folder
1. Now create a build folder: `npm run build` OR `npm build`
1. Test to make sure your project is working by running node in your server file. 
    - Ex) `node server/server.js` -  Use `ls` if you are having trouble. 
1. Open your browser and enter in your droplets IP address + :YOURPORT 
    - Ex) `138.68.247.223:8000`

![alt text](https://i.imgur.com/XRyNj9Q.png)

##### *If you have errors you cannot figure out, double check the code in your server file and if necessary run `npm run build` over again

***

## Configure pm2

##### Make sure you are in the upper most folder of your project

1. Using the same file path you tested with node a few steps earlier, start pm2 by typing  `pm2 start YOURSERVERFILEPATH` 
    - Ex) `pm2 start server/server.js`
1. A row with columns should pop up and then you will be good to go, your website is continuously running
##### Example of the row w/columns from pm2:
![alt text](https://i.imgur.com/1z7uv66.png)

- Other pm2 commands:
    - Restart all instances: `pm2 restart all`
    - Restart a specific instance: `pm 2 restart PROJECTID`
    - Display all instances: `pm2 list`
    - Stop all instances: `pm2 stop all`


***

# Bonus Content - Update Site/Add Domain Name

## Updating your live website
1. I recommend always starting by making sure your local project works: `npm start` OR `yarn start`
1. Next make sure your project is saved and everything is up to date on GitHub
1. Using your terminal, connect to your droplet: `ssh root@YOURIPADDRESS`
1. If you are not already in, use `ls` and `cd` to navigate to your project folder
1. Now type in `git status` and there should be no new changes. If there are new changes, skip the next step
1. If there are no new changes now type: `git fetch` to update with GitHub
1. Now it should be a commit behind so use `git pull` to pull down the code and even out the commits
1. Now you can run `npm run build` to create an updated build folder
1. Make sure to restart pm2: `pm2 restart all` OR `pm2 restart PROJECTID`

##### *If you need to change your *.env* folder, make sure to run `npm run build` so everything is updated


***

## Replacing the IP address with a domain name
##### To use a domain name, you must purchase one

- GoDaddy
##### Currently the only hosting company I have used. The others are most likely a similar process.

1. If you do not have one already, log on to Go Daddy and purchase your desired domain name
1. Make sure to open your browser and log in to your Digital Ocean account
1. Once on the control panel click on Networking on the right-hand side
![alt text](https://i.imgur.com/19lzmnZ.png)






