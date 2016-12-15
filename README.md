Drools on PCF simple example 
===

Create a  minimal Drools web service using Spring Boot. 

Rule shown : If the person is under 16 then they display a ChildBusPass, else a AdultBusPass. You can see the results here ( toggle 16 / 15 

https://drools1.cfapps.io/buspass?name=Steve&age=16

For the rules, I took my rules from the Bus Pass example in the JBPM project:

https://github.com/droolsjbpm/drools/tree/master/drools-examples/src/main/java/org/drools/examples/buspass

I have made the rules simple, and reduced the code by replacing some of the Java fact classes with DRL declared types. I prefer this for facts which are only referenced from within the DRL.

Build the application:

    mvn clean package

Run the application:

    java -jar target/buspass-ws-1.0.0-SNAPSHOT.jar
    
Run on PCF 

    cf push #### target/*.jar

Then send a request to the API using curl or your favourite web browser. As described by the rules, if you request a bus pass for a person with age less than 16, you should see a ChildBusPass and for someone 16 or over, you should see an AdultBusPass.

For example, opening http://127.0.0.1:8080/buspass?name=Steve&age=15 gives me: Rule 1
    
    {"person":{"name":"Steve","age":15},"busPassType":"ChildBusPass"}
    
... and opening http://127.0.0.1:8080/buspass?name=Steve&age=16 gives me: Rule 2 
    
    {"person":{"name":"Steve","age":16},"busPassType":"AdultBusPass"}

For How the DRL rules are configured, take a look at BusPass.drl udner Resources folder of the /SRC
