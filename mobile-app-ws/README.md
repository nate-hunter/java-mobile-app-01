# PLAN FOR APP:
- User signs up/log in/log out
- User creates a profile
    - Selects a favorite NBA team
- User can view data visualizations of all NBA teams
- User can edit/update team
    
## Maven:
$ cd "C:\Java-nh\Projects\java-mobile-app\20190924\mobile-app-ws"
$ ls
$ mvn install

// TO RUN PROGRAM W/MAVEN
$ mvn spring-boot:run

// TO RUN JAR FILE AS A STANDALONE JAVA APPLICATION TO UPLOAD TO A REMOTE SERVER
$ cd target
$ cp mobile-app-ws-0.0.1-SNAPSHOT.jar "C:\Users\laway\Desktop"
$ java -jar mobile-app-ws-0.0.1-SNAPSHOT.jar

## Summary of Running Web Services App:
1. Build the project with `mvn install` command
2. Upload the deployable `.jar` file to a production server
3. Run application with `java -jar <file name>` command

// WAR IMPLEMENTATION:
$ cd "C:\Java-nh\Projects\java-mobile-app\20190924\mobile-app-ws"
$ mvn clean
$ mvn install

// TOMCAT SERVER:
$ cd ~/Desktop/apache-tomcat-9.0.26/bin
$ ./startup.sh (if get the message "Permission denied", run `$chmod a+x *.sh`)

*/* Navigate to `localhost:8080` to confirm if Apache Tomcat is running
*/* SIGN UP new Apache Tomcat user name and password
*/* In 'Tomcat Web Application Manager' **UPLOAD** .war file and **DEPLOY**

// AWS: CONNECTING TO SERVER VIA SSH
$ cd "/c/Java-nh/Projects/java-mobile-app/AWS Key Pair"
$ ssh -i MobileAppEC2Server.pem ec2-user@ec2-3-14-126-142.us-east-2.compute.amazonaws.com
*/* TO CHECK WHICH VERSION JAVA USING - WANT TO USE JAVA 8
$ java -version
*/* TO SELECT java-1.8.0 (IF INSTALLED)
$ sudo /usr/sbin/alternatives --config java
=> SELECT '2'
$ sudo /usr/sbin/alternatives --config javac


// DOWNLOAD AND INSTALL APACHE TOMCAT ON AWS EC2 LINUX SERVER
$ yum list tomcat*
$ sudo yum install tomcat8
$ sudo yum install tomcat8-admin-webapps
$ sudo service tomcat8 start
$ sudo service tomcat8 stop

// CONFIGURE TOMCAT USERS
$ whereis tomcat8
$ cd /usr/share/tomcat8
$ cd conf/ (TO LOCATE `tomcat-users.xml`)
$ sudo vi tomcat-users.xml
*/* EDIT:   [TO BEGIN EDITING: PRESS "o" | TO EXIT VI: "Esc" >> ":wq"]
    <role rolename="manager-gui"/>
    <user username="tomcat" password="s3cret" roles="manager-gui"/>
 */* TO APPLY CHANGES, RESTART SERVER:
 $ sudo service tomcat8 restart
 
// IF GETTING 403 ERROR, INSERT:
*/* Tomcat Home ▸ webapps ▸ manager ▸ META-INF:
   <Context privileged="true" antiResourceLocking="false"
        docBase="${catalina.home}/webapps/manager">
        <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
    </Context>
    
    // ORIGINAL:
    <Context antiResourceLocking="false" privileged="true" >
      <Valve className="org.apache.catalina.valves.RemoteAddrValve"
             allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
      <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?:\$1)?|java\.util\.(?:Linked)?HashMap"/>
    </Context>

// DOWNLOAD AND INSTALL MYSQL SERVER on EC2 LINUX SERVER
$ sudo yum install mysql-server
*/* TO START:
$ sudo service mysqld start
*/* TO CHECK STATUS:
$ sudo service mysqld status
*/* TO CONFIGURE MYSQL:
$ sudo /usr/bin/mysql_secure_installation
=> SET PASSWORD: NHmy...
*/* TO LOGIN:
$ mysql -u root -p
*/* CAN NOW RUN COMMANDS, eg:
mysql> show databases;
mysql> create database mobile_app;
mysql> create user 'njh'@'localhost' identified by 'NJHawsmy...';
mysql> grant all privileges on mobile_app.* to 'njh';
mysql> flush privileges;
mysql> exit
*/* TO SIGN IN WITH NEW USER CREDENTIALS:
$ mysql -u njh -p
=> ENTER PASSWORD
mysql> show databases;

// DEPLOY THE WEB SERVICE APP ON APACHE TOMCAT:
*/* IN PROJECT DIRECTORY:
$ mvn install




// THE END //