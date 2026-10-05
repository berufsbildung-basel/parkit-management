
# This document contains problems, issues and feedback identified during the project.


## Users park in the wrong spot

**Problem**
- Users may reserve a specific parking spot but park in a different spot due to unclear or insufficient information about the assigned location. 
- This can result in users occupying spots reserved by others and creates conflicts between reservations.


**Proposed solution**
- Install an LED matrix to display the current status of each parking spot and clearly indicate which spots are available, occupied, or reserved. 
- This should make it easier for users to identify their assigned spot and reduce incorrect parking.

**Related work**
- Detailed information about the LED integration can be found in `workstream/led-integration`.


**Status** - In progress

---

## Vehicles remain in parking spots after reservation expiration

**Problem**
- Users may remain in a parking spot after their reservation has expired.
- This can prevent the next user from using a spot that has already been reserved and create conflicts between consecutive reservations.


**Proposed solution**
- Send an automatic reminder notification before the reservation expires (e.g. 30, 15, or 10 minutes in advance). 
- The notification should remind the user that their reservation is about to expire and that the parking spot should be vacated.

**Related work**
- Detailed information about the LED integration can be found in `workstream/reservation-reminder`.

**Status** - Planned

---

## Rebooking / extending on the same day 

**Problem**
- It is not possible to rebook for the same day, even when the slot is still available.
- It is also not possible to extend the current booking.

**To discuss**
- Allow same-day rebooking if the slot is still available.
- Allow users to extend an active booking if there is no conflicting booking.

**Status**
Open — to be discussed

---

## Cancelation a spot reservation

**Problem**
- Users currently cannot cancel a spot reservation once it has been created. 


**To discuss**
- Allow users to cancel an active reservation.
- Define any restrictions or cancellation deadline.

**Status**
Open — to be discussed

---

## No overview of parking spot locations

**Problem**
There is no clear overview showing where each parking spot is located and which spots are corner or otherwise constrained by their position.

Users cannot easily determine the exact location and characteristics of a reserved spot before parking, which can be especially problematic for larger vehicles.

**To discuss**
- A map or overview showing the location of each parking spot.
- Information about relevant characteristics, such as corner locations or limited space.

**Status**
Open — to be discussed