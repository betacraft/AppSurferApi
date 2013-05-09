## 1. Get apps -

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

## 2. Get app details -

### 2.1 Using uid:

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
    
### 2.2 Using package_name:

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
    
## 3. Get widget code -

URL - /v1/publisher/apps/:app_uid/widget

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
    <td> needs to be present in URL </td>
  </tr>
  <tr>
    <td> autoplay </td>
    <td> boolean </td>
    <td> Default false. </td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
            "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0a3a-0130-e0e8-12313d053c1b/widget"

Response - 

    {
      "success": true,
      "widget_code": "<iframe src='http://www.appsurfer.com/widget/cdb0e5bd0-aef9-012f-53be-1231400041ds3?phone_align=left&scroll=false&tour=true&action=widget&controller=api%2Fv1%2Fpublisher%2Fapps&id=cdb0e5b0-aef9-012f-53be-1231400041d3', style='width:620px; height:620px;border:none;' frameBorder:'none' ALLOWTRANSPARENCY='true'></iframe>\n    "
    }


## 4. Get Surf it button code - 

URL - /v1/publisher/apps/:app_uid/surfit_button/:type

Method - GET

Params - 

<table>
  <tr>
    <th>Param </th><th> Type </th><th> Description </th>
  </tr>
  <tr>
    <td> app_uid </td><td> string </td><td> needs to be present in URL </td>
  </tr>
  <tr>
    <td> type </td><td> string </td><td> Optional. Default is - surfit_small_hz. Other options include - surfit_hz, surfit_vt </td>
  </tr>
</table>

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a" -H "content-type:application/json"
            "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0a3a-0130-e0e8-12313d053c1b/surfit_button"

Response - 

    {
      "success": true,
      "button_code": "<script type='text/javascript' src='http://www.appsurfer.com/surf.js.js'></script>\n    <iframe src='http://www.appsurfer.com/apps/7122-location-tester/buttons/small_hz' scrolling='no' frameborder='0' style='height:35px; width:100px;border:none;' class='ASWButtonFrame' data-domain='http://www.appsurfer.com'></iframe>"
    }
