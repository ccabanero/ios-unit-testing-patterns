[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) 

#### Description
Example unit tests for a ViewController class (in a Storyboard) that is composed of a UITableView and adopts the UITableViewDelegate and UITableViewDataSource protocols.

#### Code Sample
	import UIKit
	import XCTest
	
	class ExampleTests: XCTestCase {
	
	    //note: remember to add the Main.storyboard and ViewController under test as a member of the test target (via file inspector)
	    
	    //declaring the ViewController under test as an implicitly unwrapped optional
	    var viewControllerUnderTest : ViewController!
	    
	    override func setUp() {
	        super.setUp()
	        
	        //get the storyboard the ViewController under test is inside
	        var storyboard: UIStoryboard = UIStoryboard(name: "Main", bundle: NSBundle(forClass: self.dynamicType))
	        
	        //get the ViewController we want to test from the storyboard (note the identifier is the id explicitly set in the identity inspector)
	        self.viewControllerUnderTest = storyboard.instantiateViewControllerWithIdentifier("MyViewController") as ViewController
	        
	        //load view hierarchy
	        if(self.viewControllerUnderTest != nil) {
	            
	            self.viewControllerUnderTest.loadView()
	            self.viewControllerUnderTest.viewDidLoad()
	        }
	    }
	    
	    func testViewControllerIsComposedOfTableView() {
	        
	        XCTAssertNotNil(self.viewControllerUnderTest.tableView, "ViewController under test is not composed of a UITableView")
	    }
	    
	    func testViewControllerConformsToTableViewDataSource() {
	        
	        XCTAssert(self.viewControllerUnderTest.conformsToProtocol(UITableViewDataSource), "ViewController under test does not conform to the UITableViewDataSource prototocol")
	        
	        XCTAssert(self.viewControllerUnderTest.respondsToSelector(Selector("numberOfSectionsInTableView:")), "ViewController under test does not implement numberOfSectionsInTableView protocol method")
	        
	        XCTAssert(self.viewControllerUnderTest.respondsToSelector(Selector("tableView:numberOfRowsInSection:")), "ViewController under test does not implement tableView:numberOfRowsInSection protocol method")
	        
	        XCTAssert(self.viewControllerUnderTest.respondsToSelector(Selector("tableView:cellForRowAtIndexPath:")), "ViewController under test does not implement tableView:cellForRowAtIndexPath")
	    }
	    
	    func testViewControllerConformsToTableViewDelegateProtocol() {
	    
	        XCTAssert(self.viewControllerUnderTest.conformsToProtocol(UITableViewDelegate), "ViewController under test does not conform to the UITableViewDelegate protocol.")
	        
	        XCTAssert(self.viewControllerUnderTest.respondsToSelector(Selector("tableView:didSelectRowAtIndexPath:")), "ViewController under test does not implement tableView:didSelectRowAtIndexPath: protocol method")
	    }
	    
	    //continue with App-specific tests ...
	}