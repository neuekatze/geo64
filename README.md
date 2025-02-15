
# Base64 Geohash Specification

## Introduction

Geo64 is an alternative geospatial encoding format based on the traditional Geohash, but it instaed uses Base64 instead of Base32. This makes it even more compact while maintaining precision and efficiency in encoding and decoding geographical coordinates.

## Encoding Process

### Defining Latitude and Longtitude Ranges

-   Latitude (`lat`) is within `[-90, 90]`.
-   Longitude (`lon`) is within `[-180, 180]`.

### Converting Coordinates into a Binary Representation

1.  Start with an empty bitstream.
2.  Alternately assign bits to longtitude (even-indexed bits) and latitude (odd-indexed bits).
3.  Each bit halves the current range of the respective coordinate:
    -   A `1` means the value is in the upper half.
    -   A `0` means the value is in the lower half.
4.  Continue until the desired precision is reached (typically 6 bits per character in the final encoding).

### Converting the Bitstream into Base64

1.  Group the bitstream into 6-bit segments.
2.  Convert each 6-bit segment into a Base64 character using the following character set:
    
    ```
    ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/
    ```
    
3.  The final result is a Base64-encoded string representing the location.

## Decoding Process

1.  Convert the Base64 string back into a bitstream.
2.  Assign bits alternately to longitude and latitude.
3.  Determine the coordinate range for each bit, refining it step by step.
4.  The midpoint of the final range for latitude and longitude is the decoded coordinate.

## Examples
`0d`
![0d](https://github.com/user-attachments/assets/9b0e04c7-44c8-4569-a5d1-a781ca5499ca)

`0BPI`
![0BPI](https://github.com/user-attachments/assets/570d23e5-bf08-4e8b-bfbf-5d939fd6a944)

`x2Nfw`
![x2Nfw](https://github.com/user-attachments/assets/cac1b7d1-08ad-4bf7-89c4-75782b91a013)

`x2NfwPMa`
![x2NfwPMa](https://github.com/user-attachments/assets/3f65913a-4eb1-497f-970d-32f52d7e4f4e)

The last one is so small it is very difficult to even notice where it is.

It is more compact than Geohash. Eight characters is when it starts to give absurdly small locations. 


## Implementation

A reference implementation in JavaScript is provided in the repository for encoding and decoding Base64 Geohashes. Other implementations can be easily derived from the specification above.
