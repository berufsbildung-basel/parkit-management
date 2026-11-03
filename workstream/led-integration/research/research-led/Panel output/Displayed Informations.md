
1. **Parking information**
    - The system must display the parking space assigned to the driver's reservation.
    - The displayed information must match the current reservation data in Parkit.
    - The displayed information must be updated when the reservation or assigned parking space changes.
    - The parking space must be clearly identifiable by the driver.
2. **Reservation periods**
    - The system must support the reservation periods used by Parkit, including morning, afternoon, and full-day reservations.
    - The system must correctly show when a parking space becomes available again.
    - Availability information such as FREE UNTIL 12:00 should be supported where needed.
3. **Licence plates**
    - The system must support the licence plate formats required by the project.
    - Different licence plate lengths and supported characters must be handled.
    - A consistent format for displaying licence plates must be defined.

• • Privacy must be considered when licence plate information is displayed


# LED Parking Display – Technical Notes

## 1. LED Matrix Specifications

### 1.1 Matrix Dimensions

|Property|Value|
|---|---|
|Resolution|128 × 64 pixels|
|Edge margin|1 pixel per side|
|Usable area|126 × 62 pixels|
|Background|Black|

### 1.2 Character Capacity

**Scale: 2 × 2**

- Maximum character size: 10 × 10 pixels
    
- Maximum characters per row: **12**
    
- Maximum rows: **6**
    
- Total capacity: **72 characters**
    

_Note: The calculation does not include additional character spacing or space reserved for the Adobe logo._

### 1.3 Adobe Logo

| Property    | Value               |
| ----------- | ------------------- |
| Text        | `adobe`             |
| Colour      | Red (`#FF0000`)     |
| Font scale  | 2 × 2               |
| Position    | Bottom-right corner |
| Edge margin | 1 pixel             |

---

## 2. Parkit Integration

### 2.1 Required Data

- Parking space number
    
- Licence plate
    
- Reservation start time
    
- Reservation end time
    
- Reservation status
    

### 2.2 Automatic Updates

The display updates when:

- New reservation is created
    
- Existing reservation is modified
    
- Reservation is cancelled
    
- Parking space assignment changes
    
- Reservation starts or ends
    

**Synchronization:** Automatic synchronization with Parkit.

### 2.3 Connection Errors

- Display `NO DATA` if current information is unavailable.
    
- Avoid displaying incorrect or outdated reservation information.
    

---

## 3. Reservation Handling

### 3.1 Reservation Periods

|Type|Example time|
|---|---|
|Morning|08:00–12:00|
|Afternoon|12:00–18:00|
|Full Day|08:00–18:00|

_Note: Times are examples. Actual reservation periods are defined in Parkit._

### 3.2 Display States

|Status|Display|
|---|---|
|Reserved|`BS 123456`|
|Free|`FREE`|
|Free until next reservation|`FREE UNTIL 12:00`|
|Free all day|`FREE ALL DAY`|

### 3.3 Automatic Switching

- Check current time.
    
- Compare reservation start and end times.
    
- Automatically update the licence plate.
    
- Display `FREE` when no reservation is active or scheduled to start immediately.
    

**Example – Consecutive Reservations**

|Time|Display|
|---|---|
|08:00–12:00|`BS 123456`|
|12:00–18:00|`B AB 1234`|
|After 18:00|`FREE`|

---

## 4. Licence Plate Handling

### 4.1 Supported Countries

| Country     | Example     |
| ----------- | ----------- |
| Switzerland | `BS 123456` |
| Germany     | `B AB 1234` |
| France      | `AB-123-CD` |
| Italy       | `AB 123 CD` |
| Austria     | `W 12345 A` |

### 4.2 Supported Characters

- Letters: `A–Z`
    
- Numbers: `0–9`
    
- Spaces
    
- Hyphens (`-`)
    
- Additional special characters if required
    

### 4.3 Dynamic Font Scaling

- Short licence plate → Larger font
    
- Long licence plate → Smaller font
    
- Automatic adjustment to available width
    
- Text must fit within the 128 × 64 matrix
    

### 4.4 Display Formatting

- Uppercase letters
    
- Consistent pixel font
    
- Consistent character spacing
    
- Horizontally centred licence plate
    
- Preserve important separators
    

---

## 5. Privacy

### 5.1 Licence Plate Display

- Display only during the reservation period.
    
- Remove licence plate after reservation ends.
    
- Do not display driver names.
    
- Optionally hide part of the licence plate.
    

**Example:** `BS ***456`

---

## 6. Prototype

### 6.1 Display Configuration

|Property|Value|
|---|---|
|Matrix|128 × 64 pixels|
|Background|Black|
|Font|Pixel font|
|Adobe logo|Red, bottom-right|

### 6.2 Display Examples

---

## 7. Testing

### 7.1 Font and Readability

- Test different font scales
    
- Verify maximum character capacity
    
- Check readability from inside a vehicle
    

### 7.2 Licence Plates

- Swiss licence plates
    
- International licence plates
    
- Long licence plates
    
- Special characters
    

### 7.3 Parkit Integration

- New reservation
    
- Reservation cancellation
    
- Parking space reassignment
    
- Automatic reservation switching
    
- Connection failure
    

### 7.4 Display

- Adobe logo positioning
    
- Edge margins
    
- Brightness
    
- Contrast
    
- Text overlapping
    

---

## 8. Open Questions

### Display

- Minimum readable font size?
    
- Display licence plate and reservation time simultaneously?
    
- Final Adobe logo size?
    
- Display country codes for international licence plates?
    

### Technical

- Is a Parkit API available?
    
- Wi-Fi or LAN connection?
    

### Privacy

- Display complete or partially hidden licence plates?

![[Pasted image 20261019092254.png]]
