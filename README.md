iOS Unit Testing Patterns
=========================


#### Description
Unit testing code snippets for various iOS development scenarios.

####Language
Swift

####Unit Testing Framework
XCTest.framework

####Sample Unit Tests for Controller Classes

Description | Language
------------ | ------------- 
[ViewController (in Storyboard) composed of UITableView](https://gist.github.com/ccabanero/39ee6d5fd7b289dee695) | Swift
[ViewController (in Storyboard) composed of UICollectionView](https://gist.github.com/ccabanero/6ef47c1aeb21acfb326d30f6b01825d1) | Swift
[ViewController (in Storyboard) implements Target-Action for a UIBarButtonItem](https://gist.github.com/ccabanero/4a1a4bfbf5fa3fbbb1070c8765c3de73) | Swift
[ViewController (in Storyboard) composed of UIButton](https://gist.github.com/ccabanero/b92197516342c0147688) | Swift
[ViewController (in Storyboard) composed of UILabel](https://gist.github.com/ccabanero/68cd8ff461316930f707) | Swift
[Testing Segue is called with mock UIViewController](https://gist.github.com/ccabanero/9f7ad6775eacec3cc997) | Swift
[Testing Segue passes data to Target ViewController](https://gist.github.com/ccabanero/308db4882b7ca4967ebb5d17530177f3) | Swift
[Testing a CustomView is properly initialized by ViewController](https://gist.github.com/ccabanero/ac7237e4591092130326) | Swift
[ViewController (in Storyboard) composed of MKMapView](https://gist.github.com/ccabanero/90c73c46ed1671298775) | Swift
[ViewController (with xib) composed of CLLocationManager](https://gist.github.com/ccabanero/dd35e7bee8205ad225f3de1391027aa5) | Swift
[ViewController (with xib) composed of UISegmentedControl](https://gist.github.com/ccabanero/e204496231a41759fa94) | Objective-C
[ViewController (with xib) composed of UIPickerView](https://gist.github.com/ccabanero/8d1dfa65218b8bb10ebf) | Objective-C
[ViewController (in Storyboard) composed of UIImagePickerController](https://gist.github.com/ccabanero/3c758af01944cc591fbb) | Objective-C
[Testing UIAlertController with mock UIViewController](https://gist.github.com/ccabanero/b88a77caba37f8dd9fbf) | Swift
[Testing UIRightBarButtonItem has correct custom UIImage](https://gist.github.com/ccabanero/ed9111e472f6cb283ff8c3e714712efa) | Swift
[Testing that APIClient requests data during ViewController/s viewDidLoad() event](https://gist.github.com/ccabanero/d3bc7c36b2b1381be97494404407ce26) | Swift


####Sample Unit Tests for Model Classes

Description | Language
------------ | ------------- 
[Testing Model Class Initialization](https://gist.github.com/ccabanero/90c6e2aadfd4efa6b059333edeb2b314) | Swift
[Testing Model Class methods](https://gist.github.com/ccabanero/4221831a4c527c0453a8506628df34af) | Siwft
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


    
