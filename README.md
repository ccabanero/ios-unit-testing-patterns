iOS Unit Testing Patterns
=========================


#### Description
Examples of unit testing patterns for iOS application development. 

####Languages
Swift and Objective-C

####Unit Testing Framework
XCTest.framework

####Sample Unit Tests for Controller Classes

Description | Language
------------ | ------------- 
[ViewController (with xib) composed of UITableView](https://gist.github.com/ccabanero/bc0fe961ca060dc63803) | Objective-C
[ViewController (in Storyboard) composed of UITableView](https://gist.github.com/ccabanero/39ee6d5fd7b289dee695) | Swift
[ViewController (with xib) composed of MKMapView](https://gist.github.com/ccabanero/ae7c3e5eff7602b06047) | Objective-C
[ViewController (in Storyboard) composed of MKMapView](https://gist.github.com/ccabanero/90c73c46ed1671298775) | Swift
[ViewController (with xib) composed of CLLocationManager](https://gist.github.com/ccabanero/cd6e068c9271a6c30bfc) | Objective-C
[ViewController (with xib) composed of UISegmentedControl](https://gist.github.com/ccabanero/e204496231a41759fa94) | Objective-C
[ViewController (with xib) composed of UIButton](https://gist.github.com/ccabanero/d9aee20b1d6fa3d8a001) | Objective-C
[ViewController (in Storyboard) composed of UIButton](https://gist.github.com/ccabanero/b92197516342c0147688) | Swift
[ViewController (with xib) composed of UIPickerView](https://gist.github.com/ccabanero/8d1dfa65218b8bb10ebf) | Objective-C
[ViewController (with xib) composed of UILabel](https://gist.github.com/ccabanero/e8f4ce9b7881d5d31939) | Objective-C
[ViewController (in Storyboard) composed of UILabel](https://gist.github.com/ccabanero/68cd8ff461316930f707) | Swift
[ViewController (in Storyboard) composed of UIImagePickerController](https://gist.github.com/ccabanero/3c758af01944cc591fbb) | Objective-C

####Sample Unit Tests for Model Classes

Description | Language
------------ | ------------- 
[Asynchronous Unit Test When Model performs work over the Network](https://gist.github.com/ccabanero/24a46c777bb29da95ba5) | Swift
[Model adopts the MKAnnotation protocol](https://gist.github.com/ccabanero/f6f8aeb7ea06073753bf) | Objective-C
[Model can Process the Response From Async Network Request](https://gist.github.com/ccabanero/1160dc6d95182593d111)| Objective-C
[Confirming Model object instantiation of a NSManagedObject subclass](https://gist.github.com/ccabanero/93501b0cc78e2023f119) | Objective-C
[Confirming that a NSManagedObject subclass Category properly seeds CoreData](https://gist.github.com/ccabanero/3de1a0cfecc7cb4fa9e6) | Objective-C

####Set Up

* When unit testing ViewController classes in storyboards, make sure to explicitly declare a 'Storyboard ID' property in the Identity Inspector for that ViewController.

* With Xcode 7, avoid adding classes to the Unit Testing target (or changing the access control level of classes for the sake of unit testing).  Instead use the __@testable__ attribute before declaring your test case class (see below).

````
    import XCTest
    @testable import YourAppTargetName

    class UnitTestsTests: XCTestCase {

        var viewControllerUnderTest: ViewController!

        override func setUp() {
            super.setUp()

            let storyboard = UIStoryboard(name: "Main", bundle: nil)
            self.viewControllerUnderTest = storyboard.instantiateViewControllerWithIdentifier("ViewController") as! ViewController

            self.viewControllerUnderTest.loadView()
            self.viewControllerUnderTest.viewDidLoad()
        }

        override func tearDown() {
            // Put teardown code here. This method is called after the invocation of each test method in the class.
            super.tearDown()
        }
```` 

####Connect
* Twitter: [@clintcabanero](http://twitter.com/clintcabanero)
* GitHub: [ccabanero](http:///github.com/ccabanero)


    
