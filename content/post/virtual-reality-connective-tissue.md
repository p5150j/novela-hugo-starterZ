---
timeToRead: 5
authors:
- Patrick Ortell
title: Virtual Reality Connective Tissue
excerpt: 'Virtual Reality Connective Tissue is a project controlling micro controllers
  in the real world from within virtual reality '
date: 2022-04-06T06:00:00+00:00
hero: "/images/150306532-bf11af13-1b0a-4d2d-97e4-647b6105a7b3.gif"

---
### Abstract:

As the world, our devices, and our attention spans get smaller our needs to fill that void with consumerism, laziness, and gluttony get stronger. We have all dreamed of a dystopian future like wall-e, minority report, ready player one, and alike wherein human-computer interfaces have evolved into more of an extension of our physical selves. On the more dramatic level, we have even seen a subculture starting to do bio-hacking and implementing RFID chips into their bodies much like implanted keyfobs.

![](/images/yoal-desurmont-nschnjdtose-unsplash.jpg)

Without getting off track too much... we all have a flavor of this rabbit hole we could go down... but this brings me to my first question.

### Question:

Is XR the next step closer to these worlds of dreams and nightmares? We have all seen, if not owned an Oculus, HoloLens, MagicLeap, and soon Apple glass & VR devices. At the very least Augmented reality has touched your life in some small way by seeing how a product would look in your house via an overlay on your smartphone camera.

But all of these devices are only scratching the surface (industrial or commercial) they are all still presenting us with a new way to consume media types... we can now interact with them with hand tracking and they have opened new doors to how we consume and interact with content... but I have yet to see anyone doing anything wherein we can connect the 2 worlds and bring us closer to that human-computer interface.

![](/images/possessed-photography-ykw0jjp7rlu-unsplash.jpg)

* What if we could interact with a virtual world in a way that changed the tangible world around us?
* With a swipe of my hand, I could turn on my stove and adjust the timer and burner heat with a slide and tab of an index finger?
* Could I do highly technical work in a nuclear power plant that isn't safe for humans and cant be automated from 10k miles away?

> ## _How do we start?_

#### Human virtual touch GPIO translation

Make a simple light turn on and off in the real world from an event we take in the virtual world. What would we need to do this?

###### For this we will need 4 things:

* Some buttons in a virtual world
* A way for the user to interact with the buttons
* A way for the buttons to fire events and communicate with an external real-world device (rest API)
* A 2nd device in the real world to consume and respond to our virtual events

#### Buttons and firing events

Now that we have our buttons in Unity let's connect them to publishing events that another device can subscribe to. For this, we can use a REST API and POST data using 2 functions TurnLightOn() and TurnLightOff().

```js  
...
  using Models;
  using Proyecto26;
  using UnityEngine.Networking;
  
  private RequestHelper currentRequest;
  
  private void LogMessage(string title, string message) {
    Debug.Log(message);
  }
  
  public void TurnLightOn() {
    currentRequest = new RequestHelper {
      Uri = "http://10.0.0.188:8888/relays/3",
        Body = new Post {
          state = true,
        },
        EnableDebug = true
    };
    RestClient.Post < Post > (currentRequest)
      .Then(res => {
          RestClient.ClearDefaultParams();
        this.LogMessage("Success", JsonUtility.ToJson(res, true));
      })
      .Catch(err => this.LogMessage("Error", err.Message));
  }
  
  public void TurnLightOff() {
    currentRequest = new RequestHelper {
      Uri = "http://10.0.0.188:8888/relays/3",
        Body = new Post {
          state = false,
        },
        EnableDebug = true
    };
    RestClient.Post < Post > (currentRequest)
      .Then(res => {
          RestClient.ClearDefaultParams();
        this.LogMessage("Success", JsonUtility.ToJson(res, true));
      })
      .Catch(err => this.LogMessage("Error", err.Message));
  }
```

#### Raspberry pi

The first thing we need to do on an external device is to connect an electrical relay to a light bulb and then have the Raspberry pi in between them. Here is a crude drawing of the connections.

![](https://user-images.githubusercontent.com/444888/150848618-47cad787-bd35-4fe3-ac95-0a8eead031db.jpeg)

![](https://user-images.githubusercontent.com/444888/150307233-bdf7d046-8547-4195-9ed6-73dbd185a517.jpg)

Cool now that that's all set up let's write some code and get a node server running with a REST API to toggle the relay values. On the Raspberry pi make sure you have node installed and you create a server.js file.

```js
sudo sucurl -fsSL https://deb.nodesource.com/setup_17.x | bash -
sudo apt install nodejs

cd into a dir/you/want
touch server.js
```

Now let's make our server that will consume the VR events and toggle the lights

```js
    const fs = require('fs');
    const http = require('http');
    const gpio = require('onoff').Gpio;
    
    const relays = [
      new gpio(26, 'out'),
      new gpio(20, 'out'),
      new gpio(21, 'out')
    ];
    
    const allRelaysOff = () => {
      relays.forEach(relay => relay.writeSync(0));
    };
    
    const relayServer = (request, response) => {
      let requestBody = '';
    
      request.on('data', chunk => {
        requestBody = `${requestBody}${chunk.toString()}`;
      });
    
      request.on('end', () => {
        // Check request method is valid.
        if (!['GET', 'POST'].includes(request.method)) {
          response.writeHead(500);
          response.end('Bad request.');
          return;
        }
    
        if (request.url === '/') {
          console.log('Home page requested.');
          fs.readFile('index.html', (error, content) => {
            response.writeHead(200, { 'Content-Type': 'text/html' });
            response.end(content, 'utf-8');
          });
    
          return;
        }
    
        if (['/relays/1', '/relays/2', '/relays/3'].includes(request.url)) {
          response.writeHead(200);
          let relayNumber = parseInt(
            request.url.substring(request.url.length - 1),
            10
          );
    
          // Take 1 off of relayNumber as arrays are indexed.
          relayNumber = relayNumber - 1;
    
          if (request.method === 'POST') {
            // Parse the request body JSON.
            try {
              const r = JSON.parse(requestBody);
    
              if (r.state === true) {
                relays[relayNumber].writeSync(1);
                console.log(`Switched relay ${relayNumber} on.`);
              } else if (r.state === false) {
                relays[relayNumber].writeSync(0);
                console.log(`Switched relay ${relayNumber} off.`);
              } else {
                response.writeHead(500);
                response.end('Bad request.');
                return;
              }
            } catch (e) {
              response.writeHead(500);
              response.end('Bad request.');
              return;
            }
          }
    
          // Return true if the relay is on, otherwise false.
          response.end(relays[relayNumber].readSync() === 1 ? 'true' : 'false');
          return;
        } else {
          // If we get to here, we have an unknown request.
          response.writeHead(404);
          response.end('Not found.');
        }
      });
    };
    
    // Turn off all relays on start up.
    allRelaysOff();
    
    // Create a web server and listen on 8888.
    http.createServer(relayServer).listen(8888);
    
    // Handle Ctrl+C exit cleanly by turning off all relays.
    process.on('SIGINT', () => {
      allRelaysOff();
      process.exit();
    });
```

![](https://user-images.githubusercontent.com/444888/150306562-a3c2f98e-9790-49e3-8add-ea4a5c51793b.png)

Using a tool like[ Postman to test the API](https://www.postman.com/) you can debug and make sure your events are being fired correctly and simulate the payloads coming from the VR device.

![](https://user-images.githubusercontent.com/444888/150306592-528281ac-6e14-4c7f-867c-88d9ba7be310.png)

After it's been tested and you are ready, start the VR project on the HMD, and boom!

![](/images/150306532-bf11af13-1b0a-4d2d-97e4-647b6105a7b3.gif)

### 