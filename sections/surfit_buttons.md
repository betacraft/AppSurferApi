## Get Surf it button code - 

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
