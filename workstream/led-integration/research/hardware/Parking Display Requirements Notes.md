
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


## . LED Matrix Specifications

### 1.1 Matrix Dimensions

- **Matrix resolution:** 128 × 64 pixels (width × height)
    
- **Edge margin:** 1 pixel on each side
    
- **Usable area:** 126 × 62 pixels
    
- **Background:** Black
    

### 1.2 Character Dimensions

|Character size|Width|Height|
|---|---|---|
|Minimum|1 px|5 px|
|Maximum|5 px|5 px|

### 1.3 Character Scaling

Each character can be enlarged using different scaling factors.

| Scale | Minimum size | Maximum size |
| ----- | ------------ | ------------ |
| 1 × 1 | 1 × 5 px     | 5 × 5 px     |
| 2 × 2 | 2 × 10 px    | 10 × 10 px   |
| 3 × 3 | 3 × 15 px    | 15 × 15 px   |
| 4 × 4 | 4 × 20 px    | 20 × 20 px   |


**Note:** Larger scaling improves readability but reduces the number of characters that can be displayed.

### 1.4 Maximum Character Capacity

**Matrix resolution:** 128 × 64 pixels

At a scale of **2 × 2**:

- Maximum character size: 10 × 10 pixels
    
- Maximum of **12 characters per row**
    
- Maximum of **72 characters across 6 rows**


These values assume a fixed character cell size of 10 × 10 pixels without additional spacing between characters and a 1-pixel edge margin.

The actual capacity depends on character width, spacing and layout. The Adobe logo also reduces the available display area.

### 1.5 Advantages of the 128 × 64 Matrix

- More space for longer international licence plates.
    
- Larger text can be used without losing important information.
    
- Parking number, licence plate and reservation status can be displayed simultaneously.
    
- Additional space for the Adobe logo.
    

---

## 2. Adobe Logo

### 2.1 Appearance

- **Text:** `adobe`
    
- **Colour:** Red (`#FF0000`)
    
- **Font scale:** 2 × 2
    
- **Position:** Bottom-right corner of the LED matrix
    
- **Background:** Black
    

### 2.2 Logo Placement

- The Adobe text should remain visible without interfering with the parking information.
    
- The logo should use as little space as possible.
    
- The same logo position should be used on every display.
    
- A minimum margin of 1 pixel should be maintained.
    

---

## 4. Font Preview

![[Pasted image 20261019092254.png]]

---

## 5. Open Questions

- What is the minimum readable font size from the expected viewing distance?
    
- Should the licence plate and reservation time be displayed simultaneously?
    
- How much space should be reserved for the Adobe logo?
    
- Should the country code be displayed for international licence plates?
    

---

## 6. Prototype

### 6.1 Prototype Examples

**Example 1 – Reserved Parking Space**

```text
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│              BS 123456                 │
│                                        │
│              RESERVED                  │
│                                  adobe │
└────────────────────────────────────────┘
```

**Example 2 – Available Parking Space**

```text
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│                 FREE                   │
│              UNTIL 12:00               │
│                                        │
│                                  adobe │
└────────────────────────────────────────┘
```

**Example 3 – International Licence Plate**

```text
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│              B AB 1234                 │
│                                        │
│              RESERVED                  │
│                                  adobe │
└────────────────────────────────────────┘
```

**Example 4 – Full-Day Reservation**

```text
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│              BS 123456                 │
│                                        │
│               ALL DAY                  │
│                                  adobe │
└────────────────────────────────────────┘
```

**Example 5 – Connection Error**

```text
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│               NO DATA                  │
│                                        │
│           CONNECTION ERROR             │
│                                  adobe │
└────────────────────────────────────────┘
```

## 7. Parkit Integration

### 7.1 Display Updates

The display must automatically update when:

- A new reservation is created.
    
- An existing reservation is modified.
    
- A reservation is cancelled.
    
- A different parking space is assigned.
    
- A reservation starts or ends.
    

## 8. Reservation Handling

### 8.1 Reservation Periods

The system must support the reservation periods defined in Parkit.

| Reservation type | Example time | Display     |
| ---------------- | ------------ | ----------- |
| Morning          | 08:00–12:00  | `BS 123456` |
| Afternoon        | 12:00–18:00  | `BS 123456` |
| Full Day         | 08:00–18:00  | `BS 123456` |

Note: These times are examples. The actual reservation periods must be retrieved from Parkit.

### 8.2 Parking Availability

The LED display should automatically change its content depending on the current reservation status.

|Situation|Display|
|---|---|
|Parking space is reserved|`BS 123456`|
|Available until 12:00|`FREE UNTIL 12:00`|
|Available for the entire day|`FREE ALL DAY`|
|Reservation starts|Display licence plate|
|Reservation ends|Display next reservation or `FREE`|

### 8.3 Automatic Switching

- The system compares the current time with the reservation start and end times.
    
- When a reservation ends, the display automatically changes to the next status.
    
- If another reservation starts immediately, the new licence plate is displayed.
    
- No manual interaction should be required.


## 9. Licence Plate Handling

### 9.1 Supported Formats

The system must support Swiss and international licence plates.

|Country|Example|
|---|---|
|Switzerland|`BS 123456`|
|Germany|`B AB 1234`|
|France|`AB-123-CD`|
|Italy|`AB 123 CD`|
|Austria|`W 12345 A`|

### 9.2 Dynamic Font Scaling

- The system should automatically adjust the font size depending on the licence plate length.
    
- Short licence plates can be displayed using a larger scaling factor.
    
- Longer licence plates should use a smaller scaling factor.
    
- The licence plate must remain readable and fit within the 128 × 64 matrix.
    

### 9.3 Consistent Formatting

- Use uppercase letters.
    
- Use the same pixel font for all licence plates.
    
- Keep consistent spacing between characters.
    
- Centre the licence plate horizontally.
    
- Preserve important characters such as hyphens.
    

## 10. Privacy and Data Protection

### 10.1 Licence Plate Privacy

- Licence plates should only be displayed when necessary.
    
- The display should not show the driver's name or other personal information.
    
- Licence plate information should be removed when the reservation ends.
    
- Displaying partially hidden licence plates should be considered if full visibility is not required.
    

### 10.2 Data Security

- Communication between Parkit and the LED displays should be secured.
    
- Only authorized systems should be able to change display information.
    
- Reservation data should not be stored permanently on the LED matrix controller unless required.

