# node-red-contrib-alexa-remote2

This is a collection of node-red nodes for interacting with alexa.
All functionality is from the great [alexa-remote2](https://www.npmjs.com/package/alexa-remote2).
The goal is to expose all of [alexa-remote2](https://www.npmjs.com/package/alexa-remote2)s functionality in node-red nodes.

[Changelog](CHANGELOG.md)

### Setup
1. Drag a **alexa sequence node** into your flow.
2. Create a new Account by pressing the edit button at the right side of the *Account* field.
3. Enter the **Cookie** or the **Email** and **Password** of your Amazon Alexa Account.
4. Choose a **Service Host** and **Page** depending on your location. For Example:

   ||Service Host|Page
   |---|---|---
   |USA|pitangui.amazon.com|amazon.com
   |UK|alexa.amazon.co.uk|amazon.co.uk
   |GER|layla.amazon.de|amazon.de
   
5. *Add* the new Account.
6. Enter the **Device** name (or Serial Number) of the target Alexa Device that is connected to your account.

Now trigger the Alexa Sequence Node with any message and your Alexa will say "Hello World!". (Hopefully!)

### Examples
To use the following examples you need to select your account for each of the *alexa remote nodes*, or modify the account that is already set for the nodes. All following examples depend on node-red-dashboard.

#### 1. Alexa Speak Simple Dashboard
Enter a phrase for Alexa to say on a chosen device.
```
[{"id":"de7f6276.2c32c","type":"ui_text_input","z":"6c4a7aff.92cf94","name":"","label":"","group":"f5f6c00c.16c28","order":1,"width":0,"height":0,"passthru":true,"mode":"text","delay":"1","topic":"","x":120,"y":160,"wires":[["ffbf475d.b10808"]]},{"id":"ffbf475d.b10808","type":"change","z":"6c4a7aff.92cf94","name":"","rules":[{"t":"set","p":"speakText","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":330,"y":160,"wires":[[]]},{"id":"5762364e.35ea58","type":"ui_button","z":"6c4a7aff.92cf94","name":"","group":"f5f6c00c.16c28","order":2,"width":0,"height":0,"passthru":false,"label":"Speak","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":110,"y":200,"wires":[["d5ce44e5.569f58"]]},{"id":"d5ce44e5.569f58","type":"alexa-remote-sequence","z":"6c4a7aff.92cf94","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","sequenceInputs":[{"command":"speak","value_type":"flow","value_value":"speakText"}],"x":340,"y":200,"wires":[[]]},{"id":"2196935a.a8600c","type":"change","z":"6c4a7aff.92cf94","name":"","rules":[{"t":"set","p":"device","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":480,"y":100,"wires":[[]]},{"id":"7c505cbc.615d74","type":"alexa-remote-get","z":"6c4a7aff.92cf94","name":"","account":"1374a985.bc9da6","target_type":"str","target_value":"devices","serialOrName_type":"str","serialOrName_value":"","options":{"devices":{},"cards":{"limit":{"type":"num","value":"10"},"beforeCreationTime":{"type":"str","value":"%t"}},"media":{},"playerInfo":{},"list":{"size":{"type":"num","value":"100"},"startTime":{"type":"str","value":""},"endTime":{"type":"str","value":""},"completed":{"type":"bool","value":"false"},"listType":{"type":"select","value":"TASK"}},"wakewords":{},"notifications":{"cached":{"type":"bool","value":"true"}},"doNotDisturb":{},"devicesNotificationState":{},"bluetooth":{"cached":{"type":"bool","value":"true"}},"activities":{"startTime":{"type":"str","value":""},"size":{"type":"num","value":"1"},"offset":{"type":"num","value":"1"}},"account":{},"conversations":{"latest":{"type":"bool","value":"true"},"includeHomegroup":{"type":"bool","value":"true"},"unread":{"type":"bool","value":"false"},"modifiedSinceDate":{"type":"str","value":"1970-01-01T00:00:00.000Z"},"includeUserName":{"type":"bool","value":"true"}},"automationRoutines":{"limit":{"type":"num","value":"2000"}},"musicProviders":{},"homeGroup":{},"devicePreferences":{},"smarthomeDevices":{},"smarthomeGroups":{},"smarthomeEntities":{},"smarthomeBehaviourActionDefinitions":{}},"x":330,"y":40,"wires":[["4daecd07.8870b4"]]},{"id":"51ca6c0f.bf4674","type":"inject","z":"6c4a7aff.92cf94","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"onceDelay":"0","x":130,"y":40,"wires":[["7c505cbc.615d74"]]},{"id":"4daecd07.8870b4","type":"change","z":"6c4a7aff.92cf94","name":"","rules":[{"t":"set","p":"options","pt":"msg","to":"payload.devices.accountName","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":140,"y":100,"wires":[["f82615ff.8f47a8"]]},{"id":"f82615ff.8f47a8","type":"ui_dropdown","z":"6c4a7aff.92cf94","name":"","label":"Device","place":"","group":"f5f6c00c.16c28","order":3,"width":0,"height":0,"passthru":true,"options":[{"label":"","value":"","type":"str"}],"payload":"","topic":"","x":310,"y":100,"wires":[["2196935a.a8600c"]]},{"id":"f5f6c00c.16c28","type":"ui_group","z":"","name":"Alexa Speak","tab":"e44a6ba2.3e2b08","order":1,"disp":true,"width":"6","collapse":false},{"id":"1374a985.bc9da6","type":"alexa-remote-account","z":"","name":"","bluetooth":true,"alexaServiceHost":"layla.amazon.de","userAgent":"","acceptLanguage":"","amazonPage":"amazon.de","initType":"lazy","useWsMqtt_type":"onoff","useWsMqtt_value":"on","bluetooth_type":"onoff","bluetooth_value":"on"},{"id":"e44a6ba2.3e2b08","type":"ui_tab","z":"","name":"Alexa Speak","icon":"speaker","order":2}]
```

#### 2. Alexa Speak List Dashboard:
In this example you can save phrases to be said.
And send them by clicking a button. You need to press the inject node under Create File before using it.
```
[{"id":"898032fd.85f24","type":"ui_text_input","z":"e7b2915c.e4c45","name":"","label":"","group":"eb8bd3d0.2ce6e","order":1,"width":0,"height":0,"passthru":true,"mode":"text","delay":"1","topic":"","x":380,"y":520,"wires":[["3312844.51b6a7c"]]},{"id":"3312844.51b6a7c","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"speakText","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":550,"y":520,"wires":[[]]},{"id":"973ac1c0.d882b","type":"ui_button","z":"e7b2915c.e4c45","name":"","group":"eb8bd3d0.2ce6e","order":3,"width":"3","height":"1","passthru":false,"label":"Test","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":390,"y":560,"wires":[["9f19dc42.fb8bc"]]},{"id":"e8ea2d46.47da7","type":"ui_template","z":"e7b2915c.e4c45","group":"8ed9eef4.04083","name":"","order":4,"width":"6","height":"10","format":"<div ng-repeat=\"text in msg.payload track by $index\" layout=\"row\">\n    <md-button style=\"background:transparent\"><ng-md-icon ng-click=\"send({indexToDelete:$index})\" style=\"stroke:#FFF;\" icon=\"delete\"></ng-md-icon></md-button>\n    <md-button flex style=\"padding:200px; margin: 5px;\" class=\"nr-dashboard-button\" ng-click=\"send({payload:text})\">{{text}}</md-button>\n</div>","storeOutMessages":false,"fwdInMessages":false,"templateScope":"local","x":420,"y":640,"wires":[["98f74e6d.75ae9"]]},{"id":"799b94f9.8e16ec","type":"inject","z":"e7b2915c.e4c45","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"onceDelay":0.1,"x":130,"y":320,"wires":[["d7f7fa9e.689f08"]]},{"id":"98f74e6d.75ae9","type":"switch","z":"e7b2915c.e4c45","name":"","property":"indexToDelete","propertyType":"msg","rules":[{"t":"istype","v":"undefined","vt":"undefined"},{"t":"istype","v":"number","vt":"number"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":640,"wires":[["3286c048.6d995","9090c51f.daa7b8"],["d577850c.f0cdb8","8be50957.fe7788"]]},{"id":"d577850c.f0cdb8","type":"debug","z":"e7b2915c.e4c45","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"indexToDelete","x":770,"y":660,"wires":[]},{"id":"9090c51f.daa7b8","type":"alexa-remote-sequence","z":"e7b2915c.e4c45","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","sequenceInputs":[{"command":"speak","value_type":"msg","value_value":"payload"}],"x":760,"y":560,"wires":[["2797506e.206ba"]]},{"id":"a502fbb3.ceca88","type":"ui_button","z":"e7b2915c.e4c45","name":"","group":"eb8bd3d0.2ce6e","order":2,"width":"3","height":"1","passthru":false,"label":"Add","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":110,"y":520,"wires":[["2ee032e2.3c09be"]]},{"id":"8be50957.fe7788","type":"file in","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","format":"utf8","chunk":false,"sendError":false,"x":170,"y":800,"wires":[["965d7479.206dd8"]]},{"id":"965d7479.206dd8","type":"json","z":"e7b2915c.e4c45","name":"","property":"payload","action":"","pretty":false,"x":110,"y":840,"wires":[["f1d9d5a7.9af4f8"]]},{"id":"f1d9d5a7.9af4f8","type":"function","z":"e7b2915c.e4c45","name":"remove at indexToDelete","func":"if(!Array.isArray(msg.payload))\n    return node.error('payload is not array');\n\nif(!Number.isInteger(msg.indexToDelete))\n    return node.error('index is no integer');\n\nmsg.payload.splice(msg.indexToDelete, 1);\nreturn msg;","outputs":1,"noerr":0,"x":170,"y":880,"wires":[["8846fdf7.6e9b2"]]},{"id":"d7f7fa9e.689f08","type":"file in","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","format":"utf8","chunk":false,"sendError":false,"x":170,"y":360,"wires":[["a6bc0f5e.6c201"]]},{"id":"a6bc0f5e.6c201","type":"json","z":"e7b2915c.e4c45","name":"","property":"payload","action":"","pretty":false,"x":110,"y":400,"wires":[["e8ea2d46.47da7"]]},{"id":"fb0243dc.a59ae","type":"comment","z":"e7b2915c.e4c45","name":"Removing Item","info":"","x":140,"y":760,"wires":[]},{"id":"8846fdf7.6e9b2","type":"file","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","appendNewline":false,"createDir":false,"overwriteFile":"true","x":170,"y":920,"wires":[["e8ea2d46.47da7"]]},{"id":"3286c048.6d995","type":"debug","z":"e7b2915c.e4c45","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","x":750,"y":620,"wires":[]},{"id":"2ee032e2.3c09be","type":"file in","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","format":"utf8","chunk":false,"sendError":false,"x":170,"y":560,"wires":[["78738910.a71808"]]},{"id":"78738910.a71808","type":"json","z":"e7b2915c.e4c45","name":"","property":"payload","action":"","pretty":false,"x":110,"y":600,"wires":[["6888a023.5d0bc"]]},{"id":"6888a023.5d0bc","type":"function","z":"e7b2915c.e4c45","name":"push flow.speakText","func":"if(!Array.isArray(msg.payload))\n    return node.error('payload is not array');\n\nmsg.payload.push(flow.get('speakText'));\nreturn msg;","outputs":1,"noerr":0,"x":160,"y":640,"wires":[["44b3ba.eae6bc48"]]},{"id":"44b3ba.eae6bc48","type":"file","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","appendNewline":false,"createDir":false,"overwriteFile":"true","x":170,"y":680,"wires":[["e8ea2d46.47da7"]]},{"id":"608b0725.5b4878","type":"comment","z":"e7b2915c.e4c45","name":"Adding Item","info":"","x":130,"y":480,"wires":[]},{"id":"6c2420f5.7eabb","type":"comment","z":"e7b2915c.e4c45","name":"Loading list","info":"","x":130,"y":280,"wires":[]},{"id":"7b554fc5.a5377","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"device","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":900,"y":60,"wires":[[]]},{"id":"600f461.c9f82b8","type":"alexa-remote-get","z":"e7b2915c.e4c45","name":"","account":"1374a985.bc9da6","target_type":"str","target_value":"devices","serialOrName_type":"str","serialOrName_value":"","options":{"devices":{},"cards":{"limit":{"type":"num","value":"10"},"beforeCreationTime":{"type":"str","value":"%t"}},"media":{},"playerInfo":{},"list":{"size":{"type":"num","value":"100"},"startTime":{"type":"str","value":""},"endTime":{"type":"str","value":""},"completed":{"type":"bool","value":"false"},"listType":{"type":"select","value":"TASK"}},"wakewords":{},"notifications":{"cached":{"type":"bool","value":"true"}},"doNotDisturb":{},"devicesNotificationState":{},"bluetooth":{"cached":{"type":"bool","value":"true"}},"activities":{"startTime":{"type":"str","value":""},"size":{"type":"num","value":"1"},"offset":{"type":"num","value":"1"}},"account":{},"conversations":{"latest":{"type":"bool","value":"true"},"includeHomegroup":{"type":"bool","value":"true"},"unread":{"type":"bool","value":"false"},"modifiedSinceDate":{"type":"str","value":"1970-01-01T00:00:00.000Z"},"includeUserName":{"type":"bool","value":"true"}},"automationRoutines":{"limit":{"type":"num","value":"2000"}},"musicProviders":{},"homeGroup":{},"devicePreferences":{},"smarthomeDevices":{},"smarthomeGroups":{},"smarthomeEntities":{},"smarthomeBehaviourActionDefinitions":{}},"x":330,"y":60,"wires":[["5b30513d.31569","2797506e.206ba"]]},{"id":"c926e98f.513238","type":"inject","z":"e7b2915c.e4c45","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"onceDelay":"0","x":130,"y":100,"wires":[["600f461.c9f82b8"]]},{"id":"5b30513d.31569","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"options","pt":"msg","to":"payload.devices.accountName","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":560,"y":60,"wires":[["82412fb.37915d"]]},{"id":"82412fb.37915d","type":"ui_dropdown","z":"e7b2915c.e4c45","name":"","label":"Device","place":"","group":"977902fd.7796a","order":1,"width":0,"height":0,"passthru":true,"options":[{"label":"","value":"","type":"str"}],"payload":"","topic":"","x":730,"y":60,"wires":[["7b554fc5.a5377"]]},{"id":"9f19dc42.fb8bc","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"speakText","tot":"flow"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":560,"wires":[["9090c51f.daa7b8"]]},{"id":"e5b2fd56.eea8e","type":"ui_template","z":"e7b2915c.e4c45","group":"167ceb0c.592785","name":"Status","order":0,"width":0,"height":0,"format":"<div style=\"margin:auto; margin-top:0;\" ng-bind-html=\"msg.payload\"></div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1110,"y":280,"wires":[[]]},{"id":"2797506e.206ba","type":"switch","z":"e7b2915c.e4c45","name":"","property":"error","propertyType":"msg","rules":[{"t":"istype","v":"object","vt":"object"},{"t":"istype","v":"undefined","vt":"undefined"}],"checkall":"true","repair":false,"outputs":2,"x":780,"y":280,"wires":[["bf562f00.1e99d"],["f35b6845.925b08"]]},{"id":"bf562f00.1e99d","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"error.message","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":940,"y":260,"wires":[["e5b2fd56.eea8e"]]},{"id":"f35b6845.925b08","type":"change","z":"e7b2915c.e4c45","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"Success","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":940,"y":300,"wires":[["e5b2fd56.eea8e"]]},{"id":"285d043c.fc0c6c","type":"ui_button","z":"e7b2915c.e4c45","name":"","group":"977902fd.7796a","order":4,"width":"0","height":"0","passthru":false,"label":"Refresh","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":120,"y":60,"wires":[["600f461.c9f82b8"]]},{"id":"e32745e7.9959e8","type":"inject","z":"e7b2915c.e4c45","name":"","topic":"","payload":"[]","payloadType":"json","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":470,"y":320,"wires":[["83a906c0.06f808"]]},{"id":"83a906c0.06f808","type":"file","z":"e7b2915c.e4c45","name":"","filename":"alexa-remote-speak.json","appendNewline":false,"createDir":false,"overwriteFile":"true","x":530,"y":360,"wires":[[]]},{"id":"9fda1bfb.f9d908","type":"comment","z":"e7b2915c.e4c45","name":"Create File","info":"","x":480,"y":280,"wires":[]},{"id":"eb8bd3d0.2ce6e","type":"ui_group","z":"","name":"Add Phrase","tab":"a33c95fe.e44598","order":2,"disp":true,"width":"6","collapse":false},{"id":"8ed9eef4.04083","type":"ui_group","z":"","name":"List","tab":"a33c95fe.e44598","order":3,"disp":true,"width":"6","collapse":false},{"id":"1374a985.bc9da6","type":"alexa-remote-account","z":"","name":"","bluetooth":true,"alexaServiceHost":"layla.amazon.de","userAgent":"","acceptLanguage":"","amazonPage":"amazon.de","initType":"lazy","useWsMqtt_type":"onoff","useWsMqtt_value":"on","bluetooth_type":"onoff","bluetooth_value":"on"},{"id":"977902fd.7796a","type":"ui_group","z":"","name":"Choose Device","tab":"a33c95fe.e44598","order":1,"disp":true,"width":"6","collapse":false},{"id":"167ceb0c.592785","type":"ui_group","z":"","name":"Status","tab":"a33c95fe.e44598","disp":true,"width":"6","collapse":false},{"id":"a33c95fe.e44598","type":"ui_tab","z":"","name":"Alexa Speak Advanced","icon":"speaker","order":3}]
```

#### 3. Alexa Music Dashboard:
Dashboard where you can enter a query for music to be played from a chosen provider on a chosen device.
You can also pause, resume and change the volume, toggle repeat and toggle shuffle.
```
[{"id":"973c7e19.b17b3","type":"ui_dropdown","z":"8952f023.eb17","name":"","label":"Provider","place":" ","group":"42ad2772.9b9cc8","order":2,"width":0,"height":0,"passthru":true,"options":[{"label":"","value":"","type":"str"}],"payload":"","topic":"","x":300,"y":340,"wires":[["5c47a5f9.bc9b6c"]]},{"id":"cb357910.eaf2f8","type":"alexa-remote-action","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","target_type":"select","target_value":"playMusicProvider","serialOrName_type":"flow","serialOrName_value":"device","options":{"checkAuthentication":{},"createNotification":{"type":{"type":"str","value":"Alarm"},"label":{"type":"str","value":""},"value":{"type":"str","value":"2019-01-01T00:00:00"},"status":{"type":"str","value":"ON"},"sound":{"type":"str","value":""}},"deleteNotification":{"id":{"type":"str","value":""}},"tuneinSearch":{"query":{"type":"str","value":""}},"findDevice":{},"renameDevice":{"newName":{"type":"str","value":""}},"deleteDevice":{},"executeAutomationRoutine":{"automationId":{"type":"str","value":""}},"playMusicProvider":{"providerId":{"type":"flow","value":"musicProvider"},"searchPhrase":{"type":"flow","value":"musicQuery"}},"sendTextMessage":{"conversationId":{"type":"str","value":""},"text":{"type":"str","value":""}},"deleteSmarthomeDevice":{"smarthomeDevice":{"type":"str","value":""}},"deleteSmarthomeGroup":{"smarthomeGroup":{"type":"str","value":""}},"deleteAllSmarthomeDevices":{},"discoverSmarthomeDevice":{},"querySmarthomeDevices":{"applicanceIds":{"type":"str","value":""},"entityType":{"type":"str","value":""}},"connectBluetooth":{"address":{"type":"str","value":""}},"unpaireBluetooth":{"address":{"type":"str","value":""}},"disconnectBluetooth":{"address":{"type":"str","value":""}}},"x":310,"y":500,"wires":[["1cbfbccf.8de253"]]},{"id":"5c47a5f9.bc9b6c","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"musicProvider","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":340,"y":380,"wires":[[]]},{"id":"da2e7bd4.5f4b28","type":"ui_button","z":"8952f023.eb17","name":"","group":"42ad2772.9b9cc8","order":5,"width":"3","height":"1","passthru":false,"label":"Play","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":110,"y":500,"wires":[["cb357910.eaf2f8"]]},{"id":"a0df016b.ffc6","type":"ui_text_input","z":"8952f023.eb17","name":"","label":"","group":"42ad2772.9b9cc8","order":3,"width":0,"height":0,"passthru":true,"mode":"text","delay":300,"topic":"","x":120,"y":440,"wires":[["e46c4f81.8ca15"]]},{"id":"e46c4f81.8ca15","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"musicQuery","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":320,"y":440,"wires":[[]]},{"id":"a0c75b7d.2bd828","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"pause","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"num","value":"50"}},"shuffle":{"value":{"type":"bool","value":"true"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":330,"y":540,"wires":[["1cbfbccf.8de253"]]},{"id":"1a9775ab.931b0a","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"device","pt":"flow","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":320,"y":180,"wires":[[]]},{"id":"69281b57.4fcba4","type":"ui_button","z":"8952f023.eb17","name":"","group":"447b35db.86ebac","order":1,"width":"3","height":"1","passthru":false,"label":"Pause","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":110,"y":540,"wires":[["a0c75b7d.2bd828"]]},{"id":"eefb4c6f.2a38a","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"play","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"num","value":"50"}},"shuffle":{"value":{"type":"bool","value":"true"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":330,"y":580,"wires":[["1cbfbccf.8de253"]]},{"id":"f32469e5.830928","type":"ui_button","z":"8952f023.eb17","name":"","group":"447b35db.86ebac","order":2,"width":"3","height":"1","passthru":false,"label":"Resume","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":120,"y":580,"wires":[["eefb4c6f.2a38a"]]},{"id":"8f693e0f.77968","type":"ui_slider","z":"8952f023.eb17","name":"","label":"Volume","group":"447b35db.86ebac","order":3,"width":0,"height":0,"passthru":true,"outs":"end","topic":"","min":0,"max":"100","step":1,"x":120,"y":620,"wires":[["5763919f.4e1ae"]]},{"id":"5763919f.4e1ae","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"volume","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"msg","value":"payload"}},"shuffle":{"value":{"type":"bool","value":"true"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":330,"y":620,"wires":[["1cbfbccf.8de253"]]},{"id":"fd75715f.b0d2a","type":"alexa-remote-get","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","target_type":"str","target_value":"devices","serialOrName_type":"str","serialOrName_value":"","options":{"devices":{},"cards":{"limit":{"type":"num","value":"10"},"beforeCreationTime":{"type":"str","value":"%t"}},"media":{},"playerInfo":{},"list":{"size":{"type":"num","value":"100"},"startTime":{"type":"str","value":""},"endTime":{"type":"str","value":""},"completed":{"type":"bool","value":"false"},"listType":{"type":"select","value":"TASK"}},"wakewords":{},"notifications":{"cached":{"type":"bool","value":"true"}},"doNotDisturb":{},"deviceNotificationState":{},"bluetooth":{"cached":{"type":"bool","value":"true"}},"activities":{"startTime":{"type":"str","value":""},"size":{"type":"num","value":"1"},"offset":{"type":"num","value":"1"}},"account":{},"conversations":{"latest":{"type":"bool","value":"true"},"includeHomegroup":{"type":"bool","value":"true"},"unread":{"type":"bool","value":"false"},"modifiedSinceDate":{"type":"str","value":"1970-01-01T00:00:00.000Z"},"includeUserName":{"type":"bool","value":"true"}},"automationRoutines":{"limit":{"type":"num","value":"2000"}},"musicProviders":{},"homeGroup":{},"devicePreferences":{},"smarthomeDevices":{},"smarthomeGroups":{},"smarthomeEntities":{},"smarthomeBehaviourActionDefinitions":{}},"x":330,"y":60,"wires":[["6e5e03c0.38139c","1cbfbccf.8de253"]]},{"id":"ffc106.2dc36ef8","type":"inject","z":"8952f023.eb17","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"onceDelay":"0","x":110,"y":100,"wires":[["fd75715f.b0d2a","583e85ee.9be71c"]]},{"id":"6e5e03c0.38139c","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"options","pt":"msg","to":"payload.devices.accountName","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":320,"y":100,"wires":[["f48d91b.300097"]]},{"id":"f48d91b.300097","type":"ui_dropdown","z":"8952f023.eb17","name":"","label":"Device","place":" ","group":"42ad2772.9b9cc8","order":1,"width":0,"height":0,"passthru":true,"options":[{"label":"","value":"","type":"str"}],"payload":"","topic":"","x":290,"y":140,"wires":[["1a9775ab.931b0a"]]},{"id":"583e85ee.9be71c","type":"alexa-remote-get","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","target_type":"str","target_value":"musicProviders","serialOrName_type":"str","serialOrName_value":"","options":{"devices":{},"cards":{"limit":{"type":"num","value":"10"},"beforeCreationTime":{"type":"str","value":"%t"}},"media":{},"playerInfo":{},"list":{"size":{"type":"num","value":"100"},"startTime":{"type":"str","value":""},"endTime":{"type":"str","value":""},"completed":{"type":"bool","value":"false"},"listType":{"type":"select","value":"TASK"}},"wakewords":{},"notifications":{"cached":{"type":"bool","value":"true"}},"doNotDisturb":{},"devicesNotificationState":{},"bluetooth":{"cached":{"type":"bool","value":"true"}},"activities":{"startTime":{"type":"str","value":""},"size":{"type":"num","value":"1"},"offset":{"type":"num","value":"1"}},"account":{},"conversations":{"latest":{"type":"bool","value":"true"},"includeHomegroup":{"type":"bool","value":"true"},"unread":{"type":"bool","value":"false"},"modifiedSinceDate":{"type":"str","value":"1970-01-01T00:00:00.000Z"},"includeUserName":{"type":"bool","value":"true"}},"automationRoutines":{"limit":{"type":"num","value":"2000"}},"musicProviders":{},"homeGroup":{},"devicePreferences":{},"smarthomeDevices":{},"smarthomeGroups":{},"smarthomeEntities":{},"smarthomeBehaviourActionDefinitions":{}},"x":350,"y":220,"wires":[["462acb9d.89b1b4","1cbfbccf.8de253"]]},{"id":"462acb9d.89b1b4","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"options","pt":"msg","to":"payload.id","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":320,"y":260,"wires":[["bd980a15.bf4488"]]},{"id":"bd980a15.bf4488","type":"function","z":"8952f023.eb17","name":"pretty label","func":"let prettify = s => {\n\ts = s.replace('_', ' ');\n\ts = s.toLowerCase();\n\ts = s.split(' ').map(w => w[0].toUpperCase() + w.slice(1)).join(' ');\n\treturn s;\n};\n\nmsg.options = msg.options.map(o => {\n    let obj = {};\n    obj[prettify(o)] = o;\n    return obj;\n});\n\nreturn msg;","outputs":1,"noerr":0,"x":310,"y":300,"wires":[["973c7e19.b17b3"]]},{"id":"9f5154aa.7af2b8","type":"ui_template","z":"8952f023.eb17","group":"447b35db.86ebac","name":"Repeat","order":4,"width":"2","height":"1","format":"<div style=\"margin:auto;\">Repeat</div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":120,"y":680,"wires":[[]]},{"id":"c349e34e.fb2d3","type":"ui_button","z":"8952f023.eb17","name":"Repeat On","group":"447b35db.86ebac","order":5,"width":"2","height":"1","passthru":false,"label":"On","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":290,"y":680,"wires":[["2ecf5373.a30bac"]]},{"id":"7e659479.0f3f7c","type":"ui_button","z":"8952f023.eb17","name":"Repeat Off","group":"447b35db.86ebac","order":6,"width":"2","height":"1","passthru":false,"label":"Off","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":290,"y":720,"wires":[["94cd7c4f.c3cd6"]]},{"id":"2ecf5373.a30bac","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"repeat","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"msg","value":"payload"}},"shuffle":{"value":{"type":"bool","value":"true"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":490,"y":680,"wires":[["1cbfbccf.8de253"]]},{"id":"94cd7c4f.c3cd6","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"repeat","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"msg","value":"payload"}},"shuffle":{"value":{"type":"bool","value":"false"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":490,"y":720,"wires":[["1cbfbccf.8de253"]]},{"id":"dee91660.17b7a8","type":"ui_template","z":"8952f023.eb17","group":"447b35db.86ebac","name":"Shuffle","order":7,"width":"2","height":"1","format":"<div style=\"margin:auto;\">Shuffle</div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":110,"y":760,"wires":[[]]},{"id":"2ab2c8d1.5f2d58","type":"ui_button","z":"8952f023.eb17","name":"Shuffle On","group":"447b35db.86ebac","order":8,"width":"2","height":"1","passthru":false,"label":"On","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":290,"y":760,"wires":[["2b761ef4.3ded82"]]},{"id":"d6200b14.9d0fa8","type":"ui_button","z":"8952f023.eb17","name":"Shuffle Off","group":"447b35db.86ebac","order":9,"width":"2","height":"1","passthru":false,"label":"Off","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":290,"y":800,"wires":[["1ff3bbac.ad6174"]]},{"id":"2b761ef4.3ded82","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"shuffle","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"msg","value":"payload"}},"shuffle":{"value":{"type":"bool","value":"true"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":490,"y":760,"wires":[["1cbfbccf.8de253"]]},{"id":"1ff3bbac.ad6174","type":"alexa-remote-command","z":"8952f023.eb17","name":"","account":"1374a985.bc9da6","serialOrName_type":"flow","serialOrName_value":"device","command_type":"select","command_value":"shuffle","options":{"play":{},"pause":{},"next":{},"previous":{},"forward":{},"rewind":{},"volume":{"value":{"type":"msg","value":"payload"}},"shuffle":{"value":{"type":"bool","value":"false"}},"repeat":{"value":{"type":"bool","value":"true"}}},"x":490,"y":800,"wires":[["1cbfbccf.8de253"]]},{"id":"f6f24db0.e80e5","type":"ui_template","z":"8952f023.eb17","group":"e254266d.22cb48","name":"Status","order":0,"width":0,"height":0,"format":"<div style=\"margin:auto; margin-top:0;\" ng-bind-html=\"msg.payload\"></div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":990,"y":460,"wires":[[]]},{"id":"1cbfbccf.8de253","type":"switch","z":"8952f023.eb17","name":"","property":"error","propertyType":"msg","rules":[{"t":"istype","v":"object","vt":"object"},{"t":"istype","v":"undefined","vt":"undefined"}],"checkall":"true","repair":false,"outputs":2,"x":660,"y":460,"wires":[["1f92cb4.f11dd35"],["d50170c9.ccba"]]},{"id":"1f92cb4.f11dd35","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"error.message","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":820,"y":440,"wires":[["f6f24db0.e80e5"]]},{"id":"d50170c9.ccba","type":"change","z":"8952f023.eb17","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"Success","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":820,"y":480,"wires":[["f6f24db0.e80e5"]]},{"id":"980c674e.e43948","type":"ui_button","z":"8952f023.eb17","name":"","group":"42ad2772.9b9cc8","order":4,"width":"3","height":"1","passthru":false,"label":"Refresh","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":120,"y":60,"wires":[["fd75715f.b0d2a","583e85ee.9be71c"]]},{"id":"42ad2772.9b9cc8","type":"ui_group","z":"","name":"Choose","tab":"1e5180a7.dddf8f","order":1,"disp":true,"width":"6","collapse":false},{"id":"1374a985.bc9da6","type":"alexa-remote-account","z":"","name":"","bluetooth":true,"alexaServiceHost":"layla.amazon.de","userAgent":"","acceptLanguage":"","amazonPage":"amazon.de","initType":"lazy","useWsMqtt_type":"onoff","useWsMqtt_value":"on","bluetooth_type":"onoff","bluetooth_value":"on"},{"id":"447b35db.86ebac","type":"ui_group","z":"","name":"Controls","tab":"1e5180a7.dddf8f","order":2,"disp":true,"width":"6","collapse":false},{"id":"e254266d.22cb48","type":"ui_group","z":"","name":"Status","tab":"1e5180a7.dddf8f","disp":true,"width":"6","collapse":false},{"id":"1e5180a7.dddf8f","type":"ui_tab","z":"","name":"Alexa Music","icon":"music_note","order":1}]
```
