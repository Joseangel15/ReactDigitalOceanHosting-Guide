# Guide - React Project Hosting to Digital Ocean

## Table of Contents
###### Hosting a project
- Sign Up for a Digital Ocean account
- Create a Digital Ocean project & droplet
- Create a SSH key
- Check/Install proper software to droplet
- Prep project folders & files
- Create a clone of project
- Add environment variables on droplet
- Install NPM & run build
- Configure pm2

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


1. On the left hand side of the screen click on: + New Project
2. Fill out the input(Name, Description, Purpose) and click Create Project
3. If prompted to Move Resources into project, click Skip For Now
4. Click on the name of your new project on the top left hand side of the control panel
5. Now click on the Create drop down button on at the very top of your screen(on the right hand-ish side) and select Droplets
6. Leave the Choose an image option as the default(Ubuntu), scroll down and choose your desired size

##### Default image Ubuntu:
![alt text](https://i.imgur.com/zpC9ejm.png)


7. Next scroll down some more to the Choose a datacenter region section and choose the best location for you
8. Finally, scroll down a little more to Add your SSH keys and stop here. We will leave this open and finish in in the next section

##### Add your SSH Keys, stopping point:
![alt text](https://i.imgur.com/OKHFmxg.png)



***


## Create a SSH Key

##### SSH Keys are generated once per computer, only create one if you've never have before or had a key you know needs to be replaced


1. Check first if you have a key

```
cd ~/.ssh
ls
```

