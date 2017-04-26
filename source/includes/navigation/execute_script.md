## Execute Script


> Definition

```shell
# API call described below requires shell access, either login to the device by connecting a monitor or use ssh for remote login.

ROS-Service Name: /<namespace>/navigation/exec_script
ROS-Service Type: core_api/ExecScript, below is its description

#Request : Expects name of the application to execute and the arguments to be passed to it
string app_name
string arguments

#Response : return success=true if script starts to get executed
bool success
```

```cpp
No CPP API is available for execution of onboard scripts.
```

```python
# Python API described below can be used in onboard scripts only. For remote scripts you can use http client libraries to call FlytOS REST endpoints from python.

NotImplemented
```

```cpp--ros
// ROS services and topics are accessible from onboard scripts only.

Type: Ros Service
Name: /<namespace>/navigation/exec_script
call srv:
    :string app_name
    :string arguments
response srv: bool success
```

```python--ros
# ROS services and topics are accessible from onboard scripts only.

Type: Ros Service
Name: /<namespace>/navigation/exec_script
call srv:
    :string app_name
    :string arguments
response srv: bool success

```

```javascript--REST
This is a REST call for the API. Make sure to replace 
    ip: ip of the FlytOS running device
    namespace: namespace used by the FlytOS device.

URL: 'http://<ip>/ros/<namespace>/navigation/exec_script'

JSON Request:
{   app_name : String,
    arguments : String }

JSON Response:
{   success: Boolean, }

```

```javascript--Websocket
This is a Websocket call for the API. Make sure you 
initialise the websocket using websocket initialisng 
API and and replace namespace with the namespace of 
the FlytOS running device before calling the API 
with websocket.

name: '/<namespace>/navigation/exec_script',
serviceType: 'core_api/ExecScript'

Request:
{   app_name : String,
    arguments : String }

Response:
{   success: Boolean, }


```


> Example

```shell
rosservice call /<namespace>/navigation/exec_script "{}"
```

```cpp
```

```python

NotImplemented

```

```cpp--ros
#include <core_api/ExecScript.h>

ros::NodeHandle nh;
ros::ServiceClient client = nh.serviceClient<core_api::ExecScript>("/<namespace>/navigation/exec_script");
core_api::ExecScript srv;

srv.request.app_name = "sample_script.sh";
srv.request.arguments = "arg1 arg2 arg3";
client.call(srv);
success = srv.response.success;
```

```python--ros
from core_api.srv import *

script_name = "sample_script.sh"
sample_args = "arg1 arg2 arg3"
def exec_script(script_name, sample_args):
    rospy.wait_for_service('/<namespace>/navigation/exec_script')
    try:
        handle = rospy.ServiceProxy('/<namespace>/navigation/exec_script', ExecScript)
        resp = handle(app_name=script_name, arguments= sample_args)
        return resp
    except rospy.ServiceException, e:
        rospy.logerr("service call failed %s", e)

```

```javascript--REST
var  msgdata={};
msgdata["app_name"]='app12';
msgdata["arguments"]='2 45 4 run';

$.ajax({
    type: "POST",
    dataType: "json",
    data: JSON.stringify(msgdata),
    url: "http://<ip>/ros/<namespace>/navigation/exec_script",  
    success: function(data){
           console.log(data.success);
    }
};

```

```javascript--Websocket
var execScript = new ROSLIB.Service({
    ros : ros,
    name : '/<namespace>/navigation/exec_script',
    serviceType : 'core_api/ExecScript'
});

var request = new ROSLIB.ServiceRequest({    
    app_name : 'app12',
    arguments : '2 45 4 run'
});

execScript.callService(request, function(result) {
    console.log('Result for service call on '
      + execScript.name
      + ': '
      + result.success);
});
```


> Example response

```shell
success: true
```

```cpp
```

```python
NotImplemented
```

```cpp--ros
success: True
```

```python--ros
Success: True
```

```javascript--REST
{
    success:True
}

```

```javascript--Websocket
{
    success:True
}

```





###Description:

This API can run onboard executable scripts in python, shell, etc. 

###Parameters:
    
    Following parameters are applicable for onboard cpp and python scripts. Scroll down for their counterparts in RESTFul, Websocket, ROS. However the description of these parameters applies to all platforms. 
    
    Arguments:
    
    Argument | Type | Description
    -------------- | -------------- | --------------
    app_name | string | Name of the script. Script should be present in /flyt/flytapps/onboard/install directory.
    arguments | string | arguments separated by space e.g. "arg1 arg2 arg3"
    
    Output:
    
    Parameter | Type | Description
    ---------- | ---------- | ------------
    success | bool | true if action successful

### ROS endpoint:
Navigation APIs in FlytOS are derived from / wrapped around the core navigation services in ROS. Onboard service clients in rospy / roscpp can call these APIs. Take a look at roscpp and rospy api definition for message structure. 

* Type: Ros Service</br> 
* Name: /\<namespace\>/navigation/exec_script</br>
* Service Type: ExecScript

### RESTFul endpoint:
FlytOS hosts a RESTFul server which listens on port 80. RESTFul APIs can be called from remote platform of your choice.

* URL: ``POST http://<ip>/ros/<namespace>/navigation/exec_script``
* JSON Request:
{
    app_name : String,
    arguments : String
}
* JSON Response:
{
    success: Boolean
}


### Websocket endpoint:
Websocket APIs can be called from javascript using  [roslibjs library.](https://github.com/RobotWebTools/roslibjs) 
Java websocket clients are supported using [rosjava.](http://wiki.ros.org/rosjava)

* name: '/\<namespace\>/navigation/exec_script'</br>
* serviceType: 'core_api/ExecScript'


### API usage information:

* Note that the executable should be present in /flyt/flytapps/onboard/install directory.