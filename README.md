# test-appd
AppDynamics test app


-----------------------------------------Test App--------------------------------

<html>
<script charset='UTF-8'>
window['adrum-start-time'] = new Date().getTime();
(function(config){
    config.appKey = 'EUM-AAB-AUA';
    config.adrumExtUrlHttp = 'http://cdn.appdynamics.com';
    config.adrumExtUrlHttps = 'https://cdn.appdynamics.com';
    config.beaconUrlHttp = 'AppDEUM';
    config.beaconUrlHttps = 'AppDEUM';
    config.xd = {enable : false};
})(window['adrum-config'] || (window['adrum-config'] = {}));
if ('https:' === document.location.protocol) {
    document.write(unescape('%3Cscript')
 + " src='https://cdn.appdynamics.com/adrum/adrum-4.4.3.717.js' "
 + " type='text/javascript' charset='UTF-8'" 
 + unescape('%3E%3C/script%3E'));
} else {
    document.write(unescape('%3Cscript')
 + " src='http://cdn.appdynamics.com/adrum/adrum-4.4.3.717.js' "
 + " type='text/javascript' charset='UTF-8'" 
 + unescape('%3E%3C/script%3E'));
}
</script>
<!-- 5. CHANGEME: Define the rate at which the page needs to be refreshed. 
	Minimum value should be 12 seconds to accommodate Ajax request and adrum submission of Ajax request. -->
<meta http-equiv="refresh" content="20">
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
<meta http-equiv="Pragma" content="no-cache" />
<meta http-equiv="Expires" content="0" />
<title>Appdynamics BRUM Test page</title>
  <style type="text/css" media="screen">
  /************************************************************************
  Type Writer effect credit goes to : https://css-tricks.com/snippets/css/typewriter-effect/
  Under the license agreement from the Author: https://css-tricks.com/license/
  ************************************************************************/
      /* DEMO-SPECIFIC STYLES */
      .typewriter h1 {
        color: #000;
        width: 40%;
        margin-left: 25%
        font-family: monospace;
        overflow: hidden; /* Ensures the content is not revealed until the animation */
        border-right: .15em solid orange; /* The typwriter cursor */
        white-space: nowrap; /* Keeps the content on a single line */
        margin: 0 auto; /* Gives that scrolling effect as the typing happens */
        letter-spacing: .15em; /* Adjust as needed */
        animation: 
          typing 3.0s steps(25, end),
          blink-caret .5s step-end infinite;
      }

      /* The typing effect */
      @keyframes typing {
        from { width: 0 }
        to { width: 40% }
      }

      /* The typewriter cursor effect */
      @keyframes blink-caret {
        from, to { border-color: transparent }
        40% { border-color: orange }
      }  
</style>
<script>
function getRandomInt() {
  //The maximum is exclusive and the minimum is inclusive
  min = 1;
  max = 10;
  return Math.floor(Math.random() * (max - min)) + min; 
}

var avatarNames = ['', 'calebogden', 'josephstein', 'olegpogodaev', 'marcoramires', 'stephenmoon', 'bigmancho', 'follettkyle', 'araa3185', 'vivekprvr', 'russoedu']

function loadDoc() {
  var ajaxT = new ADRUM.events.Ajax();
  ajaxT.url('User-Ajax-Test');
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4) {
    	ajaxT.markFirstByteTime((new Date()).getUTCMilliseconds());
        ajaxT.markRespAvailTime((new Date()).getUTCMilliseconds());
      if (this.status == 200) {
	      //var userObj = (JSON.parse(this.responseText)).data;
        var userObj = JSON.parse(this.responseText);
	      document.getElementById("usrId").innerHTML = userObj.id;
	      document.getElementById("usrFN").innerHTML = userObj.name;
	      document.getElementById("usrLN").innerHTML = userObj.username;
        document.getElementById("company").innerHTML = userObj.company.name;
        document.getElementById("avatar").src = 'https://s3.amazonaws.com/uifaces/faces/twitter/'+ avatarNames[getRandomInt()] +'/128.jpg';
	  } else {
	  	// Mark Error
	  	var errorT = new ADRUM.events.Error({
	  		msg: 'Ajax Request Error',
	  		line: 96
	  	});
	  	ADRUM.report(errorT);

	  }
	  	ajaxT.markRespProcTime((new Date()).getUTCMilliseconds());
	  	ADRUM.report(ajaxT);
    }
  };
  xhttp.open("GET", "http://jsonplaceholder.typicode.com/users/"+getRandomInt(), true);
  xhttp.send();
  ajaxT.markSendTime((new Date()).getUTCMilliseconds());
}
setTimeout(loadDoc, 2000);
</script>
</head>
<body align="center">
  <img src="https://www.appdynamics.com/media/uploaded-images/1511798348/.thumbnails/appdynamics-340x0_q100.png">
  <p style="width:20%;margin-left: 40%"><marquee>BRUM TEST PAGE</marquee></p>
  <p>Welcome to Appdynamics EUM Test page. In a couple of minutes, you should see snapshots on Appdynamics Controller</p>
  <p><u>NOTE</u>: The geo location may be displayed as unknown, if this page is run from intranet (private ip)</p>

<br><br><br><br>
<h1>Fetching User Details</h1>
<br><br>
<div class="typewriter">
  <h1>Please wait, its an Ajax call!!!</h1>
</div>
<br><br>
<div id="demo"> 
	User Id : <span id="usrId"></span><br>
	First Name : <span id="usrFN"></span><br>
	Last Name : <span id="usrLN"></span><br>
	Works For : <span id="company"></span><br>
  <img id="avatar" src="" />
</div>
</body>
</html>
