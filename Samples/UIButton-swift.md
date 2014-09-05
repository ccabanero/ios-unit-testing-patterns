[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) | ViewController (in Storyboard) composed of UIButton

#### Description
Example unit tests for a ViewController class (in a Storyboard) that is composed of a UIButton and uses the Target-Action pattern to handle button events.

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
	    
	    func testViewControllerIsNotComposedOfButton() {
	        
	        XCTAssertNotNil(self.viewControllerUnderTest.button, "Button not in view hierarchy of ViewController under test")
	    }
	    
	    func testButtonTriggersActionMethod() {
	        
	        XCTAssertNotNil(self.viewControllerUnderTest.button.actionsForTarget(self.viewControllerUnderTest, forControlEvent:UIControlEvents.TouchUpInside), "Button does not trigger action method on TouchUpInside event")
	    }
	}