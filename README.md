# Polls

A real-time polling system where users can create polls which other users can vote. 

![Screenshot](https://github.com/Juan-Kineipe/polls/blob/main/github/architecture.jpg?raw=true)

## Requisites

- Node.js;
- Docker;

## Setup

- Install dependencies (`npm install`);
- Setup Docker to use PostgreSQL and Redis (`docker compose up -d`);
- Create a file named `.env` at the root of the project with the following content: (`DATABASE_URL="postgresql://docker:docker@localhost:5432/polls?schema=public"`);
- Run application (`npm run dev`);
- Test it using any API platform (e.g. [Postman](https://www.postman.com)).

## HTTP

### POST `/polls`

Create a new poll

#### Request body

```json
{
	"title": "What is the best JavaScript Framework?",
	"options": ["Angular", "React", "Vue.js", "Ember.js"]
}
```

#### Response body

```json
{
	"pollId": "5d932730-3aa9-41f2-b6ce-d9b08665b288"
}
```

### GET `/polls/:pollId`

Return data from a specific poll

#### Response body

```json
{
	"poll": {
		"id": "5d932730-3aa9-41f2-b6ce-d9b08665b288",
		"title": "What is the best JavaScript Framework?",
		"options": [
			{
				"id": "f54212fb-3326-486c-ac3e-1539c5e67b4c",
				"title": "Angular",
				"votes": 1
			},
			{
				"id": "4d913b79-0468-4a8f-b7c8-9252522b7e7e",
				"title": "React",
				"votes": 0
			},
			{
				"id": "953708fb-1de2-482c-a59d-19921c51d908",
				"title": "Vue.js",
				"votes": 0
			},
			{
				"id": "8c4659b1-c0a2-4871-90b7-2d51c3c2294e",
				"title": "Ember.js",
				"votes": 0
			}
		]
	}
}
```

### POST `/polls/:pollId/votes`

Add a vote to specific poll

#### Request body

```json
{
	"pollOptionId": "f54212fb-3326-486c-ac3e-1539c5e67b4c"
}
```

## WebSocket

### ws `/polls/:pollId/results`

#### Message

```json
{
	"pollOptionId": "f54212fb-3326-486c-ac3e-1539c5e67b4c",
	"votes": 1
}
```
