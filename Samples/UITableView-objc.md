[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns)

#### Description
Example unit tests for Controller class that is composed of a UITableView and adopts the UITableViewDelegate and UITableViewDataSource protocols.

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
	
	- (void)testViewControllerIsComposedOfTableView {
	    
	    NSArray *subViews = self.viewControllerUnderTest.view.subviews;
	    
	    XCTAssertTrue([subViews containsObject:self.viewControllerUnderTest.tableView], @"ViewController is not composed of a UITableView");
	}
	
	- (void)testViewControllerImplementsUITableViewDatasourceProtocolMethods {
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(numberOfSectionsInTableView:)], @"ViewController under test does not implement numberOfSectionsInTableView protocol method");
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(tableView:numberOfRowsInSection:)], @"ViewController under test does not implement numberOfRowsInSection protocol method");
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(tableView:cellForRowAtIndexPath:)], @"ViewController under test does not implement cellForRowAtIndexPath");
	    
	    //continue with other UITableViewDataSource protocol methods of interest ...
	}
	
	- (void)testViewControllerConformsToTableViewDataSource {
	    
	    XCTAssertTrue([self.viewControllerUnderTest conformsToProtocol:@protocol(UITableViewDataSource)], @"ViewController under test does not conform to the UITableViewDataSource prototocol");
	}
	
	- (void)testViewControllerImplementsUITableViewDelegateProtocolMethods {
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(tableView:didSelectRowAtIndexPath:)], @"ViewController under test does not implement tableView:didSelectRowAtIndexPath: protocol method");
	    
	    //continue with other UITableViewDelegate protocol methods of interest ...
	}
	
	- (void)testViewControllerConformsToTableViewDelegate {
	    
	    XCTAssertTrue([self.viewControllerUnderTest conformsToProtocol:@protocol(UITableViewDelegate)], @"ViewController under test does not conform to the UITableViewDelegate protocol.");
	}
	
	- (void)testTableViewCellsHaveCorrectTextLabel {
	    
	    NSIndexPath *rowIndex0 = [NSIndexPath indexPathForRow:0 inSection:0];
	    
	    UITableViewCell *cell0 = [self.viewControllerUnderTest tableView:self.viewControllerUnderTest.tableView cellForRowAtIndexPath:rowIndex0];
	    
	    XCTAssert([cell0.textLabel.text isEqualToString:@"ENTER-TEXT-OF-INTEREST"], @"ViewController under test is composed of a UITableView that has improperly initialized UITableViewCells");
	    
	    
	    NSIndexPath *rowIndex1 = [NSIndexPath indexPathForRow:1 inSection:0];
	    
	    UITableViewCell *cell1 = [self.viewControllerUnderTest tableView:self.viewControllerUnderTest.tableView cellForRowAtIndexPath:rowIndex1];
	    
	    XCTAssert([cell1.textLabel.text isEqualToString:@"ENTER-TEXT-OF-INTEREST"], @"ViewController under test is composed of a UITableView that has improperly initialized UITableViewCells");
	}
	
	@end