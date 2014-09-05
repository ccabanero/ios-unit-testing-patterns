#### Description
Example unit tests for a ViewController class that is composed of a UILabel.

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
	    
	    //load the view hierarchy
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(loadView) withObject:nil waitUntilDone:YES];
	    
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(viewDidLoad) withObject:nil waitUntilDone:YES];
	}
	
	- (void)tearDown
	{
	    self.viewControllerUnderTest = nil;
	    
	    [super tearDown];
	}
	
	- (void)testViewControllerHasLabel {
	    
	    NSArray *subviews = self.viewControllerUnderTest.view.subviews;
	    
	    XCTAssertTrue([subviews containsObject:self.viewControllerUnderTest.label], @"ViewController under test is not composed of a UILabel");
	}
	
	- (void)testLabelInitialization {
	    
	    XCTAssertEqualObjects(self.viewControllerUnderTest.label.text, @"Vader", @"ViewController under test does not properly initialize the label text property");
	}
	
	//continue with App-specific tests ...
	
	@end