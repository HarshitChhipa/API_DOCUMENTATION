## User Details API

This is our high-quality fake User detail API'S. You can use this API to request
and remove different user details and do other things.

### List Of API End Points

Lists all Users for a particular account.

```endpoint
GET /fakeurl/v1/{username} users:read
```

#### Example request

```curl
$ curl https://fakeurl.biz/fakeurl/v1/{username}
```

```bash
$ wbl fakeuser list
```

```javascript
client.listFakeUsers(function(err, users) {
  console.log(users);
});
```

```python
fakeUsers.list()
```

#### Example response

```json
[
  {
    "owner": "{username}",
    "id": "{user_id}",
    "created": "{timestamp}",
    "modified": "{timestamp}"
  },
  {
    "owner": "{username}",
    "id": "{user_id}",
    "created": "{timestamp}",
    "modified": "{timestamp}"
  }
]
```

### Create User

Creates a new, empty user.

```endpoint
POST /users/v1/{username}
```

#### Example request

```curl
curl -X POST https://fakeurl.biz/fakeurl/v1/{username}
```

```bash
$ wbl fakeuser create
```

```javascript
client.createFakeUsers({
  name: 'example',
  description: 'An example to create a user'
}, function(err, fakeUser) {
  console.log(fakeUser);
});
```

```python
response = fakeUsers.create(
  name='example', description='An example to create a user')
```

#### Example request body

```json
{
  "name": "foo",
  "description": "bar"
}
```

Property | Description
---|---
`name` | (optional) the name of the user 
`description` | (optional) a description of the user

#### Example response

```json
{
  "owner": "{username}",
  "id": "{user_id}",
  "name": null,
  "description": null,
  "created": "{timestamp}",
  "modified": "{timestamp}"
}
```

### Retrieve a user

Returns a single user.

```endpoint
GET /users/v1/{username}/{user_id}
```

Retrieve information about an existing user.

#### Example request

```curl
curl https://user.biz/users/v1/{username}/{user_id}
```

```bash
$ wbl user read-user user-id
```

```python
attrs = users.read_user(user_id).json()
```

```javascript
client.readuser('user-id',
  function(err, user) {
    console.log(user);
  });
```

#### Example response

```json
{
  "owner": "{username}",
  "id": "{user_id}",
  "created": "{timestamp}",
  "modified": "{timestamp}"
}
```

### Update a user

Updates the properties of a particular user.

```endpoint
PATCH /users/v1/{username}/{user_id}
```

#### Example request

```curl
curl --request PATCH https://user.biz/users/v1/{username}/{user_id} \
  -d @data.json
```

```python
resp = users.update_user(
  user_id,
  name='updated example',
  description='An updated example user'
  ).json()
```

```bash
$ wbl user update-user user-id
```

```javascript
var options = { name: 'foo' };
client.updateuser('user-id', options, function(err, user) {
  console.log(user);
});
```

#### Example request body

```json
{
  "name": "foo",
  "description": "bar"
}
```

Property | Description
---|---
`name` | (optional) the name of the user
`description` | (optional) a description of the user

#### Example response

```json
{
  "owner": "{username}",
  "id": "{user_id}",
  "name": "foo",
  "description": "bar",
  "created": "{timestamp}",
  "modified": "{timestamp}"
}
```

### Delete a user

Deletes a user, including all items it contains.

```endpoint
DELETE /users/v1/{username}/{user_id}
```

#### Example request

```curl
curl -X DELETE https://user.biz/users/v1/{username}/{user_id}
```

```bash
$ wbl user delete-user user-id
```

```python
resp = users.delete_user(user_id)
```

```javascript
client.deleteuser('user-id', function(err) {
  if (!err) console.log('deleted!');
});
```

#### Example response

> HTTP 204

### List items

List all the items in a user. The response body will be a
userCollection.

```endpoint
GET /users/v1/{username}/{user_id}/items
```

#### Example request

```curl
curl https://user.biz/users/v1/{username}/{user_id}/items
```

```bash
$ wbl user list-items user-id
```

```python
collection = users.list_items(user_id).json()
```

```javascript
client.listusers('user-id', {}, function(err, collection) {
  console.log(collection);
});
```

#### Example response

```json
{
  "type": "user",
  "items": [
    {
      "id": "{item_id}",
      "type": "user",
      "properties": {
        "prop0": "value0"
      }
    },
    {
      "id": "{item_id}",
      "type": "user",
      "properties": {
        "prop0": "value0"
      }
    }
  ]
}
```

### Insert or update a item

Inserts or updates a item in a user. If there's already a item
with the given ID in the user, it will be replaced. If there isn't
a item with that ID, a new item is created.

```endpoint
PUT /users/v1/{username}/{user_id}/items/{item_id}
```

#### Example request

```curl
curl https://user.biz/users/v1/{username}/{user_id}/items/{item_id} \
  -X PUT \
  -d @file.geojson
```

```bash
$ wbl user put-item user-id item-id 'geojson-item'
```

```javascript
var item = {
  "type": "user",
  "properties": { "name": "Null Island" }
};
client.insertuser(item, 'user-id', function(err, item) {
  console.log(item);
});
```

#### Example request body

```json
{
  "id": "{item_id}",
  "type": "user",
  "properties": {
    "prop0": "value0"
  }
}
```

Property | Description
--- | ---
`id` | the id of an existing item in the user

#### Example response

```json
{
  "id": "{item_id}",
  "type": "user",
  "properties": {
    "prop0": "value0"
  }
}
```

### Retrieve a item

Retrieves a item in a user.

```endpoint
GET /users/v1/{username}/{user_id}/items/{item_id}
```

#### Example request

```curl
curl https://user.biz/users/v1/{username}/{user_id}/items/{item_id}
```

```bash
$ wbl user read-item user-id item-id
```

```javascript
client.readuser('item-id', 'user-id',
  function(err, item) {
    console.log(item);
  });
```

```python
item = users.read_item(user_id, '2').json()
```

#### Example response

```json
{
  "id": "{item_id}",
  "type": "user",
  "properties": {
    "prop0": "value0"
  }
}
```

### Delete a item

Removes a item from a user.

```endpoint
DELETE /users/v1/{username}/{user_id}/items/{item_id}
```

#### Example request

```javascript
client.deleteuser('item-id', 'user-id', function(err, item) {
  if (!err) console.log('deleted!');
});
```

```curl
curl -X DELETE https://user.biz/users/v1/{username}/{user_id}/items/{item_id}
```

```python
resp = users.delete_item(user_id, item_id)
```

```bash
$ wbl user delete-item user-id item-id
```

#### Example response

> HTTP 204
