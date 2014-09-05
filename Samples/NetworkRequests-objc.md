[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) | Model can Process Response From Network Request

#### Description
Example unit test to confirm that a model class can properly process a response from an asynchronous request over the network.  Uses Grand Central Dispatch (GCD) semaphores to wait for asynchronously dispatched blocks to finish.  [Credit](http://www.g8production.com/post/76942348764/wait-for-blocks-execution-using-a-dispatch-semaphore)

This allows for confirming:

* The url request is formed correctly
* The response did not return an error
* The response has a status code of 200
* The response provided data
* The reponse data has the expected structure 
* Confirm ability to parse response
 
#### Code Sample

	- (void)testFetchingFoursquareVenues {
	    
	    //create a semaphore with initial value
	    dispatch_semaphore_t semaphore = dispatch_semaphore_create(0);
	    
	    NSURL *url = [NSURL URLWithString:@"https://api.yourawesome.com"];
	    
	    NSURLSessionDataTask *task = [self.session dataTaskWithURL:url completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
	        
	        XCTAssertNil(error, @"NSURLSessionDataTask returned completed with Error: %@", error);
	        
	        NSHTTPURLResponse *httpResponse = (NSHTTPURLResponse *)response;
	        
	        NSInteger statusCode = [httpResponse statusCode];
	        
	        XCTAssertEqual(statusCode, 200, @"NSURLSessionDataTask did not complete with status code 200. Check the request URL.  Returned Status Code of: %ld", (long)statusCode);
	        
	        if(statusCode == 200) {
	            
	            XCTAssertNotNil(data, @"NSURLSessionDataTask did not return data");
	            
	            NSDictionary *responseDict = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingAllowFragments error:nil];
	            
	            NSArray *collectionOfStuff = [MyFetcher serializeToVenueCollectionForResponse:responseDict];
	            
	            XCTAssertTrue(collectionOfStuff.count > 0, @"Failed to serialize to a collection of stuff");
	            
	            MyStuff *stuff = [collectionOfStuff lastObject];
	            
	            XCTAssertTrue([venue isKindOfClass:[MyStuff class]], @"Collection does not have objects of type MyStuff");
	            
	            //increment the semaphore
	            dispatch_semaphore_signal(semaphore);
	        }
	    }];
	    
	    [task resume];
	    
	    //decrement the semaphore
	    long rc = dispatch_semaphore_wait(semaphore, dispatch_time(DISPATCH_TIME_NOW, 2.0 * NSEC_PER_SEC));
	    
	    XCTAssertEqual(rc, 0, @"Network request timed out.");
	}