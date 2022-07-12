# Read Class 39: Location

## Get Last Known Location

Acquried via the Google Play Services "Location API".

Last Known Location is assumed to be equivalent to Current Location.

Fused Location Provider: Actual component that retrieves location data. Manages underlying location technology. Provdies simple API to specify high accuracy while using minimal power.

Utilize `getLastLocation()` to acquire location information from Fused Location Provider.

## Overview of Steps

1. App Dev project must include Google Play Services. Download this via SDK Manager and add the Library to the Project.
1. Apps using location must "request location permissions" from Android.
1. Create Location Services Client within the onCreate() method `fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);`
1. Getting last known location of the device via `getLastLocation()` method which returns a Task.
1. Use Task to reference lattitude and longitude via the Location object (which could be null if: Off; Never recorded location to begin with; Fused Location Provider hasn't requested location since last restart).
1. Select a location estimate using the FusedLocationProviderClient i.e.: `getLastLocation()` which minimizes battery usage, or `getCurrentLocation()` which causes active processing of location determination, utilizing more battery power.

*Avoid* using `requestLocationUpdates()` as it is a power-hungry process and could linger in memory if not closed properly, further draining battery power.

## Code Samples

As they existed at developer.android.com when accessed...

Adding to the onCreate() method:

```java
private FusedLocationProviderClient fusedLocationClient;

// ..

@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...

    fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
}
```

Acquiring Last Known Location:

```java
fusedLocationClient.getLastLocation()
        .addOnSuccessListener(this, new OnSuccessListener<Location>() {
            @Override
            public void onSuccess(Location location) {
                // Got last known location. In some rare situations this can be null.
                if (location != null) {
                    // Logic to handle location object
                }
            }
        });
```

## Additional Development Resources

When building location-aware Apps:

- [Request proper permissions to allow your App access to Location Services](https://developer.android.com/training/location/permissions)
- [Use Fused Location provider to get up-to-date location information including last-known location](https://developer.android.com/training/location/receive-location-updates)
- [Use appropriate methods that conserve battery power while using location services](https://developer.android.com/guide/topics/location/battery)
- [Enable using a Map within your App](https://developer.android.com/training/maps)
- Sample Code [Location Updates Foreground Service](https://github.com/android/location-samples/blob/432d3b72b8c058f220416958b444274ddd186abd/LocationUpdatesForegroundService)
- Sample Code [Location Updates Pending Intent](https://github.com/android/location-samples/tree/432d3b72b8c058f220416958b444274ddd186abd/LocationUpdatesPendingIntent)

## Internet Resources

Get Last Known Location from [Developer Android Docs](https://developer.android.com/training/location/retrieve-current)

## Footer

Return to [Root Readme](../README.html)
