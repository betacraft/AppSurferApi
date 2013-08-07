## Authentication - 

Every request to AppSurfer API will be authenticated based on auth_key present in request headers. auth_key can be found in publisher dashboard > 'My Profile' page.

    auth_key:AUTH_KEY_FROM_APPSURFER


Sample request - 

    curl https://api.appsurfer.com/v1/publisher/apps/1 -H 'auth_key:8febfca0-c658-0130-5e09-6edc03ee7e93'

