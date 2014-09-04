[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns)

#### Description

Example unit tests for Controller class that is composed of a CLLocationManager and adopts the CLLocationManagerDelegate protocol.

#### Code Sample
	
	@interface MyViewControllerTest : XCTestCase
	
	@property (nonatomic, strong) MyViewController *viewControllerUnderTest;
	
	@end
	
	@implementation MyViewControllerTest
	
	- (void)setUp
	{
	    [super setUp];
	    
	    self.viewControllerUnderTest = [[MyViewController alloc] initWithNibName:@"MyViewController" bundle:nil];
	    
	    //load the controller's view hierarchy
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(loadView) withObject:nil waitUntilDone:YES];
	    
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(viewDidLoad) withObject:nil waitUntilDone:YES];
	}
	
	- (void)tearDown
	{
	    self.viewControllerUnderTest = nil;
	    
	    [super tearDown];
	}
	
	- (void)testControllerConformsToCLLocationManagerProtocol {
	    
	    XCTAssert([self.viewControllerUnderTest conformsToProtocol:@protocol(CLLocationManagerDelegate)], @"ViewController under test does not adopt the CLLocationManagerProtocol");
	}
	
	- (void)testControllerImplementsCLLocationManagerProtocolMethods {
	    
	    XCTAssert([self.viewControllerUnderTest respondsToSelector:@selector(locationManager:didUpdateLocations:)], @"ViewController does not implement locationManager:didUpdateLocations");
	    
	    XCTAssert([self.viewControllerUnderTest respondsToSelector:@selector(locationManager:didFailWithError:)], @"ViewController does not implement locationManager:didFailWithError");
	    
	    //continue with other protocol methods that require implementation
	}
	
	@end