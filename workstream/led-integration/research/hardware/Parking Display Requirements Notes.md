
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

|Scale|Minimum size|Maximum size|
|---|---|---|
|1 × 1|1 × 5 px|5 × 5 px|
|2 × 2|2 × 10 px|10 × 10 px|
|3 × 3|3 × 15 px|15 × 15 px|
|4 × 4|4 × 20 px|20 × 20 px|

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

## 3. Additional Considerations

- **Readability:** Text must be readable from inside a vehicle.
    
- **International plates:** Longer licence plates may require smaller characters.
    
- **Automatic updates:** Display content must stay synchronized with Parkit.
    
- **Space limitations:** Important information such as the licence plate should have priority over decorative elements.
    
- **Connection failure:** The display should show a defined fallback message if current reservation data is unavailable.
    
- **Privacy:** Personal information should only be displayed when necessary.
    

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

### 6.4 Prototype Testing

The prototype should be tested for:

- Different character scaling factors (1 × 1 to 4 × 4).
    
- Swiss and international licence plate lengths.
    
- Readability at different viewing distances.
    
- Correct placement of the Adobe logo.
    
- Automatic switching between reservation states.
    
- Correct display of reservation times.
    

**Note:** These examples are conceptual layouts and do not represent the exact pixel positions of the final 128 × 64 LED matrix.


## 1. LED Matrix Specifications

### 1.1 Matrix Dimensions

- **Matrix resolution:** 64 × 64 pixels
    
- **Edge margin:** 1 × 1 pixel
    
- **Background:** Black
    

### 1.2 Character Dimensions

|Character size|Width|Height|
|---|---|---|
|Minimum|1 px|5 px|
|Maximum|5 px|5 px|

### 1.3 Character Scaling

Each character can be enlarged using different scaling factors.

|Scale|Minimum size|Maximum size|
|---|---|---|
|1 × 1|1 × 5 px|5 × 5 px|
|2 × 2|2 × 10 px|10 × 10 px|
|3 × 3|3 × 15 px|15 × 15 px|
|4 × 4|4 × 20 px|20 × 20 px|

**Note:** Larger scaling improves readability but reduces the number of characters that can be displayed. 

### 1.4 Maximum Character Capacity

**Matrix resolution:** 64 × 64 pixels

At a scale of **2 × 2**:

- Maximum character size: 10 × 10 pixels
    
- Maximum of **6 characters per row**
    
- Maximum of **24 characters across 4 rows**
    

These values assume a fixed character cell size of 10 × 10 pixels without additional spacing between characters.

The actual capacity depends on character width, spacing and layout. The Adobe logo also reduces the available display area.

---

## 2. Adobe Logo

### 2.1 Appearance

- **Text:** `adobe`
    
- **Colours:** Red 
    
- **Font scale:** 2 × 2
    
- **Position:** Bottom-right corner of the LED matrix
    
- **Background:** Black
    

### 2.2 Logo Placement

- The Adobe text should remain visible without interfering with the parking information.
    
- The logo should use as little space as possible.
    
- The same logo position should be used on every display.
    

---

## 3. Additional Considerations

- **Readability:** Text must be readable from inside a vehicle.
    
- **International plates:** Longer licence plates may require smaller characters.
    
- **Automatic updates:** Display content must stay synchronized with Parkit.
    
- **Space limitations:** Important information such as the licence plate should have priority over decorative elements.
    
- **Connection failure:** The display should show a defined fallback message if current reservation data is unavailable.
    
- **Privacy:** Personal information should only be displayed when necessary.
    

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

### 6.1 Prototype Specifications

- **Matrix resolution:** 64 × 64 pixels
    
- **Background:** Black
    
- **Font:** Pixel font
    
- **Adobe logo:** Red, bottom-right
    
- **Display content:** Parking space number, licence plate and reservation status
    

### 6.2 Display States

|State|Display information|
|---|---|
|Reserved|Parking number and licence plate|
|Free|`FREE`|
|Free until next reservation|`FREE UNTIL 12:00`|
|Full-day availability|`FREE ALL DAY`|
|Connection error|`NO DATA`|

### 6.3 Prototype Examples

**Example 1 – Reserved Parking Space**

```text
┌──────────────────────┐
│ P12                  │
│                      │
│      BS 123456       │
│                      │
│      RESERVED        │
│                adobe │
└──────────────────────┘
```

**Example 2 – Available Parking Space**

```text
┌──────────────────────┐
│ P12                  │
│                      │
│        FREE          │
│      UNTIL 12:00     │
│                      │
│                adobe │
└──────────────────────┘
```

**Example 3 – International Licence Plate**

```text
┌──────────────────────┐
│ P12                  │
│                      │
│      B AB 1234       │
│                      │
│      RESERVED        │
│                adobe │
└──────────────────────┘
```

