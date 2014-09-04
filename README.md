ios-unit-testing-patterns
=========================

Examples of unit testing patterns for iOS projects.


#### Description
Utility class for fetching ***Foursquare Venues*** in ***iOS*** or ***OS*** ***X*** projects.  

####Language
Objective-C

Unit Tests for Controllers

[UITableView](UITableView.md)

####Deployment
Being utility/model classes, simply drop the interface (.h) and implementation (.m) files provided in the ***code*** folder to your Xcode project.

####Code Usage Example
The FoursquareVenueFetcher supports fetching venues using Blocks ...

	[FoursquareVenueFetcher fetchWithLatitude:@"47.60621" withLongitude:@"-122.332071" completion:^(NSArray *results, NSError *error) {

        if(error == nil) {
        
            //iterate collection Foursquare Venue results
            for(NSDictionary *currentVenue in results) {
                
                //print Venue properties
                NSLog(@"Venue Name: %@", [currentVenue objectForKey:@"name"]);
                NSDictionary *categories = [[currentVenue objectForKey:@"categories"] lastObject];
                NSLog(@"Category: %@", [categories objectForKey:@"shortName"]);
                NSDictionary *location = [currentVenue objectForKey:@"location"];
                NSLog(@"City: %@", [location objectForKey:@"city"]);
                NSLog(@"Venue Latitude:%@", [location objectForKey:@"lat"]);
                NSLog(@"Venue Longitude:%@", [location objectForKey:@"lng"]);
            }
        }
        else {
            
            NSLog(@"%@%@", @"Uh oh, here is the error description: ", error.localizedDescription);
        }
    }];
 
The FoursquareVenueFetcher also supports fetching venues using Delegation ...

	Example goes here ....

You will need to configure the Foursquare Client Id and Foursquare Client Secret key for your App.  These can be created [hear](https://foursquare.com/developers/apps).  Then, open up the Constants.m file and update the following:

	@implementation Constants

	/*  CHANGE WITH YOUR FOURSQUARE CLIENT ID   */
	NSString *const FOURSQUARE_CLIENT_ID = @"ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890123456789012";

	/*  CHANGE WITH YOUR FOURSQUARE CLIENT SECRET   */
	NSString *const FOURSQUARE_CLIENT_SECRET = @"ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890123456789012";

	@end

####Unit Tests
Unit tests are provided in the FoursquareVenueFetchterTest.m file using the XCTest framework.  Optionally add these to your project by:

* Copying the FoursquareVenuFetcherTest.m class to your Test target in Xcode
* Run unit tests via Cmd + U

####Sample Project
A sample project is provided in the ***sample-project*** folder which uses the FoursquareVenueFetcher to plot venues by a user's location on a map.
  
####Contact
* Twitter: [@clintcabanero](http://twitter.com/clintcabanero)
* GitHub: [ccabanero](http:///github.com/ccabanero)


####License
See the LICENSE file for more info.

    
