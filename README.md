iOS Unit Testing Patterns
=========================

### Description

Unit testing code snippets for various iOS development scenarios.

### Language

Swift 4.x

### Unit Testing Framework

XCTest.framework

### Sample Unit Tests for ViewController Classes

__[Working with a ViewController composed of TableViews](https://gist.github.com/ccabanero/39ee6d5fd7b289dee695)__

* Conforms to and implements UITableViewDataSource protocol methods.
* Conforms to and implements UITableViewDelegate protocol methods.

__[Working with a ViewController composed of CollectionViews](https://gist.github.com/ccabanero/6ef47c1aeb21acfb326d30f6b01825d1)__

* Conforms to and implements UICollectionViewDatasource protocol methods.
* Conforms to and implements UICollectionViewDelegate protocol methods.
* Conforms to and implements UICollectionViewDelegateFlowLayout protocol methods.

__[Working with NavigationItems](https://gist.github.com/ccabanero/4a1a4bfbf5fa3fbbb1070c8765c3de73)__

* Testing initialization and state of back button (navigationItem.backBarButtonItem).
* Testing state of custom title view (navigationItem.titleView).
* Testing target-action pattern for Right Bar Button (navigationItem.rightBarButtonItem).
* Testing UIBarButtonItem can pop ViewController from navigation stack.
* [Testing UIRightBarButtonItem has correct custom UIImage when toggled](https://gist.github.com/ccabanero/ed9111e472f6cb283ff8c3e714712efa)

__[Working with a ViewController composed of UISearchBar](https://gist.github.com/ccabanero/0f20b0708c0d756327995e58ff3309d4)__

* Testing initialization and state of search bar after view loads.
* Conforms to SearchBarDelegate protocol methods.
* Testing of auto-suggest behavior between SearchBar.text and UITableView items.
* Testing pre-processing of Search Text when 'Search' button tapped on virtual/soft keyboard.

__Working with Segues between ViewControllers__

* [Storyboard has target Segue](https://gist.github.com/ccabanero/a0fbb675f44a5136d2811d21a77e332a)
* [Testing a Segue is called using a Mock UIViewController](https://gist.github.com/ccabanero/9f7ad6775eacec3cc997)
* [Testing Segue passes data to Target ViewController](https://gist.github.com/ccabanero/308db4882b7ca4967ebb5d17530177f3)
* [Testing ViewController can respond to an Unwind Segue](https://gist.github.com/ccabanero/177a54d2be3694f08c4f3c8f02f74394)

__[Working with a ViewController composed of Custom Views](https://gist.github.com/ccabanero/ac7237e4591092130326)__

* Testing initialization and state of Custom View properties when view loads.

__[Working with a ViewController composed of MKMapView](https://gist.github.com/ccabanero/90c73c46ed1671298775)__

* Testing state of MKMapView after view loads.
* Conforms to and implements MKMapViewDelegate protocol methods.
* Testing MapView adds annotations to the map.
* Testing MapView adds specific types of MKAnnotation.

__[Working with a ViewConroller that uses CoreLocation](https://gist.github.com/ccabanero/dd35e7bee8205ad225f3de1391027aa5)__

* Conforms to and implements CLLocationManager protocol methods.

__[Working with a ViewController composed of a UISegmentedControl](https://gist.github.com/ccabanero/e204496231a41759fa94)__

* Testing initialization and state of UISegmentedControl after view loads.
* Testing UISegmentedControl action method is invoked on change.

__[Working with a ViewController composed of a UIPickerView](https://gist.github.com/ccabanero/8d1dfa65218b8bb10ebf)__

* Testing initialization and state of UIPickerView after view loads.
* Conforms to and implements UIPickerViewDataSource protocol methods.
* Conforms to and implements UIPickerViewDelegate protocol methods.

__[Working with a ViewController composed of a UIButton](https://gist.github.com/ccabanero/b92197516342c0147688)__

* Testing initialization and state of UIButton after view loads.
* Testing target-action pattern of UIButton.

__[Working with a ViewController composed of a UILabel](https://gist.github.com/ccabanero/68cd8ff461316930f707)__

* Testing initialization and state of UILabel after view loads.
* Testing label state after invoking the action methods of other controls.


__[Working with a ViewController that presents a UIAlertController](https://gist.github.com/ccabanero/b88a77caba37f8dd9fbf)__

* Using a mock ViewController to confirm launching UIAlertViewController
* Testing the initialization and state of UIAlertController once presented.

### Sample Unit Tests for Model Classes

[Testing Model Class Initialization](https://gist.github.com/ccabanero/90c6e2aadfd4efa6b059333edeb2b314) 

[Testing Model Class methods](https://gist.github.com/ccabanero/4221831a4c527c0453a8506628df34af)

[Asynchronous Integration Test When Model performs work over the Network](https://gist.github.com/ccabanero/24a46c777bb29da95ba5)

[Model adopts the MKAnnotation protocol](https://gist.github.com/ccabanero/f6f8aeb7ea06073753bf)

[Model can Process the Response From Async Network Request](https://gist.github.com/ccabanero/1160dc6d95182593d111)

[Confirming Model object instantiation of a NSManagedObject subclass](https://gist.github.com/ccabanero/93501b0cc78e2023f119)

[Confirming that a NSManagedObject subclass Category properly seeds CoreData](https://gist.github.com/ccabanero/3de1a0cfecc7cb4fa9e6)

### Set Up for Testing ViewController

* When unit testing ViewController classes in storyboards, make sure to explicitly declare a 'Storyboard ID' property in the Identity Inspector for that ViewController.

* With Xcode 7, avoid adding classes to the Unit Testing target (or changing the access control level of classes for the sake of unit testing).  Instead use the __@testable__ attribute before declaring your test case class (see below).

````
    import XCTest
    @testable import YourAppTargetName

    class UnitTestsTests: XCTestCase {

        var viewControllerUnderTest: UIViewController!

        override func setUp() {
            super.setUp()

            let storyboard = UIStoryboard(name: "Main", bundle: nil)
            self.viewControllerUnderTest = storyboard.instantiateViewController(withIdentifier: "ViewController")

            self.viewControllerUnderTest.loadView()
            self.viewControllerUnderTest.viewDidLoad()
        }

        override func tearDown() {
            // Put teardown code here. This method is called after the invocation of each test method in the class.
            super.tearDown()
        }

        func testStuff() {
           XCTAssertEqual(1, 1)
        }
    }
```` 

### Add a Test Case file

Below are steps for adding a Test Case file for an individual class that you are testing.

* Right-click your Tests folder in the Xcode Project Navigator
* Choose New File
* Choose Cocoa Touch Class
* Use a naming convention - such as appending Test to your class name.  For example, use MapViewControllerTest for testing MapViewController.
* Choose the Subclass of __XCTestCase__
* Confirm the Test target is selected
* Choose Create

### Connect

* Twitter: [@clintcabanero](http://twitter.com/clintcabanero)
* GitHub: [ccabanero](http:///github.com/ccabanero)


    
