# MWAD_EX05_image-carousel-in-react
## Date: 7.10.2025

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

### gallery.jsx
```
import React, { useState, useEffect } from "react";
import "./gallery.css";

function ImageCarousel({ images, autoRotate = true, interval = 3000 }) {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex - 1 + images.length) % images.length);
  };

  useEffect(() => {
    if (!autoRotate) return;
    const slideInterval = setInterval(nextImage, interval);
    return () => clearInterval(slideInterval);
  }, [currentIndex, autoRotate, interval]);

  return (
    <div className="carousel-container">
  <img src={images[currentIndex]} alt={`Slide ${currentIndex}`} />
  <button className="prev" onClick={prevImage}>Prev</button>
  <button className="next" onClick={nextImage}>Next</button>
</div>
  );
}


export default ImageCarousel;
```

### gallery.css
```
.carousel-container {
  position: relative;
  width: 700px;        /* Medium size width */
  height: 600px;       /* Medium size height */
  margin: 100px auto;   /* Center horizontally */
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
}

.carousel-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.carousel-container button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.982);
  color: rgb(5, 4, 4);
  border: none;
  padding: 10px 14px;
  cursor: pointer;
  border-radius: 50%;
  font-size: 14px;
  transition: background-color 0.3s ease;
}

.carousel-container button:hover {
  background-color: rgba(111, 111, 111, 0.8);
}

.carousel-container .prev {
  left: 10px;
}

.carousel-container .next {
  right: 10px;
}

```
### App.jsx
```
import ImageCarousel from "./gallery";
import photo1 from "./assets/c1.jpeg";
import photo2 from "./assets/c2.jpg";
import photo3 from "./assets/c3.jpg";
import photo4 from "./assets/c4.jpg";
import photo5 from "./assets/c5.jpeg";
function App()
{
  const imageList = [photo1, photo2, photo3, photo4, photo5];
  return (
    <div>
      
      <ImageCarousel images={imageList}/>
    </div>
  );
}
export default App;
```

## OUTPUT
![Uploading image.png…]()


## RESULT
The program for creating Image Carousel using React is executed successfully.
