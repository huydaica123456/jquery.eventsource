# jQuery.EventSource

## 2011-05-30 Update: Tests passing 100% in Firefox/Aurora 6

# TODO: Rewrite with jQuery Deferred Objects


Gives developers the power of the EventSource API across browsers. Uses the EventSource constructor when natively available 
and falls back to Ajax polling logic when it's not. Contributions must conform to [Idiomatic Style Manifesto](https://github.com/rwldrn/idiomatic.js)


[http://wiki.github.com/rwldrn/jquery.eventsource/](http://wiki.github.com/rwldrn/jquery.eventsource/)


[http://code.bocoup.com/jquery.eventsource/unit-tests/](http://code.bocoup.com/jquery.eventsource/unit-tests/)


## Some Thoughts...

* Q. why use EventSource rather than Websockets?<br>
	A. EventSource is easier to setup on server (uses http), lighter and most of the times - that's what you acually need. (via temp01)


## Real World Example

[http://yakyakface.com/](http://yakyakface.com/)


## Provides cross browser implementation for:

[http://dev.w3.org/html5/eventsource/](http://dev.w3.org/html5/eventsource/)


## Unit tests

[http://yakyakface.com/jquery.eventsource/unit-tests/](http://yakyakface.com/jquery.eventsource/unit-tests/)


For a libray agnostic polyfill that offers base implementation fallback, check out Remy Sharp's work here:
[pollyfills/EventSource.js](https://github.com/remy/polyfills/blob/master/EventSource.js)


## Usage

		$.eventsource({
			
			// Assign a label to this event source
			
			label: "event-source-label", 

			// Set the file to receive data from the server

			url: "event-sources/server-event-source.php",
			
			// Set the type of data you expect to be returned
			// text, json supported
			
			dataType: "json", 
			
			// Set a callback to fire when the event source is opened
			// `onopen`
			open: function( data ) {


				console.log( data );

			},

			// Set a callback to fire when a message is received
			// `onmessage`
			message: function( data ) {


				console.log( data );

			}
		});
		
		
		// Close event sources by label name
		
		$.eventsource("close", "event-source-label");
		

## Varied Content Type Usage

		
		// PLAIN TEXT EXAMPLE - NO CONTENT TYPE GIVEN
		$.eventsource({
			label: "text-event-source",
			url: "test-event-sources/text-event-source.php",
			open: function() {

				console.log( "opened" );

			},
			message: function( data ) {

				console.log( data );


				$.eventsource("close", "text-event-source");
			}
		});
		
		// PLAIN TEXT EXAMPLE - HAS CONTENT TYPE
		$.eventsource({
			label: "text-event-source-ct",
			url: "test-event-sources/text-event-source-ct.php",
			dataType: "text",

			message: function( data ) {

				console.log( data );

				$.eventsource("close", "text-event-source-ct");
			}
		});


		// JSON EXAMPLE - HAS CONTENT TYPE
		$.eventsource({
			label: "json-event-source",
			url: "test-event-sources/json-event-source.php",
			dataType: "json",
			open: function() {

				console.log( "opened" );
		
			},
			message: function( data ) {

				console.log( data );

				$.eventsource("close", "json-event-source");
			}
		});		 
		

## Accessing your current event sources:
		
		// Returns an object containing all the currently active eventsource streams
		$.eventsource("streams")

		
## Server Source Requirements
		
		// Server response MUST be Content-Type: text/event-stream
		// Server response MUST be prepended with "data: "

		
		// Examples:
		
		// PHP
		header("Content-Type: text/event-stream\n\n");
		echo "data: this is a valid response";
		
		
		// Python
		print "Content-Type: text/event-stream"
		print "data: this is a valid response"

