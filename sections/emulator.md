
Emulator pages can be used, to quickly and easily show the apps in browser.

## Get Emulator Page URL

This API returns URL - which will open emulator page of AppSurfer.


URL - /v1/publisher/apps/:app_uid/emulator_url

Method - GET

e.g. - 

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
        "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0a3a-0130-e0e8-12313d053c1b/emulator_url"


Response - 

    {
      "success" : true,
      "emulator_url" : "http://dev.appsurfer.com:3000/apps/emulator/51893d30-f7cc-0130-cc68-7845c4b48655"
    }
