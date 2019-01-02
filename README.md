# Primephonic Full-Stack coding challenge
Thanks for your interest in Primephonic and for taking the time to do our full-stack coding challenge. We hope you enjoy developing it as much as we did :)

## Background
An important part of our business is keeping track of what our customers stream, so we can pay back royalties towards the labels and artists. Our payout model is different than other streaming services, in that we pay royalties based on total number of seconds streamed, instead of how many times a track has been streamed.

For this, the client apps (Android, iOS & Web) monitor the tracks being played and periodically send usage reports to our backend, which collects and processes these events.

## Task
This challenge consists of 2 parts:
### 1. Backend
Create a back-end system (using `Node.js) which simulates usage data generated from the apps. This system must:
- Every `10 seconds`, generate a random number of events (between 1 and 5 events)
- Store these events as-is, with no additional logic such as grouping, etc (can be stored in-memory)
- Expose a REST API which allows clients to query this data

### 2. Frontend
Create a frontend (using `Vue.js`) which displays the information below, and automatically refreshes the data at least every `15 seconds`:
- Total seconds streamed
- Total seconds streamed per label
- Most popular track (popular = most streamed)

# Implementation
1. Each event generated, should have the following format
```javascript
{
    "user_id": "1",                     // can be either user1, user2 or user3
    "track_id": "track1",               // can be either track1, track2 or track3
    "label": "label1",                 // can be either label1, label2 or label3
    "stream_started_on": 1546421951,    // represents when the track began streaming (Unix time)
    "seconds_streamed": 1290            // represents total numbers of seconds streamed
}
```

2. The API exposed has the following specs:

**Description**

This endpoint should enable clients to query the data with some additional filtering params.


**Parameters**

| Name | Type | Description |
| --- | --- | --- |
| `from` | `int` (seconds - Unix time) | From when to retrieve data (E.g. disregard all events which are previous than this date) |

**Response**

| Code | Body | Condition |
| --- | --- | --- |
| `200` | `see sample` | If the `from` param is in the past |
| `400` | `empty` | If the `from` param is in the future |

**Sample Request**

`GET /usage?from=1546422000`

**Sample Response**
```javascript
[
  {
    "user_id": "1",
    "track_id": "track1",
    "label": "label1",
    "stream_started_on": 1546422100,
    "seconds_streamed": 1290
  },
  {
    "user_id": "2",
    "track_id": "track2",
    "label": "label3",
    "stream_started_on": 1546422110,
    "seconds_streamed": 987
  },
  {
    "user_id": "1",
    "track_id": "track2",
    "label": "label1",
    "stream_started_on": 1546422130,
    "seconds_streamed": 1500
  }
]
```

## Design
No guidelines here, but we'd love to be impressed 🤩

## Technologies
Any of the following are allowed: `Node.js`, `Vue.js`, `JavaScript`, `Typescript`, `HTML`, `CSS`

## Submission Guidelines
- Submit your project in a single `zip` file to your Primephonic contact
- Include a `README.md` with instructions on how to run it, together with any additional information you consider appropriate (assumptions, design decisions made, etc.)
- Include *only* source code and assets (no libraries, modules, etc.)
