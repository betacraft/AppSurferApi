# Add/Edit App API

This document covers the details on creating,updating and deleting apps on AppSurfer.

## 1. Add App -

Uploading of APK happens in two steps - in first step, you should send a request to AppSurfer api and get signature and other params required for uploading file to s3.  In second step, you have to directly upload the file to s3, all required things for successful upload will be available in response of first step. If file is successfully uploaded to s3, it will redirect again to AppSurfer app, after which, validations will be done on apk file.

If you want to change apk file for existing app, same steps should be followed except that - app_uid should be provided in first step.

### 1.1 Get Access Token - 

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
    <td>Required if existing app apk needs be updated. </td>
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

E.g.

Make sure that client making request should be able to follow redirects. On POST to s3, it does 303 GET redirect to rails app.

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

If validation fails on apk, response will contain success false with all validation errors.

### 1.3 Update App Details -

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
    <td> description </td><td> text </td><td> Optional app description </td>
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
    <td> market_button </td><td> boolean </td><td> Default - true. If false Download from market button won't show up </td>
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

### 1.4 Delete App -

URL - /v1/publisher/apps/:app_uid

Method - DELETE

Params - app_uid in url

Use with care. This will delete the app and all history related with app including number of sessions played and other stats. This can't be undone.

E.g - 

    curl -X DELETE -H "auth_key: c0c40350-0a16-0130-850c-asdfasdfasdf"
                      "http://api.appsurfer.com/v1/publisher/apps/f9dce550-0sdfa3a-sdf30-e0e8-12313d053c1b"
