[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns) | Model adopts the MKAnnotation protocol

#### Description
Example unit tests for Model class that adopts the MKAnnotation protocol.

#### Code Sample
	
	#import <XCTest/XCTest.h>
	#import "FerryTerminalAnno.h"
	#import <CoreLocation/CoreLocation.h>
	#import <MapKit/MapKit.h>
	
	@interface FerryTerminalAnnoTest : XCTestCase
	
	@property (nonatomic, strong) FerryTerminalAnno *annoUnderTest;
	
	@end
	
	
	@implementation FerryTerminalAnnoTest
	
	- (void)setUp
	{
	    [super setUp];
	    
	    
	    //fetch sample data from geojson
	    NSString *filePath = [[NSBundle mainBundle] pathForResource:@"layerferryterminals" ofType:@"geojson"];
	    
	    NSString *geoJSONString = [[NSString alloc] initWithContentsOfFile:filePath encoding:NSUTF8StringEncoding error:NULL];
	    
	    NSDictionary *geoJSON = [NSJSONSerialization JSONObjectWithData:[geoJSONString dataUsingEncoding:NSUTF8StringEncoding] options:NSJSONReadingAllowFragments error:nil];
	    
	    NSArray *geoJSONFeatures = [geoJSON objectForKey:@"features"];
	    
	    NSDictionary *geoJSONAsDict = [geoJSONFeatures objectAtIndex:0];
	    
	    
	    //instantiate model object using dictionary
	    self.annoUnderTest = [[FerryTerminalAnno alloc] initWithDictionary:geoJSONAsDict];
	}
	
	- (void)tearDown
	{
	    self.annoUnderTest = nil;
	    
	    [super tearDown];
	}
	
	- (void)testAnnotationModelClassCanBeInstantiatedWithDictionary {
	    
	    XCTAssertNotNil(self.annoUnderTest, @"Failed to instantiate annotation");
	    
	    XCTAssertNotNil(self.annoUnderTest.title, @"Required title property not initialized for annotation");
	    
	    XCTAssertNotNil(self.annoUnderTest.subtitle, @"Required subtitle property not initialized for annotation");
	    
	    XCTAssert(self.annoUnderTest.coordinate.latitude > 1, @"Latitude property for annotation not initialized correctly");
	    
	    XCTAssert(self.annoUnderTest.coordinate.longitude < 1, @"Longitude property for annotation not initialized correctly.");
	}
	
	- (void)testAnnotationConformsToMKAnnotationProtocol {
	    
	    XCTAssert([self.annoUnderTest conformsToProtocol:@protocol(MKAnnotation)], @"Annotation under test does not conform to the MKAnnotation protocol");
	}
	
	- (void)testAnnotationImplementsMKAnnotationProtocolProperties {
	    
	    XCTAssertNotNil(self.annoUnderTest.title, @"Annotation does not have required title property");
	    
	    XCTAssertNotNil(self.annoUnderTest.subtitle, @"Annotation does not have required subtitle property");
	    
	    XCTAssert(self.annoUnderTest.coordinate.latitude > 0, @"Annotation does not have optional coordinate property");
	    
	    XCTAssert(self.annoUnderTest.coordinate.longitude < 0, @"Annotation does not have optional coordinate property");
	}
	
	- (void)testAnnoCanBeAddedToMapViewAsMKAnnotation {
	    
	    MKMapView *mapView = [[MKMapView alloc] init];
	    
	    NSUInteger initialCountOfAnnotations = mapView.annotations.count;
	    
	    [mapView addAnnotation:self.annoUnderTest];
	    
	    NSUInteger countOfParkAnnotationsAfterAddedToMap = mapView.annotations.count;
	    
	    XCTAssertTrue(countOfParkAnnotationsAfterAddedToMap > initialCountOfAnnotations, @"Annotation under test cannot be added to a MKMapView");
	}
	
	//continue with application-specific tests ...
	
	@end
