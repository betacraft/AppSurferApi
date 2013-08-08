# Apps API

AppSurfer API provides ways for creating, editing and updating apps on AppSurfer apps.

Apps API can be used for - 

- [Get apps](#1-get-apps)
- [Create app](#2-create-app)
- [Update apk](#3-update-app)
- [Update app](#4-update-app)
- [Get app details](#5-get-app-details)
- [Delete app](#6-delete-app)
 

## 1. Get apps

This will return list of all the apps that are owned by a developer.

URL - /v1/publisher/apps

Method - GET

Params -

<table>
  <tr>
    <td>Param </td>
    <td> Type </td>
    <td> Description </td>
  </tr>
  <tr>
    <td> category </td>
    <td> integer </td>
    <td> App category for filtering apps. Returns apps from all categories if absent.</td>
  </tr>
  <tr>
    <td> page </td>
    <td> integer </td>
    <td> Page number</td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
            "http://api.appsurfer.com/v1/publisher/apps?category=1&page=1"

Response - 

    {
        "apps": [
            {
                "uid": "bf1c99e0-2cbc-0130-544b-123138155349",
                "name": "Simbu",
                "tagline": "You v/s time,and your fight  for food ",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/11159/seventy/open-uri20121220-2-7oz19y?1355998814"
            },
            {
                "uid": "84cf2830-2cb9-0130-0fb0-1231381d64fc",
                "name": "Terminal Velocity Space Racing",
                "tagline": "Dodge your way through electric fields ",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/11136/seventy/open-uri20121220-2-awlc1p?1355997426"
            },
            {
                "uid": "e8e3e740-2c13-0130-4b9c-22000a1e85c6",
                "name": "Angry Hornets Light",
                "tagline": "-",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/11093/seventy/open-uri20121219-2-pibvi3?1355926296"
            },
            {
                "uid": "f3fd3e90-27dd-0130-bd94-123139160e10",
                "name": "Bow Man 3",
                "tagline": "Bow game man bowman",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/10415/seventy/open-uri20121214-2-qdeeb5?1355463316"
            },
            {
                "uid": "0b9dd600-27c4-0130-7369-1231381d6960",
                "name": "Whack-A-Mole もぐらたたき",
                "tagline": "Whack-A-Mole",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/10313/seventy/open-uri20121214-2-1ilk80?1355452189"
            },
            {
                "uid": "4c1012a0-26f8-0130-4090-12313b0325b7",
                "name": "animalkeeper　肉食or草食",
                "tagline": "animalkeeper",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/9975/seventy/open-uri20121213-2-okvu5x?1355393867"
            },
            {
                "uid": "2549b420-26f7-0130-9f0d-1231381d612b",
                "name": "AgileMan   アジャイルマン",
                "tagline": "AgileMan",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/9971/seventy/open-uri20121213-2-12jxbjv?1355393864"
            },
            {
                "uid": "3d835210-2622-0130-cc31-22000a9d0268",
                "name": "ZOO KEEPER",
                "tagline": "Big Tex Apps, Big Daddy App, Games, Zoo, animals",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/9811/seventy/open-uri20121212-2-m97f5k?1355393789"
            },
            {
                "uid": "1e828380-24c4-0130-cb84-1231381d9165",
                "name": "An Ultimate Hunt Arcade Game",
                "tagline": "An Ultimate Hunt Arcade Game",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/9457/seventy/open-uri20121210-2-h079aj?1355393631"
            },
            {
                "uid": "a70f8f20-2352-0130-bfc7-1231381d8d48",
                "name": "Drone Attack",
                "tagline": "Hunting season has begun.",
                "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/9136/seventy/open-uri20121208-2-m6ukhg?1355393347"
            }
        ]
    }


## 2. Create App

Path - /v1/publisher/apps

Method - POST

Params - 

<table>
  <tr>
    <th> Param </th>
    <th> Type </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> name </td> 
    <td> string </td>
    <td> Required. App name required to generate access_token </td>
  <tr>
  <tr>
    <td> description </td> 
    <td> text </td>
    <td> Optional </td>
  <tr>
  <tr>
    <td> opt_for_showcase </td> 
    <td> boolean </td>
    <td> Default is false. If set to true, and if app is present on google market, it will be published on AppSurfer showcase as well. </td>
  <tr>
  <tr>
    <td> publisher_name </td> 
    <td> string </td>
    <td> Few widget types may require this to be shown on widgets. </td>
  <tr>
</table>


E.g. - 

    curl https://api.appsurfer.com/v1/publisher/apps -X POST -H 'content-type:application/json' -H 'auth_key:8f9c6ca0-353b-012f-177f-12313b036578' -d '{"name":"test"}'


Response - 

    { 
      "success":true,
      "message":"App Created successfully.",
      "app_uid":"63d93ed0-e249-0130-681b-441ea1e48f44"
    }


## 3. Update Apk

For updating apk for an app on AppSurfer, it requires two steps - 

- Getting temporary authentication for s3
- Uploading apk file to s3

Update apk API can be used for first time apk upload of an app or for updating apk of existing app.

### 3.1 Get Temporary authentication for s3 - 

Path - /v1/publisher/apps/get_token

Method - GET

Params -

<table>
  <tr>
    <th> Param </th>
    <th>  Type </th>
    <th>Description</th>
  </tr>
  <tr>
    <td> name </td> 
    <td> string </td>
    <td> App name required to generate access_token </td>
  <tr>
    <td>apk_name</td>
    <td>string </td>
    <td>Required to generate access_token </td>
  </tr>
  <tr> 
    <td>app_uid </td>
    <td>string </td>
    <td>Required</td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-asdf-0130-850c-22000a9d050a" "http://api.appsurfer.com/v1/publisher/apps/get_token?name=Githubs&apk_name=githubs.apk"


Response - 

     {
      "key": "tmp/76/sample.apk",
      "AWSAccessKeyId": "AbbbbbbbbbbbbQ",
      "success_action_redirect": "http://api.appsurfer.com/v1/publisher/apps/uploaded/123123?apk_name=sample.apk&app_name=sample&app_uid=cdb0e5b0-eeee-012f-53be-1231400041d3",
      "bucket": "cloudbuckset",
      "acl": "private",
      "policy": "eyJleHBpcmFdd0aW9sIjoiMjAxMi0xMC0zMVQwNjoyNzozNS4wMDBaIiwiY29uZGl0aW9ucyI6W3siYnbGUuYXBrIn0seyJhY2wiOiJwcml2YXRlIn0seyJzdWNjZXNzX2FjdGlvbl9yZWRpcmVjdCI6Imh0dHA6Ly9kZXZhcGkuYXBwc3VyZmVyLmNvbasdfTodzMDAwL3YxL3B1Ymxpc2hlci9hcwHBzL3VwbG9hZGVkLzc2P2Fwa19uYW1lPXNhbXBsZS5hcGsmYXBwX25hbWU9c2FtcGxlJmFwcF91aWQ9Y2RiMGU1YjAtYWVmOS0wMTJmLTUzYmUtMTIzMTQwMDA0MWQzIn1dasdfasdffQ",
      "signature": "zWdesogmMj2EXwwQdZsskwSHRiqo8zeB1/ss2c=",
      "s3_url": "https://droidcloud.s3.amazonaws.com"
     }


### 3.2 Upload File to s3 - 

URL - Found from above step as `s3_url`

Method - POST

Params - 

<table>
  <tr>
    <th>Param</th>
    <th>Type</th> 
    <th>Description</th>
  </tr>
  <tr>
    <td>key</td>
    <td>string</td>
    <td>Required. Found from app upload step1 API</td>
  </tr>
  <tr>
    <td>AWSAccessKeyId</td>
    <td>string</td>
    <td>--"-- </td>
  </tr>
  <tr>
    <td>success_action_redirect</td>
    <td>string</td>
    <td>--"--</td>
  </tr>
  <tr>
    <td>bucket</td>
    <td>string</td>
    <td>--"-- </td>
  </tr>
  <tr>
    <td> acl </td>
    <td>string </td>
    <td> --"-- </td>
  </tr>
  <tr>
    <td> policy </td>
    <td> string </td>
    <td> --"-- </td>
  </tr>
  <tr>
    <td>signature </td>
    <td>string </td>
    <td>--"-- </td>
  <tr>
    <td> file </td>
    <td> file </td>
    <td> File to be uploaded </td>
  </tr>
</table>

E.g.

Make sure that client making upload request should be able to follow redirects. On POST to s3, it does 303 GET redirect to AppSurfer app.

    curl -X POST -F "key=tmp/228/github.apk"\
                 -F "AWSAccessKeyId=AKIsdAJTL35BC2OZ7FZublisher/apps/uploaded/228?apk_name=githubs.apk&app_name=Githubs"\
                 -F "bucket=droidcloud"\
                 -F "acl=private"\
                 -F "policy=esyJleHBpcmF0aW9uIjoiMjAxMi0xMS0wNlQxMTozMzoxNy4wMDBaIiwiY29uZGl0aW9ucyI6W3siYnVja2V0IjoiZHJvaWRjbG91ZC1zdGFnaW5nIn0seyJrZXkiOiJ0bXAvMjI4L2dpdGh1Yi5hcGsifSx7ImFjbCI6InByaXZhdGUifSx7InN1Y2Nlc3NfYWN0aW9uX3JlZGlyZWN0IjoiaHR0cDovL3ByZWFwaS5hcHBzdXJmZXIuY29tL3YxL3B1Ymxpc2hlci9hcHBzL3VwbG9hZGVkLzIyOD9hcGtfbmFtZT1naXRodWIuYXBrJmFwcF9uYW1lPUdpdGh1YiJ9XX0="\
                 -F "signature=/T7AnK3NkT2sYReBfM0oyMeaa+Vc="\
                 -F "file=@githubs.apk"\
                 -L "https://droidcloud.s3.amazonaws.com"

**Important - params needs to be ordered in same order as received in get_token request.

Response - 

If any http error happens while uploading to s3, it will indicate it with proper http response code without redirect to appsurfer app.

On successful upload, amazon will redirect to AppSurfer app. If apk passes all validations, then it will respond as -

    {
      "success": true,
      "app_uid": "cdb0e5b0-aef9-eeee-53ee-1230000041d3"
    }

If validation fails on apk, response will be as below - 

    {
      "success": false,
      "error": ["Your app requires native code which is not supported by AppSurfer"]
    }



## 4 Update App


URL - /v1/publisher/apps/:app_uid

Method - PUT

Params - 

<table>
  <tr>
    <th>Param </th><th> Type </th><th> Description </th>
  </tr>
  <tr>
    <td>app_uid </td><td> string </td><td> uid found from Apk upload request. Should be present in url at :app_uid</td>
  </tr>
  <tr>
    <td> name </td><td> string </td><td> App's name. </td>
  </tr>
  <tr>
    <td> description </td><td> text </td><td> Optional app description. </td>
  </tr>
  <tr>
    <td> published </td><td> boolean </td><td> Default - true. If set to false, app will only be usable from sandbox mode </td>
  </tr>
  <tr>
    <td> socially_shareable </td><td> boolean </td><td> Default to true for public apps. If set to false, social share widgets wont show up in widget. These buttons will share links on AppSurfer widget. </td>
  </tr>
  <tr>
    <td> default_layout </td><td> boolean </td><td> default - 0 i.e. portrait. This decides orientation of phone image in widget. Send 1 for landscape. </td>
  </tr>
  <tr>
</table>

E.g.

    curl -X PUT -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a"\
                --data "name=gihtubs&description=githubs_app_desc&published=false&socially_shareable=false&default_layout=false&market_button=false" "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0a3a-0130-e0e8-12313d053c1b"

Response - 
  
    {
      "success": true,
      "app_uid": "37f7sadf7350-04d0-0130-ac48-00163e4c2006"
    }




## 5. Get app details

### 5.1 Using UID:

Returns details of a app.


URL - /v1/publisher/apps/:app_uid

Method - GET

Params -

<table>
  <tr>
    <td>Param </td>
    <td> Type </td>
    <td> Description </td>
  </tr>
  <tr>
    <td> app_uid </td>
    <td> string </td>
    <td> needs to be present in URL</td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
            "http://api.appsurfer.com/v1/publisher/apps/03b214f0-3ac1-012f-1888-12313b036578"

Response - 

    {
        "app": {
            "name": "SuDoKu",
            "tagline": "World's Fastest Sudoku Solver",
            "description": "Experience the Best Sudoku Puzzle on the Market - After close to Million Sudoku Downloads on Nokia Store, the Original Sudoku Plus will floor you! Here are few things to watch out for in Sudoku Plus:\r\n1.Worlds fastest Sudoku Solver\r\n2.Track & improve your Guesses\r\n3.Various levels of difficulties\r\n4. Best Sudoku User Interface",
            "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/4/seventy/ico_sp_96x96.png?1355389151",
            "google_market_url": "https://play.google.com/store/apps/details?id=com.sudokuplus&rdid=com.sudokuplus&rdot=1",
            "screenshots": [
                "https://droidcloud-dev.s3.amazonaws.com/images/257/screenshot/open-uri20121003-2-15rw4zn?1349265216",
                "https://droidcloud-dev.s3.amazonaws.com/images/258/screenshot/open-uri20121003-2-1pzqhy0?1349265217"
            ],
            "publisher": "Webonise Labs"
        }
    }
    

### 5.2 Using package_name:

URL - /v1/publisher/apps/package/:package_name

Method - GET

Params -

<table>
  <tr>
    <td>Param </td>
    <td> Type </td>
    <td> Description </td>
  </tr>
  <tr>
    <td> package_name </td>
    <td> string </td>
    <td> needs to be present in URL</td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
            "http://api.appsurfer.com/v1/publisher/apps/package/com.sudokuplus"

Response - 

    {
        "app": {
          "name": "SuDoKu",
          "tagline": "World's Fastest Sudoku Solver",
          "description": "Experience the Best Sudoku Puzzle on the Market - After close to Million Sudoku Downloads on Nokia Store, the Original Sudoku Plus will floor you! Here are few things to watch out for in Sudoku Plus:\r\n1.Worlds fastest Sudoku Solver\r\n2.Track & improve your Guesses\r\n3.Various levels of difficulties\r\n4. Best Sudoku User Interface",
          "logo_url": "https://droidcloud-dev.s3.amazonaws.com/images/4/seventy/ico_sp_96x96.png?1355389151",
          "google_market_url": "https://play.google.com/store/apps/details?id=com.sudokuplus&rdid=com.sudokuplus&rdot=1",
          "screenshots": [
              "https://droidcloud-dev.s3.amazonaws.com/images/257/screenshot/open-uri20121003-2-15rw4zn?1349265216",
              "https://droidcloud-dev.s3.amazonaws.com/images/258/screenshot/open-uri20121003-2-1pzqhy0?1349265217"
          ],
          "publisher": "Webonise Labs"
        }
    }


## 6 Delete App

Use with care. This will delete the app and all history related with app including number of sessions played and other stats. This can't be undone.

URL - /v1/publisher/apps/:app_uid

Method - DELETE

Params - app_uid in url


E.g - 

    curl -X DELETE -H "auth_key: c0c40350-0a16-0130-850c-asdfasdfasdf"
                      "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0sdfa3a-sdf30-e0e8-12313d053c1b"
