# Yube API

## Endpoints

### Implementation

Endpoints are implemented as callbacks to a given folder. For example, `GET /video-data` could get the video data, and be declared as:

```py
{
  "callback": video_functions.like_video,
  "token_check": True,
  "permissions": ["like"],
}
```

The callback function format is roughly:

```py
callback(client, data, context)
```

* Client contains a connection to the client for responding to the request.
* Data holds the data of the request as a pre-parsed JSON object.
* Context contains things like access to the Video Store or AuthDB and generally provides high level primitives for use in code.

All user data is sanitised and the token validity is checked *before* being sent to the callback function so it should not have to worry about doing anything too stupid (though mistakes can always happen).

### Notes

* We should only ever have to sanitise and auth in one place so that we don't need to remember to do it when adding a new feature.
  * This is not that hard for generic tokens and making sure that some endpoints are only useable by tokens with certian privleges.
  * This is harder for when there are different things like videos and comments where you need to check the ownership (unless we have an object ownership system).
