# AskMeAnything bot
Bot ask for asking me anything. (Smooch.io + Dialogflow + GitHub Issues + Node.js)

Test the bot here: https://mycaule.github.io/ama-bot/

![screenshot](images/screenshot.png)

Proof of concept of a chatbot with integrated backoffices:
 - Dialogflow for user intent configuration,
 - GitHub issues for fallbacks.

## Setup

Fill in the secrets file with API keys `config/secrets.json`.

```
npm install
nodemon app.js
ngrok http 3000
```

Configure the following two Smooch integration in their web interface:
- Web messenger
- Webhooks

## Deploy with Docker

See [Dockerizing a Node.js web app](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/).

```
# Rebuilding the image
docker build -t mycaule/ama-bot .
```

```
# Pulling existing build from docker.io
docker pull mycaule/ama-bot

# Listing images
docker images

# Create secrets.json locally
vi config/secrets.json

# Running the image with a redirection to local port 8080
docker run -p 8080:3000 -v <full path to config>/secrets.json:/usr/src/app/config/secrets.json -d mycaule/ama-bot

# Listing docker processes
docker ps

# Printing app output
docker logs <container id>

# Enter the container
docker exec -it <container id> /bin/bash
```

## Routes

Available HTTP routes are:
- `GET /`: A web interface for the chatbot,
- `POST /`: A webhook implementing Smooch and Dialogflow REST API calls.

## TODO
- [x] Implement a webchat bot on Smooch.io
- [x] [Dialogflow](https://dialogflow.com) and Smalltalk Intent
- [ ] Internet Knowledge for questions off topic
  - Google Answer box
  - [DuckDuckGo Instant Answer API](https://duckduckgo.com/api)
  - [Wolfram API](https://products.wolframalpha.com/api/)
- [ ] [Google API](https://www.npmjs.com/package/googleapis)
  - Calendar integration
- [ ] Fill in [Github Issue](https://developer.github.com/v3/issues/) for unanswered questions like in [sindresorhus/ama](https://github.com/sindresorhus/ama):
   - Node.js lib: https://www.npmjs.com/package/github
- [ ] Deploy demo app on Heroku or Cloud Functions.
