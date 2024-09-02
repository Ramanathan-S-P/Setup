# Logrotate
This ia a system utility that helps in compressing, logging and rotating log files of the system and application processes.
Every linux system have a utility called logrotate for this purpose and in this documentation we chose to focus more on creating custom logrotation process by configuring pm2-logrotate for nodejs apps and nginx logrotate.
#
## NGINX-Logrotate
When nginx server is installed in your machine there would be a default `nginx` logrotate configuration under the `etc/logrotate.d/`.Thus we can modify it so that it can  create log files if size of the file exceeds 20mb and retain files max of 14 days old.
### Custom Logrotate
```sh
sudo nano /etc/logrotate.d/nginx
```
Give the above command to navigate to the nginx's logrotate configuration file.<br>
You can see the following<br>

![NGINX's log rotation page](/resources/NGINX_LR.png)<br>

Here daily option specifies to create log file daily  thus change it to `size 20M`.
Also change the rotate option's value to 10 thus it retains files max of  10 days old.
### Verification
Dry run the nginx configuration page using the following command to verify if your changes are applied as intended.<br>
```sh
logrotate /etc.logrotate.d/nginx -d
```
<br>
<br>

![NGINX_CUSTOM_LR](/resources/NGINX_CUSTOM_LR.png)<br>

#
## PM2-Logrotate
Node js apps generally write their log in stdout and stderr files, Thus to log them based on necessities we neeed to make use of the pm2-logrotate tool to modify their logging behaviour
### Install PM2-logrotate
```sh
pm2 install pm2-logrotate
```
### Custom pm2-logrotate conf
We can make changes to the values of  options as needed using the <br>`pm2 set pm2-logrotate:<option> <value>` command.

```bash
pm2 set pm2-logrotate:max_size 20M
pm2 set pm2-logrotate:retain 10 
```
### Verify
```sh
pm2 show pm2-logrotate
```
In the output you can see the Process Configuration part that shows the logrotate configuration of pm2. If changes made it can be seen through this if applied or not.
<br>
<br>
![PM2_O/P](/resources/PM2_OP.png)

<br>

You can find the logfiles under `/home/user/.pm2/logs`

***To learn more about the logrotate options and value use the below given command.***
```sh 
man logrotate
```
