[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) | ViewController (with xib) composed of UISegmentedControl

#### Description
Example unit tests for a ViewViewController class that is composed of a UISegmentedControl and uses the Target-Action pattern to handle control events.

#### Code Sample
	#import <XCTest/XCTest.h>
	#import "MyViewController.h"
	
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
	
	- (void)testViewControllerIsComposedOfUISegmentedControl {
	    
	    NSArray *subviews = [self.viewControllerUnderTest.view subviews];
	    
	    XCTAssertTrue([subviews containsObject:self.viewControllerUnderTest.segmentedControl], @"ViewController under test does not have a UISegmentedControl in its view hierarchy");
	}
	
	- (void)testSegmentedControlTitleInitialization {
	    
	    //simulate selecting first segment
	    NSString *titleForSegmentAtIndex0 = [self.viewControllerUnderTest.segmentedControl titleForSegmentAtIndex:0];
	    
	    XCTAssertEqualObjects(@"Map", titleForSegmentAtIndex0, @"UISegmentedControl improperly initialized - title of segment at index 0 is incorrect");
	    
	    NSString *titleForSegmentAtIndex1 = [self.viewControllerUnderTest.segmentedControl titleForSegmentAtIndex:1];
	    
	    XCTAssertEqualObjects(@"List", titleForSegmentAtIndex1, @"UISegmentedControl improperly initialized - title of segment at index 1 is incorrect");
	}
	
	- (void)testSegmentedControlNumberOfSegmentInitialization {
	    
	    XCTAssertEqual([self.viewControllerUnderTest.segmentedControl numberOfSegments], 2, @"UISegmentedControl improperly initialized - does not have expected number of segments");
	}
	
	- (void)testSegmentedControlTriggersActionMethod {
	    
	    XCTAssert([self.viewControllerUnderTest.segmentedControl actionsForTarget:self.viewControllerUnderTest forControlEvent:UIControlEventValueChanged], @"SegmentedControl does not triffer action method ValueChanged");
	}
	
	//continue with App-specific tests ...
	
	@end