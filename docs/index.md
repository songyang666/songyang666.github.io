# 
<div class="image-container">
  <img src="resources/images/img.png" alt="Image 0">
  <figcaption>Discover ideas, insights, and inspiration in every corner of this space.</figcaption>
</div>
<div class="image-container">
  <img src="resources/images/img_1.png" alt="Image 1">
  <figcaption>Step into a world of creativity, learning, and endless possibilities.</figcaption>
</div>
<div class="image-container">
  <img src="resources/images/img_2.png" alt="Image 2">
  <figcaption>Your next great idea might be just a scroll away. Start exploring!</figcaption>
</div>
<div class="image-container">
  <img src="resources/images/img_3.png" alt="Image 3">
  <figcaption>Explore stories, knowledge, and adventures crafted just for you.</figcaption>
</div>

<div class="image-container">
  <img src="resources/images/img_4.png" alt="Image 4">
  <figcaption>Where passion meets purpose. Dive into the journey!</figcaption>
</div>

<div class="image-container">
  <img src="resources/images/img_5.png" alt="Image 5">
  <figcaption>Thanks for stopping by! Let's make this visit worth your while.</figcaption>
</div>

<div class="image-container">
  <img src="resources/images/img_6.png" alt="Image 6">
  <figcaption>Join me as we uncover insights, spark ideas, and ignite inspiration.</figcaption>
</div>


<style>
.image-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.image-container img {
position: absolute;
top: 0;
left: 0;
width: 100%;
height: auto;
object-fit: cover;
transform: translateY(100%);
transition: transform 0.3s ease-in-out;
}

.image-container figcaption {
position: absolute;
bottom: 20px;
left: 20px;
color: white;
font-size: 1.2rem;
text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.image-container.active {
opacity: 1;
}

.image-container.active img {
transform: translateY(0);
}
</style>

<script>
const imageContainers = document.querySelectorAll('.image-container');
let currentIndex = 0;

function showImage() {
  const currentContainer = imageContainers[currentIndex];
  currentContainer.classList.add('active');

  setTimeout(() => {
    currentContainer.classList.remove('active');
    currentIndex = (currentIndex + 1) % imageContainers.length;
    showImage();
  }, 3000);
}

showImage();
</script>