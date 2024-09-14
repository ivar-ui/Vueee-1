<template>
  <div class="dashboard" :style="{ backgroundColor: currentBackgroundColor }">
    <header>
      <h1 class="title">Vue Punya Ipannn</h1>
    </header>

    <main class="horizontal-layout">
      <section class="card carousel">
        <h2>Gambar-gambar</h2>
        <div class="image-container">
          <transition-group name="fade">
            <img
              v-for="(image, index) in images"
              :key="image"
              :src="image"
              v-show="index === currentImageIndex"
              alt="Carousel Image"
              class="carousel-image"
            />
          </transition-group>
        </div>
        <div class="carousel-controls">
          <button @click="prevImage" class="btn">&larr;</button>
          <button @click="nextImage" class="btn">&rarr;</button>
        </div>
      </section>

      <div class="controls-container">
        <section class="card counter">
          <h2>Penghitung Angka</h2>
          <div class="content">
            <p class="count">{{ count }}</p>
            <div>
              <button @click="incrementCount" class="btn">+</button>
            </div>
          </div>
        </section>

        <section class="card color-changer">
          <h2>Warna-warna</h2>
          <div class="content">
            <div class="color-box" :style="{ backgroundColor: boxColor }"></div>
            <button @click="changeColor" class="btn">Ubah</button>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      count: 0,
      boxColor: '#FFB3BA',
      images: [
        'https://i.pinimg.com/originals/58/fd/de/58fdde8cbc17d77bb8d68719b61e94f3.jpg',
        'https://i.pinimg.com/originals/c0/77/05/c07705b7f67ae3c65f1158007deb611f.jpg',
        'https://i.pinimg.com/originals/26/10/ac/2610acdeee1a8ddd8b86a4267a9bce14.jpg'
      ],
      currentImageIndex: 0,
      pastelColors: ['#FFB3BA', '#BAFFC9', '#BAE1FF', '#FFFFBA', '#FFDFBA'],
      currentBackgroundColor: '#FFB3BA'
    }
  },
  methods: {
    incrementCount() {
      this.count++
    },
    changeColor() {
      this.boxColor = this.getRandomColor()
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length
    },
    prevImage() {
      this.currentImageIndex =
        (this.currentImageIndex - 1 + this.images.length) % this.images.length
    },
    getRandomColor() {
      return this.pastelColors[Math.floor(Math.random() * this.pastelColors.length)]
    },
    changeBackgroundColor() {
      this.currentBackgroundColor = this.getRandomColor()
    }
  },
  mounted() {
    // Change background color every 5 seconds
    setInterval(this.changeBackgroundColor, 5000)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

body {
  margin: 0;
  padding: 0;
}

.dashboard {
  font-family: 'Poppins', sans-serif;
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  transition: background-color 2s ease;
}

.title {
  text-align: center;
  color: #696969;
  font-size: 2.5rem;
  margin-bottom: 2rem;
  font-weight: 600;
}

.horizontal-layout {
  display: flex;
  gap: 20px;
}

.card {
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

.carousel {
  flex: 2;
}

.controls-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

h2 {
  color: #696969;
  margin-top: 0;
  font-size: 1.2rem;
  font-weight: 600;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.count {
  font-size: 3rem;
  font-weight: 600;
  color: #ffb3ba;
  margin: 10px 0;
}

.color-box {
  width: 100px;
  height: 100px;
  border-radius: 10px;
  margin: 10px 0;
}

.btn {
  background-color: #ffb3ba;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin: 5px;
  font-family: 'Poppins', sans-serif;
  font-weight: 400;
}

.btn:hover {
  background-color: #ffa0ab;
}

.image-container {
  position: relative;
  width: 100%;
  height: 400px;
  overflow: hidden;
  border-radius: 10px;
}

.carousel-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-controls {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .horizontal-layout {
    flex-direction: column;
  }

  .image-container {
    height: 300px;
  }
}
</style>
