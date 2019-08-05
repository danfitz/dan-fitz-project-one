# Single-page PSD Conversion

This project requires me to convert a PSD design into a responsive website. [This is the design](https://scene.zeplin.io/project/5d14daaa78189773b2f59efc
).

## Presentation Notes

### Challenge #1: Mobile-first

For this PSD conversion, I wanted to try something new and design the website **mobile-first**. This goal was a challenge for me because I had no clear methodology for approaching mobile-first. This is what I learnt...

Creating the mobile version was easy. It just involved setting my inspector to `320px` and adding each block one by one, one below the next.

The challenge of mobile-first, I found, came down to one constant question: **for each section, at what point is there enough space for me to float elements within that section onto the same line?**

**Answer**: the point at which they start to become *unreadable* when stretched the full width of the page.

`[move around width while viewing featured post image]`

### Challenge #2: Cropping Images via CSS

The second challenge I faced was that some images were cropped in the PSD when compared to the original image files.

The easy solution would have been to use `background`.

```css
div {
  background: url("images/image.jpg");
  background-size: cover;
  background-position: left top;
  width: 100%;
  height: 500px;
```

However, `background` is better for atmospheric images, and I felt like the images in the PSD had semantic value for assistive devices. I needed to find a way to crop using an `img` tag. Here's my solution:

```html
<div class="image-container">
  <img src="images/image.jpg" alt="I have semantic value">
</div>
```

Using the CSS below, I was able to turn `.image-container` into a window that displays a zoomed-in section of `img`.

```css
.image-container {
  overflow: hidden; /* 1. Hides content that moves outside container, creating a window */
}
.image-container img {
  width: 150%; /* 2. Makes image expand beyond .image-container */
  height: 500px;
  object-fit: cover; /* 3. Does the same thing as background-size: cover; */
  object-position: left top; /* 4. Does the same thing as background-position: left top; */
}
```
