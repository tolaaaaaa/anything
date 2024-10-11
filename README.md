

# API Documentation: Create Post

## Endpoint
`POST /api/posts/create`

This endpoint creates a new post based on the post type and additional fields provided in the request body.

---

## Request Body

The request body should include different fields depending on the type of post (`player`, `tournament`, `match`, or `team`). Below are the required fields for each type of post.

### Common Fields for All Post Types

| Field     | Type   | Description                                     | Required |
|-----------|--------|-------------------------------------------------|----------|
| type      | String | Type of the post. Options: `player`, `tournament`, `match`, `team` | Yes      |
| playerId  | String | The unique identifier of the player creating the post | Yes      |
| location  | String | The location for the post                       | Yes      |
| date      | String | Date of the event or match                      | Optional |

---

### Type: `player` (Find a team as a player)

| Field     | Type   | Description                                     | Required |
|-----------|--------|-------------------------------------------------|----------|
| position  | String | The position the player is looking to play       | Yes      |
| location  | String | The location for the post                       | Yes      |
| date      | String | The date the player is available                | Optional |

![WhatsApp Image 2024-10-11 at 11 18 32_2bdd652c](https://github.com/user-attachments/assets/1495649a-9a4c-40fd-94e3-50bd7dacfaf5)


#### Example Request Body:
```json
{
  "type": "player",
  "playerId": "60f5c75e47ad570017a9a7de",
  "position": "Forward",
  "location": "New York",
  "date": "2024-10-15"
}
```

---

### Type: `tournament` (Find a team or tournament)

| Field       | Type   | Description                                     | Required |
|-------------|--------|-------------------------------------------------|----------|
| description | String | Description of the tournament or event          | Yes      |
| date        | String | Date of the tournament or event                 | Optional |

![WhatsApp Image 2024-10-10 at 06 49 20_9a588939](https://github.com/user-attachments/assets/4f5c4162-b033-45db-af1a-9b1295d395c5)


#### Example Request Body:
```json
{
  "type": "tournament",
  "playerId": "60f5c75e47ad570017a9a7de",
  "description": "Looking for teams to join our local tournament",
  "location": "Los Angeles",
  "date": "2024-11-01"
}
```

---

### Type: `match` (Find an opponent to play a match)

| Field       | Type   | Description                                     | Required |
|-------------|--------|-------------------------------------------------|----------|
| date        | String | The date of the match                           | Yes      |
| groundName  | String | The name of the ground where the match will be played | Yes      |
| description | String | Description of the match                        | Yes      |

![WhatsApp Image 2024-10-10 at 06 49 20_a45ff893](https://github.com/user-attachments/assets/570e275d-907a-4501-9916-969a8ffeb0f6)


#### Example Request Body:
```json
{
  "type": "match",
  "playerId": "60f5c75e47ad570017a9a7de",
  "date": "2024-10-20",
  "groundName": "Main Stadium",
  "description": "Looking for opponents for a friendly match",
  "location": "San Francisco"
}
```
![alt text](<WhatsApp Image 2024-10-10 at 06.49.20_959e2a88.jpg>)

---

### Type: `team` (Find a player to join my team)

| Field       | Type   | Description                                     | Required |
|-------------|--------|-------------------------------------------------|----------|
| position    | String | The position the team is looking to fill        | Yes      |
| date        | String | The date of the event                           | Yes      |
| groundName  | String | The name of the ground where the event will be held | Yes      |
| description | String | Description of the event or match               | Yes      |

![WhatsApp Image 2024-10-10 at 06 49 20_58f7c4a8](https://github.com/user-attachments/assets/76a48d27-555d-41dd-8649-68d98d14871f)


#### Example Request Body:
```json
{
  "type": "team",
  "playerId": "60f5c75e47ad570017a9a7de",
  "position": "Goalkeeper",
  "date": "2024-10-18",
  "groundName": "City Sports Arena",
  "description": "We are looking for a goalkeeper to join our team for a tournament",
  "location": "Boston"
}
```

---



## Response

If the post is successfully created, the API returns the created post details along with the player’s information.

### Example Success Response:
```json
{
  "_id": "60f6ed05d9b9c80018d5a0b9",
  "type": "team",
  "location": "Boston",
  "player": {
    "_id": "60f5c75e47ad570017a9a7de",
    "name": "John Doe",
    "dp": "https://example.com/john.jpg",
    "phone": "+123456789"
  },
  "position": "Goalkeeper",
  "date": "2024-10-18",
  "groundName": "City Sports Arena",
  "description": "We are looking for a goalkeeper to join our team for a tournament"
}
```

---

## Error Responses

The API provides error messages for the following scenarios:

### Missing Required Fields
If required fields (e.g., `type`, `location`, `playerId`, etc.) are missing from the request body, the API will return a 400 status code and an error message.

#### Example:
```json
{
  "message": "Type, location, and playerId are required"
}
```

### Player Not Found
If the `playerId` provided does not correspond to a valid player in the database, the API will return a 404 status code.

#### Example:
```json
{
  "message": "Player does not exist"
}
```

### Invalid Post Type
If the `type` provided is not valid, the API will return a 400 status code.

#### Example:
```json
{
  "message": "Invalid post type"
}
```

### Internal Server Error
If an unexpected error occurs while processing the request, the API will return a 500 status code with the error message.

#### Example:
```json
{
  "message": "Internal server error",
  "error": "Error details..."
}
```

---

## Notes

- Ensure that the `playerId` is valid and corresponds to an existing player in the system.
- Each post type requires different fields in the request body, as outlined above.
