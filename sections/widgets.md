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

