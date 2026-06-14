# Google Maps Platform GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Google Maps Platform APIs, covering Maps, Routes, Places, Geocoding, Elevation, Geolocation, Address Validation, Roads, Time Zone, Street View, and Aerial View capabilities.

Google Maps Platform does not natively expose a GraphQL endpoint. This schema is a conceptual representation that maps the REST API surface to GraphQL types, enabling developers to reason about the data model and evaluate GraphQL gateway or federation patterns on top of the underlying REST APIs.

## Source APIs

- **Geocoding API** — `https://maps.googleapis.com/maps/api/geocode`
- **Places API (New)** — `https://places.googleapis.com/v1`
- **Routes API** — `https://routes.googleapis.com`
- **Directions API** — `https://maps.googleapis.com/maps/api/directions`
- **Distance Matrix API** — `https://maps.googleapis.com/maps/api/distancematrix`
- **Elevation API** — `https://maps.googleapis.com/maps/api/elevation`
- **Geolocation API** — `https://www.googleapis.com/geolocation/v1`
- **Roads API** — `https://roads.googleapis.com/v1`
- **Time Zone API** — `https://maps.googleapis.com/maps/api/timezone`
- **Address Validation API** — `https://addressvalidation.googleapis.com/v1`
- **Street View Static API** — `https://maps.googleapis.com/maps/api/streetview`
- **Maps Static API** — `https://maps.googleapis.com/maps/api/staticmap`
- **Aerial View API** — `https://aerialview.googleapis.com`

## Schema File

The GraphQL schema is defined in [`google-maps-schema.graphql`](google-maps-schema.graphql).

## Type Summary

| Category | Types |
|---|---|
| Core Geography | `LatLng`, `Location`, `Bounds`, `Viewport` |
| Geocoding | `Geocode`, `GeocodeResult`, `AddressComponent`, `PlusCode` |
| Places | `Place`, `PlacePhoto`, `PlaceReview`, `PlaceOpeningHours`, `PlacePeriod`, `PlaceSpecialDay`, `PlacePlusCode`, `PlaceAccessibility`, `PlaceAmenity` |
| Place Search | `PlacesNearby`, `PlaceSearch`, `PlaceTextSearch`, `PlaceSearchPagination` |
| Autocomplete | `PlaceAutocompletion`, `Prediction`, `StructuredFormatting`, `PlaceDetails` |
| Routing | `Directions`, `Route`, `Leg`, `Step`, `Waypoint`, `Duration`, `Distance` |
| Distance Matrix | `DistanceMatrix`, `DistanceMatrixRow`, `DistanceMatrixElement` |
| Elevation | `Elevation`, `ElevationResult` |
| Geolocation | `GeolocationRequest`, `GeolocationResult`, `CellTower`, `WifiAccessPoint` |
| Roads | `RoadsSnapToRoad`, `SnapPoint` |
| Time Zone | `TimeZone` |
| Address Validation | `AddressValidation`, `AddressValidationResult`, `ValidationGranularity`, `ComponentName`, `UspsData` |
| Static Maps | `StaticMapRequest`, `StaticMapMarker`, `StaticMapPath` |
| Street View | `StreetViewMetadata`, `StreetViewPanorama` |
| Aerial View | `AerialView`, `VideoMetadata` |
| Map Objects | `Map`, `MapId`, `Marker`, `Polyline`, `Polygon`, `InfoWindow`, `AdvancedMarker` |

## Query Capabilities

The schema defines the following root query fields:

- `geocode(address, bounds, language, region, components)` — Forward geocode an address to coordinates
- `reverseGeocode(latlng, language, resultType, locationType)` — Reverse geocode coordinates to address
- `place(placeId, fields, language, region)` — Retrieve details for a specific place
- `searchPlacesNearby(location, radius, keyword, type, language)` — Search for places near a location
- `searchPlacesByText(query, location, radius, language, region)` — Text-based place search
- `autocomplete(input, location, radius, language, components)` — Autocomplete predictions for user input
- `directions(origin, destination, mode, waypoints, language)` — Get directions between two points
- `distanceMatrix(origins, destinations, mode, language, units)` — Compute distance and duration for origin/destination pairs
- `elevation(locations)` — Get elevation data for specific locations
- `elevationAlongPath(path, samples)` — Sample elevation along a path
- `geolocate(homeMobileCountryCode, homeMobileNetworkCode, radioType, carrier, cellTowers, wifiAccessPoints)` — Determine location from network signals
- `snapToRoads(path, interpolate)` — Snap GPS coordinates to roads
- `nearestRoads(points)` — Find nearest road segments to given points
- `timeZone(location, timestamp, language)` — Get time zone information for a location
- `validateAddress(address, previousResponseId, enableUspsCass)` — Validate and standardize an address
- `streetViewMetadata(location, pano, size, heading, fov, pitch)` — Get metadata about a Street View panorama
- `aerialView(address)` — Get aerial view video metadata for an address

## Authentication

All Google Maps Platform APIs require an API key passed as the `key` query parameter in the underlying REST calls. In a GraphQL gateway implementation, the key would typically be injected via an HTTP header (e.g., `X-Goog-Api-Key`) or server-side environment configuration.

## Reference

- GitHub: https://github.com/googlemaps
- Documentation: https://developers.google.com/maps/documentation
- Pricing: https://mapsplatform.google.com/pricing
- Status: https://status.cloud.google.com
