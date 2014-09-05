[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns)

#### Description
Example unit tests for a ViewController class that is composed of a MKMapView and adopts the MKMapViewDelegate protocol.

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
	
	- (void)testControllerIsComposedOfMapView {
	    
	    XCTAssertNotNil(self.viewControllerUnderTest.mapView, @"Controller is not composed of MapView");
	}
	
	- (void)testControllerImplementsMKMapViewDelegateMethods {
	    
	    XCTAssertTrue([self.viewControllerUnderTest respondsToSelector:@selector(mapView:viewForAnnotation:)], @"Controller does not conform to MapView:viewForAnnotation");
	}
	
	- (void)testControllerConformsToMKMapViewDelegate {
	    
	    XCTAssertTrue([self.viewControllerUnderTest conformsToProtocol:@protocol(MKMapViewDelegate)], @"Controller does not conform to MKMapViewDelegate protocol");
	}
	
	- (void)testMapIsShowingCustomTileOverlay {
	    
	    //get the url template for the tile overlay
	    NSString *urlTemplate = @"ENTER-URL-TEMPLATE";
	    
	    
	    //find a tile overlay with the same url template
	    NSArray *mapOverlays = self.viewControllerUnderTest.mapView.overlays;
	    
	    BOOL tileOverlayIsAddedToMap = NO;
	    
	    for(id currentOverlay in mapOverlays) {
	        
	        if([currentOverlay isKindOfClass:[MKTileOverlay class]]) {
	            
	            MKTileOverlay *currentTileOverlay = (MKTileOverlay *)currentOverlay;
	            
	            NSString *currentUrlTemplate = currentTileOverlay.URLTemplate;
	            
	            if([currentUrlTemplate isEqualToString:urlTemplate]) {
	                
	                tileOverlayIsAddedToMap = YES;
	                
	                break;
	            }
	        }
	    }
	    
	    XCTAssertTrue(tileOverlayIsAddedToMap, @"The map does not show the tile overlay.");
	}
	
	//------------------------------------------------
	//  FEATURE - User can toggle location on and off
	//------------------------------------------------
	- (void)testViewControllerHasLocationButton {
	    
	    XCTAssertNotNil(self.viewControllerUnderTest.locationButton, @"ViewController under test is not composed of a Location Button");
	}
	
	- (void)testLocationButtonTriggersActionMethod {
	    
	    XCTAssertTrue([self.viewControllerUnderTest.locationButton actionsForTarget:self.viewControllerUnderTest forControlEvent:UIControlEventTouchUpInside], @"Location button does not trigger action method");
	}
	
	@end