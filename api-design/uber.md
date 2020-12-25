Uber API

Entities

Rides
rideId: string
driverId: string
riderIds: string[]
time: timestamp,
pickup_location: GeoLocation
dropoff_location: GeoLocation

GeoLocation
lat: float
long: float

User
userId: string
password_digest: string
email: string
current_location: GeoLocation

root url: api.uber.com/v1

CRUD

Create a Ride
POST /ride (riderId: string, location: GeoLocation)
=> Ride

Read a Ride
GET /ride/current {get the current ride driver/rider is in}
=> Ride
GET /ride/:id {get a ride by rideId}
=> Ride
GET /ride/user/:id {get all rides by a userId}
=> Ride[]

Update a Ride
PUT /ride (participantId: string, rideId: string, ... attributes to edit)
=> Ride

Cancel a Ride
DELETE /ride/:id/user/:id (rideId: string, participantId: string) // participantId can be either a driver or a rider
=> Ride
