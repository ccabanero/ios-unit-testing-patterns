[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) 

#### Description
Example unit tests for a ViewController class (in a storyboard) that is composed of a UILabel.

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
	    
	    override func tearDown() {
	        
	        self.viewControllerUnderTest = nil
	        
	        super.tearDown()
	    }
	    
	    func testViewControllerIsComposedOfLabel() {
	
	        XCTAssertNotNil(self.viewControllerUnderTest.label, "ViewController under test is not composed of a UILabel")
	    }
	    
	    func testViewControllerInitializesLabelText() {
	        
	         XCTAssert(self.viewControllerUnderTest.label.text == "Vader", "ViewController under test does not initialize the text property of UILabel correctly")
	    }
	}
