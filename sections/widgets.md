## Get widget code -

AppSurfer widgets come in two types as - widgets for mobile size and tablet size. Both these types can be customised with various options as per need.


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
    <tr>
    <td> widget_type </td>
    <td> phone / tablet </td>
    <td> - phone: returns widget type phone which takes maximum size of 620px620px or less depending on cusmisation. This will be default option. <br/><br/>
    - tablet: returns widget type tablet which takes minimum size of 600px*600px. If given more height and width, tablet widget's can utilize that. </td>
  </tr>
  <tr>
    <td> orientation </td>
    <td> landscape / portrait </td>
    <td> Depending on default_orientation given for app, it will default to landscape or portrait. <br/><br/>
    - landscape: phone loads up in landscape orientation <br/><br/>
    - portrait: phone loads up in portrait orientation </td>
  </tr>
  <tr>
    <td> controls_needed </td>
    <td> boolean </td>
    <td> Default is false. If set to true, it will show buttons for 'GPS data send', 'Toggle Orientation', 'Start Tablet Mode', 'Toggle Accelerometer mode'. Recommeded if app requires any of features like gps data or accelerometer input. </td>
  </tr>
  <tr>
    <td> header_needed </td>
    <td> boolean </td>
    <td> Default if false. If set to true, it will add an info bar to widget with app logo, app name, publisher name and buttons like - 'share' and 'install'.  </td>
  </tr>
  <tr>
    <td> locale </td>
    <td> string </td>
    <td> Optional. For e.g. en_US, fr_CA. Sets locale for this particular widget.  </td>
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

