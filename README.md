# About
The Amazon Connect Chat javascript library (ChatJS) gives you the power to build your own chat widget to customize the chat experience. This can be used for both the end customer chat interface and the agent user interface, in conjunction with [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams).

For your reference, please refer to the [Chat UI reference implementation](https://github.com/amazon-connect/amazon-connect-chat-ui-examples). This will help you deploy an API Gateway and Lambda function for initiating chat from your webpage. From there you can use the ChatJS library to build a custom widget,

# Learn More
To learn more about Amazon Connect and its capabilities, please check out
the [Amazon Connect User Guide](https://docs.aws.amazon.com/connect/latest/userguide/).

# Chat Deep Dive
With the release of chat 

# Usage
Run the Makefile to generate `amazon-connect-chat.js`, then copy this file
into your application or host it in an Amazon S3 bucket behind Amazon Cloudfront.

```
$ make
```

## Getting Started
### Whitelisting


### Downloading ChatJS

```
$ git clone https://github.com/amazon-connect/amazon-connect-chatjs
```

Once you download ChatJS, change into the directory and build it:

```
$ cd amazon-connect-chatjs
$ make
```

This will generate a file called `amazon-connect-chat.js`, this is the full
Connect Chat API which you will want to include in your page.  You can serve
`amazon-connect-chatjs.js` with your web application.

### Build your own with NPM
Install latest LTS version of [NodeJS](https://nodejs.org)

```
$ git clone https://github.com/amazon-connect/amazon-connect-chatjs
$ cd amazon-connect-chatjs
$ npm install
$ gulp 
```

Find build artifacts in **release** directory -  This will generate a file called `amazon-connect-chat.js` and the minified version of the same `amazon-connect-chatjs-min.js` - this is the full Connect Streams API which you will want to include in your page.

## API Definition

### `chatSession.sendMessage`
`Method param:` args
```
args = {
    message: "string" //required: *yes*,* *min len: 1, max len: 1024
    contentType: "string", //required: *yes*, only valid string for message is text/plain
    metadata: 
}
```
`Exceptions:`
IllegalArgumentException
(API takes care of other exceptions)

### `chatSession.sendEvent`
`Method param:` args
```
args = {
    content: "string", //required: no, nullable, reserved for future use; // min len: 1, max len: 1024
    contentType: "string", //required: *yes*, custom type depicting chat events
             // supported types ->
             //  "application/vnd.amazonaws.connect.event.typing 
             // | "application/vnd.amazonaws.connect.event.participant.joined
             // | "application/vnd.amazonaws.connect.event.participant.left
             // | "application/vnd.amazonaws.connect.event.transfer.succeed
             // | "application/vnd.amazonaws.connect.event.transfer.failed
             // | "application/vnd.amazonaws.connect.event.chat.ended
             // *Must* be one of the above strings, or an IllegalArgumentException will be thrown
    metadata: //required: no
}
```
`Exceptions:`
IllegalArgumentException
(API takes care of other exceptions)

### `chatSession.getTranscript`
`Method param:` args
```
args = {
   contactId: "string" //min len: 1, max len:256, required: No
   maxResults: number, //required: no, Nullable, min:0, max: 100
   nextToken: "string", //required: no, min len:1, max len: 1000, 
   scanDirection: "string", //required: no, enum string to indicate FORWARD | BACKWARD
   sortOrder: "string", //required: no, enum string to indicate DESCENDING | ASCENDING
   startPosition: { // required: no
      id: "string", //min len: 1, max len:256
      mostRecent: number, // min:0, max: 100
      absoluteTime: "string" // String matching ISO 8601 format: "yyyy-MM-ddThh:mm:ssZ"
   }
   metadata: //required: no
} metadata: //required: no
```
`Exceptions:`
No Exceptions (API takes care of other exceptions)