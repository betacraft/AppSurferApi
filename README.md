AppSurfer Api
============

AppSurfer API docs -

AppSurfer APIs are currently private. To get access to APIs, contact with us at contact@rainingclouds.com

# Publisher API

## Overview - 

Using this API app publishers can add, edit or remove apps from AppSurfer.

Base URL - https://api.appsurfer.com

All below paths to be used with this URL.

## Authentication - 

auth_key need to be sent in all request headers for authentication.



## 1. Add App -

### 1.1 Get Access Token - 

Path - /v1/publishers/apps/access_token

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
    <td>Required if existing app apk needs be updated. </td>
  </tr>
</table>

Params - 

     {
      "key": "tmp/76/sample.apk",
      "AWSAccessKeyId": "AbbbbbbbbbbbbQ",
      "success_action_redirect": "http://api.appsurfer.com/v1/publisher/apps/uploaded/123123?apk_name=sample.apk&app_name=sample&app_uid=cdb0e5b0-eeee-012f-53be-1231400041d3",
      "bucket": "cloudbucket",
      "acl": "private",
      "policy": "eyJleHBpcmFdd0aW9uIjoiMjAxMi0xMC0zMVQwNjoyNzozNS4wMDBaIiwiY29uZGl0aW9ucyI6W3siYnbGUuYXBrIn0seyJhY2wiOiJwcml2YXRlIn0seyJzdWNjZXNzX2FjdGlvbl9yZWRpcmVjdCI6Imh0dHA6Ly9kZXZhcGkuYXBwc3VyZmVyLmNvbasdfTodzMDAwL3YxL3B1Ymxpc2hlci9hcwHBzL3VwbG9hZGVkLzc2P2Fwa19uYW1lPXNhbXBsZS5hcGsmYXBwX25hbWU9c2FtcGxlJmFwcF91aWQ9Y2RiMGU1YjAtYWVmOS0wMTJmLTUzYmUtMTIzMTQwMDA0MWQzIn1dasdfasdffQ",
      "signature": "zWdeogmMj2EXwwQdZskwSHRiqo8zeB1/ss2c=",
      "s3_url": "https://cloud.s3.amazonaws.com"
     }


### 1.2 Upload File - 

URL - Found from step 1 as s3_url

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
    <td>Required. Get it in access_token API</td>
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


Response - 

    {
      "success": true,
      "app_uid": "cdb0e5b0-aef9-eeee-53ee-1230000041d3",
      "widget_url": "http://www.appsurfer.com/widget/cdb0e5b0-aef9-eeee-53ee-1230000041d3"
    }

### 1.3 Update App Details -

URL - /v1/publishers/apps

Method - PUT

Params - 

<table>
  <tr>
    <th>Param </th><th> Type </th><th> Description </th>
  </tr>
  <tr>
    <td>app_uid </td><td> string </td><td> uid found from Apk upload request. </td>
  </tr>
  <tr>
    <td> name </td><td> string </td><td> App's name. </td>
  </tr>
  <tr>
    <td> description </td><td> text </td><td> optional </td>
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
    <td> market_button </td><td> boolean </td><td> default - false. If true and app is present on google market, Download from market button will show up </td>
  </tr>
  <tr>
</table>


Response - 
  
    {
      "success": true,
      "app_uid": "37f7sadf7350-04d0-0130-ac48-00163e4c2006",
      "widget_url": "http://api.appsurfer.com/widget/37f7735d0-04d0-0130-ac48-00163sde4c2006"
    }

### 1.4 Update App Details -

URL - /v1/publishers/apps/:app_uid

Method - DELETE

Params - app_uid in url

Use with care. This will delete the app and all history related with app including number of sessions played and other stats. This can't be undone.


## 2. Get widget code -

URL - /v1/publisher/apps/:app_uid/widget

Method - GET

Params - 

| Param | Type | Description |
| app_uid | string | needs to be present in URL |
| autoplay | boolean | Default false. |

Response - 

    {
      "success": true,
      "widget_code": "<iframe src='http://www.appsurfer.com/widget/cdb0e5bd0-aef9-012f-53be-1231400041ds3?phone_align=left&scroll=false&tour=true&action=widget&controller=api%2Fv1%2Fpublisher%2Fapps&id=cdb0e5b0-aef9-012f-53be-1231400041d3', style='width:620px; height:620px;border:none;' frameBorder:'none' ALLOWTRANSPARENCY='true'></iframe>\n    "
    }

## 3. Get Surf it button code - 

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

Response - 

    {
      "success": true,
      "button_code": "<script type='text/javascript' src='http://www.appsurfer.com/surf.js.js'></script>\n    <iframe src='http://www.appsurfer.com/apps/7122-location-tester/buttons/small_hz' scrolling='no' frameborder='0' style='height:35px; width:100px;border:none;' class='ASWButtonFrame' data-domain='http://www.appsurfer.com'></iframe>"
    }