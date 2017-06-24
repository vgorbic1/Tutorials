## Ajax
In the WordPress interface when you write a new post, you can add or remove tags and categories
without refreshing the whole page: This is Ajax.

Ajax is a web development technique that enables a page to retrieve data asynchronously, in the
background, and to update parts of the page without reloading it. The word originally stands as
an acronym for Asynchronous JavaScript And XML, but despite its name the use of XML is not
actually mandatory. You can sometimes read it as AJAX, but the form Ajax is more widely adopted.

Ajax is not a technology or a programming language but a group of technologies: It involves client -
side scripts such as JavaScript and server - side script such as PHP that outputs content in HTML,
CSS, XML, and JSON — or actually mostly anything.

Due to browser security restrictions, most Ajax requests cannot successfully retrieve
data from a different domain, subdomain, or even protocol. JSONP requests are not subject to the same 
origin policy restrictions.

A sample script:
```html
<html>
	<head>
		<title> Ajax Example </title>
		<script src='http://code.jquery.com/jquery-1.4.2.js'> </script>
	</head>
	<body>
		<h1> Ajax example, reading JSON response </h1>
		<p> View <a id="load" href="http://twitter.com/ozh"> Ozh' latest tweets </a>
		</p>
		<div id="tweets"> </div>
		<script type="text/javascript">
		// When the DOM is ready, add behavior to the link
		$(document).ready(function(){
			$('#load').click(function(){
				load_tweets();
				// Skip default behavior (ie sending to the link href)
				return false;
			});
		});
		// Main function: load tweets in JSON
		function load_tweets() {
			// Activity indicator:
			$('#tweets').html('loading tweets...');
			// Ajax JSON request
			$.getJSON(
				'http://twitter.com/status/user_timeline/ozh.json?count=5 & callback=?',
				// Callback function with JSON response
				function(data) {
					// Put empty <ul> in the placeholder
					$('#tweets').html(' <ul> </ul> ');
					// Read each object in the JSON response and add text to the <ul>
					$(data).each(function(i, tweet) {
						$('#tweets ul').append(' <li> '+tweet.text+' </li> ');
					});
				}
			);
		}
		</script>
	</body>
</html>
```
Ajax popularized the usage of tiny animated images, called throbbers, to
indicate background activity. Sites such as http://ajaxload.info/ enable you
to create your own images that match your design.
