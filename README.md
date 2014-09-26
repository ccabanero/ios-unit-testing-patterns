iOS Unit Testing Patterns
=========================


#### Description
Examples of unit testing patterns for iOS projects.  

While it is usually straightforward to create unit tests for your Model classes, the mechanics of how to write unit tests that assert the behaviors and responsibilities of your Controller classes are usually less straightforward.  Being so, the list below provides more examples for ways to approach unit testing your UIViewController subclasses.

####Languages
Objective-C and Swift

####Unit Testing Framework
XCTest.framework

####Sample Unit Tests for Controller Classes

Description | Language
------------ | ------------- 
[ViewController (with xib) composed of UITableView](https://gist.github.com/ccabanero/bc0fe961ca060dc63803) | Objective-C
[ViewController (in Storyboard) composed of UITableView](Samples/UITableView-swift.md) | Swift
[ViewController (with xib) composed of MKMapView](Samples/MKMapView-objc.md) | Objective-C
[ViewController (in Storyboard) composed of MKMapView](Samples/MKMapView-swift.md) | Swift
[ViewController (with xib) composed of CLLocationManager](Samples/CLLocationManager-objc.md) | Objective-C
[ViewController (with xib) composed of UISegmentedControl](Samples/UISegmentedControl-objc.md) | Objective-C
[ViewController (with xib) composed of UIButton](Samples/UIButton-objc.md) | Objective-C
[ViewController (in Storyboard) composed of UIButton](Samples/UIButton-swift.md) | Swift
[ViewController (with xib) composed of UIPickerView](Samples/UIPickerView-objc.md) | Objective-C
[ViewController (with xib) composed of UILabel](Samples/UILabel-objc.md) | Objective-C
[ViewController (in Storyboard) composed of UILabel](Samples/UILabel-swift.md) | Swift

####Sample Unit Tests for Model Classes

Description | Language
------------ | ------------- 
[Model adopts the MKAnnotation protocol](Samples/MKAnnotation-objc.md) | Objective-C
[Model can Process Response From Network Request](Samples/NetworkRequests-objc.md)| Objective-C

####Contact
* Twitter: [@clintcabanero](http://twitter.com/clintcabanero)
* GitHub: [ccabanero](http:///github.com/ccabanero)


    
