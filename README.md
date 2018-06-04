# Shiny Dashboards
In industry there will be a lot of operations to perform and monitor. In each and every process there will be data which obtained from sensors and that data will be stacked in database. Here our motivation of this project is to analyze that data and help people to take decisions in performing operations. 

Dashbords will be installed in firm's database and data will be directly derouted to dashboards.

Here we designed three dashboards by targeting various aspects.
1. Real-Time Analysis Dashboard
2. Offline Analysis Dashboard
3. Production Dashboard

# **Real-Time Analysis Dashboard:** 

Dashboard Documentation: https://docs.google.com/document/d/1p0Zkw4aBPcuu0tzuqkSxLxC7uTgn2IAB2l3KypZPQFg/edit?usp=sharing

Dashboard Link:  https://tiproject.shinyapps.io/Deploymentr/

In this one data will be analyzed in Real time for every 1 min (data will be refreshed for every 1 min). So we can see the data shiftwise and hourwise in a particular day (This dashboard designed for only a day).We give realtime alerts in dashbord to take furthur action also we can send SMS or mail to people who should take care of the firm.

# **Offline Analysis Dashboard:**

Dashboard Documentation : https://docs.google.com/document/d/1N7dH1Ykp5382dtHkLq8zmhrc3hs2WyEcUcMm_etdg4Y/edit?usp=sharing

Dashboard Link: https://tiproject.shinyapps.io/quality_dashboard/

This dashboard will have connection to entire data which presented in database. So, we can choose data and can see trends in last 6 months or one year and so on (There will be a date range button we need to choose from that).

# **Production Dashboard:**

Dashboard Documentation : https://docs.google.com/document/d/18yTxLrfZAhvYL9pG_8Ww1mtQbJ1X6JWdVr6VI_b6nTo/edit?usp=sharing

Dashboard Link:  https://tiproject.shinyapps.io/PDashboard/

This dashboard also takes data in realtime. In this one mainly on production engineer perspective whereas other dashboards on quality engineers perspective. Here we can give production we are planning per day/ per week/ per month and actual production will be taken from data which is in database. We can have clear picture about actual and planned prodution deviation.

# **Installation of R, R studio server and Shiny server in Database:**

This tutorial helps to learn about deploying shiny apps in shiny server from scratch.

In this tutorial we will discuss about how to install R,Rstudio,Shiny server

This tutorial is based upon 64 bit ubuntu system.

# **Install R:**

Open termial in ubuntu and type the following: To ensure we get the most recent version of R, we need to first add xenial (our Ubuntu release name) to our sources.list:

`sudo sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" >> /etc/apt/sources.list'`

Now add public keys

`gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
gpg -a --export E084DAB9 | sudo apt-key add -`

Now install R

`sudo apt-get update
sudo apt-get -y install r-base`

Now you should be able to run R by typing

`R`

Now quit R by typing quit() or open new terminal If you chose the weakest machine type, many packages won’t be able to install because of not enough memory. We need to add 1G of swap space:

`sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
sudo /sbin/mkswap /var/swap.1
sudo /sbin/swapon /var/swap.1
sudo sh -c 'echo "/var/swap.1 swap swap defaults 0 0 " >> /etc/fstab'`

Lets install some dependencies to run R

`sudo apt-get -y install libcurl4-gnutls-dev
sudo apt-get -y install libxml2-dev
sudo apt-get -y install libssl-dev`

# **Install Rstudio:**

Go back to terminal and type the following:

`sudo apt-get install gdebi-core
wget https://download1.rstudio.org/rstudio-1.0.44-amd64.deb
sudo gdebi rstudio-1.0.44-amd64.deb
rm rstudio-1.0.44-amd64.deb`

# **Install R packages:**

Open terminal and type the following commands

`sudo apt-get install openssl`

Some packages are available in github so install devtools to install packages from Github

`sudo su - -c "R -e \"install.packages('devtools', repos='http://cran.rstudio.com/')\""
sudo su - -c "R -e \"devtools::install_github('daattali/shinyjs')\""
sudo su - -c "R -e \"devtools::install_github('andrewsali/shinycssloaders')\""`

Open Rstudio and type the following commands in terminal

`install.packages(c("shiny","shinydashboard","ggplot2","plotly","lubridate","shinythemes","shinyjs","reshape","dplyr","tidyr","xts","pool","dplyr","shinyjs","xlsx","readxl","DT","pool","bubbles","shinySignals","plyr"))`

Install some packages from github

`devtools::install_github("jcheng5/bubbles")
devtools::install_github("hadley/shinySignals")`

If there are any problems install packages see "https://www.digitalocean.com/community/tutorials/how-to-install-r-packages-using-devtools-on-ubuntu-16-04"

To install rJava package: First install Java if it is not present

`sudo apt-get install default-jre`

Then install JDK

`sudo apt-get install default-jdk`

Then assotiate the JDK installed with R

`sudo R CMD javareconf`

Install RJava and Rgdal

`sudo apt-get install r-cran-rjava
sudo apt-get install libgdal1-dev libproj-dev`

Install package in RStudio: Open Rstudio and type

`install.packages("rJava")`

If you have any problems in installing java and configuring see https://poweruphosting.com/blog/install-java-ubuntu/ https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get

# **Installing Rstudio server:**

Lets install some pre-requisites

`sudo apt-get -y install libapparmor1 gdebi-core`

Now install Rstudio-server by typing in terminal

`wget https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb
sudo gdebi rstudio-server-1.1.383-amd64.deb`

By default Rstudio server uses port number 8787,so to acsess Rstudio type http://127.0.0.1:8787/ or networkip:8787. Network ip can be known by typing Hostname -I in terminal.

# **Install Shiny-server:**

First install shiny package

`sudo su - -c "R -e \"install.packages('shiny', repos='http://cran.rstudio.com/')\""`

To install shiny-server type

`wget https://download3.rstudio.org/ubuntu-12.04/x86_64/shiny-server-1.5.5.872-amd64.deb
sudo gdebi shiny-server-1.5.5.872-amd64.deb`

By default Shiny server uses port number 3838,so to acsess Shiny server type http://127.0.0.1:3838/ or networkip:3838. Network ip can be known by typing Hostname -I in terminal.

By diffault shiny apps are under folder /opt/shiny-server/samples/sample-apps in ubuntu. U can copy your app folder inside the sample-apps and you can acssess using http://172.17.15.13:3838/sample-apps/ . Replace 172.17.15.13 with your network-ip.

Befor copying the file to the sample-apps make sure that server,ui and global in a single file App.R

# **FAQ:**

1)If your app isnt runnig in after deployed in shiny-server then you can check the error in /var/log/shiny-server.log

2)If you get an error "Error getting worker; application exited during initialization" then got to

`sudo gedit /etc/systemd/system/shiny-server.service`

and add the following line

`[Service]
Environment="SHINY_LOG_LEVEL=TRACE"`

Commands to run for the changes to take effect:

`sudo systemctl stop shiny-server
sudo systemctl daemon-reload
sudo systemctl start shiny-server`

4)To give sudo permissions to a folder

sudo chmod -R 777 /var/DirectoryName

5)It error is unable to lock

`sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock`

6)To install RMySQL

`sudo apt-get install libdbd-mysql libmysqlclient-dev`

open R

`install.packages('RMySQL')`
