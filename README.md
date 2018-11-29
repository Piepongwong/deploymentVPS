## Deployment with DigitalOcean

Digital ocean is a hosting company that offers Virtual Private Servers (VPS). A VPS feels and works just like a real server. It gives you complete control over an external computer via the terminal. After you connect to the VPS, you can execute commands on that computer as if it were yours. 

Sign up for Digital Ocean via [this link](https://m.do.co/c/40f2831c48f4) to receive $100 credit for 2 months. After that period a VPS costs $5 a month, but you're charged per hour. Therefore you can spin up projects, see if it works online and disable it again. You can host multiple projects on 1 server.

# Battle plan:
1. - [x] [create] (https://m.do.co/c/40f2831c48f4) a Digital Ocean account
2. - [ ] create a VPS in Digital Ocean
3. - [ ] connect to the VPS via the terminal with SSH
4. - [ ] install nodeJs and MongoDB on your server
5. - [ ] pull your project on the VPS using Git and Github and run it
6. - [ ] enjoy the beauty

## 1. Create a VPS in Digital Ocean

Log in to your account and click on the "Create" button. Select "Droplets" (Digital Ocean calls VPS's Droplets). Keep the distribution as Ubuntu and select the plan of 5 bucks a month. For now we don't want backups or block storage. Choose the datacenter region that is the closest to you. 

The next option deserves a separate paragraph. ;) It's time to add our **public** SSH key. This key will authenticate your computer. It ensures that only you have access to your VPS and you can connect to it without typing your password over and over again. Execute the following command in your terminal: <br>
```cat ~/.ssh/id_rsa.pub```<br>
The response should look something like this: <br>
```ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDCHJTQ570px3vhnVJrLAi9XQ1vR442ojPvPb9u+Ki9CbTF3LGm3WNfi1phkEo7Nn2+gqipZFAuqZVwrzMZVkLdJKr6IxmYNCA2SXedlUkXNftJx0Rzc0psgUh9DPUGwCoHRblZ5sIILQBCPCHtbUW7PssIfLklB/KN6yg+8QHBAJrgSV18XelMS1TI jurgen.tonneyck@ironhack.com```<br>
This is your public key. The `cat` command prints out text files in your terminal. In this case this text file your public ssh key. Note that we assume you already created your key pair. In case you didn't, follow [these steps](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys/create-with-openssh/). `~/.ssh` is the default location of the ssh keys. Your keys might be somewhere else. 

<span style="color:red">Never share your private key!</span>

Now in Digital Ocean you can click on "New SSH Key". Copy paste the key from your terminal to Digital Ocean. Name the key after the computer it belongs to, like 'personal mac'. Use your imagination.

1. - [x] create a VPS in Digital Ocean

## 3. Connect to the VPS via the terminal with SSH

After you've completed step 2, Digital Ocean will set up a VPS. This VPS has its own ip-address. Copy it from your droplet overview to your clipboard. Go to your terminal and type `ssh root@theipaddress". Of course "theipaddress" is a placeholder for your ip-address. <sub>(trust me, you will not believe what a teacher has to endure sometimes :p </sub>) . Wait whuut hooow, skrrrah, pap, pap, ka-ka-ka what happened?! Did I just turn into a hacker? YES, you did. Enjoy this moment. Reality will quickly catch up with you.

You're now inside the VPS! You can use all unix based commands that you're used to. Try out some, for example `cd /` and then `ls`. You can see the whole file structure of your very own server.

3. - [x] connect to the VPS via the terminal using SSH

## 4. Install nodeJs and MongoDB on your server

In your VPS dowload nodeJs with the following command: 
```curl -sL https://deb.nodesource.com/setup_10.x | bash -```
Now install it with: 
```apt-get install -y nodejs``` 
`apt-get` is Linux' package manager, NPM for an Operating System if you like. Verify your installation by typing `node --version`. If you get a response, it means you've installed nodeJs correctly.

MongoDB is next in line. MongoDB is already part of `apt-get`'s repositories. First update the repositories with 
```sudo apt update``` 
`sudo` stands for "super user do" and gives you admin privileges. 
![alt text](./sandwich.png)
Now install mongoDB with:
```sudo apt install -y mongodb```
The "-y" flag basically says yes to all options, similar clicking on "accept" while installing software with a graphical interface. Please be aware that you should read everything. It might contain valuable informati... Just kidding. Aint nobody got time for that. Verify your installation with `mongod --version`

4. - [x] install nodeJs and MongoDB on your server

## 5. Pull your project on the VPS using Git and Github and run it

Now it's almost business as usual. You've installed all necessary software on your new environment. Navigate to the home folder of your VPS and clone the project you want to host. There's one important difference with your local setup that we've to take into account before running `npm install` and `node nameofyourapp.js`. We are no longer listening port number 3000, but port on number 80. On servers port 3000 is blocked by default. 80 is the default port for websites in production. The proper way to change this is by setting up your environment/config variables. We save that for another lesson. The quick and dirty way is by using 
`sudo nano nameofyourapp.js`
Nano is a very simple terminal based text-editor. Locate the place where you've set your port and change it to 3000. In the bottom of your screen you'll find instructions how to exit nano ('^' stands for ctr/cmd). Now run your app as you would do normally.

- [x] pull your project on the VPS using Git and Github and run it

### 6. Enjoy the beauty
Copy paste the ip-address of your VPS in your browser. That's the same ip-address you've used to log in with ssh. In case you've forgot, go to the droplets dashboard in DigitalOcean. You do not have to specify the port, because if it's not specified, it takes port 80 by default. Voilà, ton site web. It's so fancy that I've start to speak french.  

1. - [x] [create a Digital Ocean account](https://m.do.co/c/40f2831c48f4)
2. - [x] create a VPS in Digital Ocean
3. - [x] connect to the VPS via the terminal with SSH
4. - [x] install nodeJs and MongoDB on your server
5. - [x] pull your project on the VPS using Git and Github and run it
6. - [x] enjoy the beauty
  
### Extra - setting up your port and other env vars the right way

[Install Filezilla](https://filezilla-project.org/) and connect to your server. Drag and drop your configuration file to your VPS.

Managing ports on your VPS with UFW (Uncomplicated Firewall). Type `man ufw` in your terminal for instructions. Try to connect with mongodb on your VPS using Compass. You also have to change some settings in mongo.