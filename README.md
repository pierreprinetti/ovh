# OVH shell client

## Requirements

### Tools

* sh
* date
* shasum
* cut

### Create a new OVH app

In your browser: https://eu.api.ovh.com/createApp/

### Give the app access to your account

```
export OVH_AK=<your new Application Key>
```

Then in the terminal:

```
curl \
	-X POST \
	-H "X-Ovh-Application: ${OVH_AK}" \
	-H "Content-type: application/json" \
	'https://eu.api.ovh.com/1.0/auth/credential'  -d '{
    "accessRules": [
        {
            "method": "GET",
            "path": "/*"
        },
        {
            "method": "POST",
            "path": "/*"
        },
        {
            "method": "PUT",
            "path": "/*"
        },
        {
            "method": "DELETE",
            "path": "/*"
        }
    ],
    "redirection":"https://www.example.com/"
}'
```

Click on the link and authorise. Then pick the Consumer Key from the JSON response to the curl call:

```
export OVH_CK=<your new Consumer Key>
```

## Howto

As long as `OVH_AK` and `OVH_CK` are available in the environment, it is possible to call any endpoint in the [OVH API](https://eu.api.ovh.com/console/ "OVH API reference").

```
./ovh 'GET' '/domain'
```

## Known issues

* This script does not currently handle form parameters.
* Sending a body payload is untested.
