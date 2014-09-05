[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) | ViewController (with xib) composed of UIPickerView

#### Description
Example unit tests for a ViewController class that is composed of a UIPickerView and adopts the UIPickerViewDelegate and UIPickerViewDataSource protocols.

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
	
	- (void)testViewControllerIsComposedOfUIPickerView {
	    
	    NSArray *subviews = [self.viewControllerUnderTest.view subviews];
	    
	    XCTAssertTrue([subviews containsObject:self.viewControllerUnderTest.pickerView], @"ViewController under test is not composed of a UIPickerView");
	}
	
	- (void)testViewControllerImplementsUIPickerViewDataSourceProtocolMethods {
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(numberOfComponentsInPickerView:)], @"ViewController under test does not implement numberOfComponentsInPickerView: protocol method");
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(pickerView:numberOfRowsInComponent:)], @"ViewController under test does not implement pickerView:numberOfRowsInComponent: protocol method");
	}
	
	- (void)testUIPickerViewConformsToUIPickerViewDataSource {
	    
	    XCTAssert([self.viewControllerUnderTest conformsToProtocol:@protocol(UIPickerViewDataSource)], @"ViewController under test does not conform to the UIPickerViewDataSource protocol");
	}
	
	- (void)testViewControllerImplementsUIPickerViewDelegateMethods {
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(pickerView:titleForRow:forComponent:)], @"ViewController under test does not implement pickerView:titleForRow:forComponent:");
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(pickerView:didSelectRow:inComponent:)], @"ViewController under test does not implement pickerView:didSelectRow:inComponent:");
	}
	
	- (void)testUIPickerViewConformsToUIPickerViewDelegate {
	    
	    XCTAssert([self.viewControllerUnderTest conformsToProtocol:@protocol(UIPickerViewDelegate)], @"ViewController under test does not conform to the UIPickerViewDelegate protocol");
	}
	
	- (void)testPickerViewHasCorrectRowLabel {
	    
	    //simulate selecting row 0 in the UIPickerView (i.e. Luke)
	    [self.viewControllerUnderTest.pickerView selectRow:0 inComponent:0 animated:NO];
	    
	    //get the corresponding value for the selected row
	    NSString *luke = [self.viewControllerUnderTest.pickerData objectAtIndex:[self.viewControllerUnderTest.pickerView selectedRowInComponent:0]];
	    
	    XCTAssertEqualObjects(luke, @"Luke", @"UIPickerView has incorrect row value");
	    
	    
	    //simulate selecting row 1 in the UIPickerView (i.e. Leia)
	    [self.viewControllerUnderTest.pickerView selectRow:1 inComponent:0 animated:NO];
	    
	    //get the corresponding value for the selected row
	    NSString *leia = [self.viewControllerUnderTest.pickerData objectAtIndex:[self.viewControllerUnderTest.pickerView selectedRowInComponent:0]];
	    
	    XCTAssertEqualObjects(leia, @"Leia", @"UIPickerView has incorrect row value");
	}
	
	//continue with App-specific tests ...
	
	@end