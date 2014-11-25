<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<div id="fb-root"></div>
<style>
#albumImage{
	padding:5px;
	font-size:14px;
	width:800px;
	float:right;
	text-align:center;
	margin:0px;
}	

#album{
	width:650px;
	text-align:center;
	float:left;
	border:solid 0px #Ff0000;
	padding:5px;
}	

#album .img{
	margin:5px;
	float:left;
	width:150px;
	border:solid 1px #cccccc;
	cursor:pointer;
}	

#album .title{
	border-top:solid 1px #cccccc;
	background-color:#dfdfdf;
	padding:5px;
	font-size:12px;
}
#fbtitle{
	border-top:solid 1px #cccccc;
	background-color:#dfdfdf;
	padding:5px;
	font-size:14px;
	width:633px;
	text-align:center;
	margin-left:2%;
	float:left;
}	

#albumPicturesTitle{
	border:solid 1px #cccccc;
	background-color:#dfdfdf;
	padding:5px;
	font-size:14px;
	width:800px;
	text-align:center;
}	

#albumPictures{
	width:800px;
	text-align:center;
	margin-left:25%
	float:left;
	border:solid 0px #Ff0000;
	padding:5px;
}	
#albumPictures .img{
	width:180px;
	text-align:center;
	float:left;
	border:solid 0px #Ff0000;
	padding:1px;
	margin:5px;
	border:solid 1px #cccccc;
	position:relative;
}	

</style>
<div id="albumImage">
	<div id="albumPicturesTitle">All Ablum Pictures</div>
	<div id="albumPictures"></div>
</div>
<div id="fbtitle"><a href="javascript:void(0)" onclick="FBLogin()">Get Album List</a></div>
<div>
<div id="album"></div>

</div>
<script>
  window.fbAsyncInit = function() {
  FB.init({
    appId      : '666157133451032',
    status     : true, // check login status
    cookie     : true, // enable cookies to allow the server to access the session
    xfbml      : true  // parse XFBML
  });
    FB.Event.subscribe('auth.authResponseChange', function(response) {
    if (response.status === 'connected') {
    } else if (response.status === 'not_authorized') {
      FBLogin();
    } else {
      FBlogin()
    }
  });
  };
(function(d){
   var js, id = 'facebook-jssdk', ref = d.getElementsByTagName('script')[0];
   if (d.getElementById(id)) {return;}
   js = d.createElement('script'); js.id = id; js.async = true;
   js.src = "http://connect.facebook.net/en_US/all/vb.js";
   ref.parentNode.insertBefore(js, ref);
  }(document));
  
  
function FBLogin(){
 FB.login(function(response) {
    if (response.authResponse) {
    FB.api('/me/albums', function(response) {
	for (album in response.data) {
		 
		 var albumName=response.data[album].name;
		 alert(albumName);
		 if(albumName.length>=16){
			var albumName = albumName.substring(0,10);
			var albumName=albumName+'..';
		 }
		 var picsCount=response.data[album].count;
		 if(picsCount==undefined){
			picsCount='';
		 }
		 var albumId=response.data[album].id;
		 // Get Album Cover Picture for each album
			 FB.api("/"+albumId+"/picture",function (response) {
					if (response && !response.error) {
					var albumCoverPicture=response.data.url;
					//console.log(JSON.stringify(response));
						var	elem='<div class="img" id="'+albumId+'" onclick="getAllAlbumPicture('+albumId+')"><img src="'+albumCoverPicture+'" width="150" height="150"/><div class="title">'+albumName+'('+picsCount+')</div></div>';
						$('#album').append(elem);
					}
			}
		);
		
	  }
	 });
   } else {
   		removeFB();
   }
 },{scope:'email,user_birthday,status_update,publish_stream,user_about_me,user_photos'});
} 
function FBLogout(){
	FB.logout(function(response) {
});	
}


function getAllAlbumPicture(albumid){
FB.api("/"+albumid+"/photos",function (responses) {
	if (responses && !responses.error) {
		console.log(JSON.stringify(responses));
		for(picture in responses.data){
			var albumPicture=responses.data[picture].source;
			var element='<div class="img"><img src='+albumPicture+' width="180" height="180"></div>';
			$('#albumPictures').append(element);
		}
	}
});
}
</script>
