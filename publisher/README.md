# Publisher API

## Overview - 

Using this API app publishers can add, edit or remove apps from AppSurfer.

Base URL - https://api.appsurfer.com

All Api take JSON data and respond with JSON data.

Every request should have 

    Content-Type:application/json
    
in their headers.


## Authentication - 

auth_key need to be sent in all request headers for authentication.

    auth_key:AUTH_KEY_FROM_APPSURFER
