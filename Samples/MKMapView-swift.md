[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns)

#### Description
Example unit tests for a ViewController class (in Storyboard) that is composed of a MKMapView and adopts the MKMapViewDelegate protocol.

#### Code Sample
	import UIKit
	import XCTest
	import MapKit
	
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
	    
	    func testViewControllerIsComposedOfMapView() {
	        
	        XCTAssertNotNil(self.viewControllerUnderTest.mapView, "ViewController under test is not composed of a MKMapView")
	    }
	    
	    func testControllerConformsToMKMapViewDelegate() {
	        
	        XCTAssert(self.viewControllerUnderTest.conformsToProtocol(MKMapViewDelegate), "ViewController under test does not conform to MKMapViewDelegate protocol")
	    }
	    
	    func testControllerImplementsMKMapViewDelegateMethods() {
	    
	        XCTAssert(self.viewControllerUnderTest.respondsToSelector(Selector("mapView:viewForAnnotation:")), "ViewController under test does not implement mapView:viewForAnnotation")
	    }
	    
	    func testMapInitialization() {
	        
	        XCTAssert(self.viewControllerUnderTest.mapView.mapType == MKMapType.Hybrid);
	    }
	    
	    //continue with App-specific tests ...
	}