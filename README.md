# node-red-contrib-alexa-remote2

![npm](https://img.shields.io/npm/v/node-red-contrib-alexa-remote2.svg) ![downloads](https://img.shields.io/npm/dt/node-red-contrib-alexa-remote2.svg)

This is a collection of Node-RED nodes for interacting with the Alexa API.
You can emulate routine behaviour, control and query your devices and much more!


**Note:** version 3 is an almost complete overhaul. **Only** the Alexa Account node configuration is compatible with version 2
All functionality is from [alexa-remote2](https://www.npmjs.com/package/alexa-remote2).
The goal is to expose all of [alexa-remote2](https://www.npmjs.com/package/alexa-remote2)s functionality in node-red nodes.

 - [Changelog](CHANGELOG.md)
 - [Examples](examples.md)

### **Setup**
1. Drag an **Alexa Routine** node into your flow.
2. Create a new Account by pressing the edit button at the right side of the *Account* field.
3. Choose a **Service Host** and **Page** and **Language** depending on your location. For example:

   |     | Service Host        | Page         | Language |
   |-----|---------------------|--------------|----------|
   | USA | pitangui.amazon.com | amazon.com   | en-US    |
   | UK  | alexa.amazon.co.uk  | amazon.co.uk | en-UK    |
   | GER | layla.amazon.de     | amazon.de    | de-DE    |
   
4. Set **This IP** to the ip of your Node-RED server
5. Set **Port** to a random port not in used. Do not use Node-Red port or home assistant port. Use one that is not in use.
6. Enter a **File Path** to save the authentication result so following authentications will be 
automatic. 
7. *Add* the new Account.
8. Deploy
9. Follow the url you see in the node status
10. Log in, wait until you see the node status **ready**
11. Write "Hello World!" in the *Alexa Routine* node text field.
12. Select a device in the *Alexa Routine* node devices field.

Now trigger the *Alexa Routine* Node with any message and your Alexa will say "Hello World!". (Hopefully!)
