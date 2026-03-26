# Ex05 Image Carousel
## Date:25-03-2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
```
import React, { useState, useEffect } from 'react';

import img1 from './assets/anime.jpg';
import img2 from './assets/name.jpg';
import img3 from './assets/luffy.png';

const images = [img1, img2, img3];

function App() {
  const [currentIndex, setCurrentIndex] = useState(0);
  const [fade, setFade] = useState(true);

  const nextImage = () => {
    setFade(false);
    setTimeout(() => {
      setCurrentIndex((prev) => (prev + 1) % images.length);
      setFade(true);
    }, 200);
  };

  const prevImage = () => {
    setFade(false);
    setTimeout(() => {
      setCurrentIndex((prev) => (prev - 1 + images.length) % images.length);
      setFade(true);
    }, 200);
  };

  useEffect(() => {
    const intervalId = setInterval(() => {
      nextImage();
    }, 4000);
    return () => clearInterval(intervalId);
  }, [currentIndex]);

  return (
    <div
      style={{
        textAlign: 'center',
        maxWidth: 700,
        margin: '50px auto',
        backgroundColor: '#121212',
        padding: '20px',
        borderRadius: '15px',
        boxShadow: '0 4px 20px rgba(0,0,0,0.3)',
        color: 'white',
      }}
    >
      <h2 style={{ marginBottom: 20, fontFamily: 'Poppins, sans-serif' }}>
        React Image Carousel
      </h2>

      <div
        style={{
          alignContent: 'center',
          position: 'relative',
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
        }}
      >
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex}`}
          style={{
            width: '100%',
            height: 'auto',
            borderRadius: 12,
            transition: 'opacity 0.8s ease',
            opacity: fade ? 1 : 0,
            boxShadow: '0 4px 12px rgba(0,0,0,0.4)',
            display: 'block',
          }}
        />

        {/* Prev Button */}
        <button
          onClick={prevImage}
          style={buttonStyle('left')}
          aria-label="Previous Image"
        >
          ❮
        </button>

        {/* Next Button */}
        <button
          onClick={nextImage}
          style={buttonStyle('right')}
          aria-label="Next Image"
        >
          ❯
        </button>

        {/* Dots Navigation */}
        <div style={dotContainer}>
          {images.map((_, index) => (
            <span
              key={index}
              onClick={() => setCurrentIndex(index)}
              style={{
                ...dotStyle,
                backgroundColor: index === currentIndex ? 'white' : '#555',
                transform: index === currentIndex ? 'scale(1.3)' : 'scale(1)',
              }}
            ></span>
          ))}
        </div>
      </div>

      <p style={{ marginTop: 15 }}>
        Image <b>{currentIndex + 1}</b> of <b>{images.length}</b>
      </p>
    </div>
  );
}

// --- Styles ---

const buttonStyle = (side) => ({
  position: 'absolute',
  top: '50%',
  [side]: 15,
  transform: 'translateY(-50%)',
  fontSize: '2rem',
  backgroundColor: 'rgba(255,255,255,0.2)',
  color: 'white',
  border: 'none',
  borderRadius: '50%',
  cursor: 'pointer',
  padding: '0.3rem 0.8rem',
  transition: 'background-color 0.3s ease',
});

const dotContainer = {
  position: 'absolute',
  bottom: 12,
  width: '100%',
  textAlign: 'center',
};

const dotStyle = {
  height: 12,
  width: 12,
  margin: '0 4px',
  display: 'inline-block',
  borderRadius: '50%',
  cursor: 'pointer',
  transition: 'all 0.3s ease',
};

export default App;
```


## OUTPUT

<img width="947" height="760" alt="Screenshot 2025-11-05 153028" src="https://github.com/user-attachments/assets/80ef4805-b4c3-494e-894d-4273946a8a0a" />

<img width="1033" height="836" alt="Screenshot 2025-11-05 153013" src="https://github.com/user-attachments/assets/231d0664-d55a-417c-ab52-ce1e96409991" />

<img width="975" height="823" alt="Screenshot 2025-11-05 152948" src="https://github.com/user-attachments/assets/40244456-dca3-4990-8f77-16f24b5655ce" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
