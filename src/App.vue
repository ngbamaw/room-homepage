<script lang="ts">
import ArrowIcon from './assets/images/icon-arrow.svg?component'

export default {
  components: { ArrowIcon },
  data() {
    return {
      current: 0,
      menuOpen: false,
      slides: [
        {
          title: 'Discover innovative ways to decorate',
          description: `
        We provide unmatched quality, comfort, and style for property owners
        across the country. Our experts combine form and function in bringing
        your vision to life. Create a room in your own style with our collection
        and make your property a reflection of you and what you love.`,
          image: 'desktop-image-hero-1.jpg',
        },
        {
          title: 'We are available all across the globe',
          description: `
        With stores all over the
      world, it's easy for you to find furniture for your home or place of
      business. Locally, we’re in most major cities throughout the country. Find
      the branch nearest you using our store locator. Any questions? Don't
      hesitate to contact us today.`,
          image: 'desktop-image-hero-2.jpg',
        },
        {
          title: 'Manufactured with the best materials',
          description: `Our modern
      furniture store provide a high level of quality. Our company has invested
      in advanced technology to ensure that every product is made as perfect and
      as consistent as possible. With three decades of experience in this
      industry, we understand what customers want for their home and office.`,
          image: 'desktop-image-hero-3.jpg',
        },
      ],
    }
  },
  methods: {
    getImgUrl(imgName: string) {
      return new URL(`./assets/images/${imgName}`, import.meta.url).href
    }
  },
}
</script>
<template>
  <div id="page" :class="{ 'lock-scroll': menuOpen }">
    <transition name="fade">
      <div v-show="menuOpen" class="filter"></div>
    </transition>
    <div class="menu-mobile" :class="{ open: menuOpen }">
      <div class="content">
        <button type="button" class="btn-close" @click="menuOpen = false">
          <img src="./assets/images/icon-close.svg" alt="close" />
        </button>
        <ul>
          <li>home</li>
          <li>shop</li>
          <li>about</li>
          <li>contact</li>
        </ul>
      </div>
    </div>
    <div class="menu">
      <button type="button" class="btn-menu" @click="menuOpen = true">
        <img
          src="./assets/images/icon-hamburger.svg"
          alt="open"
        />
      </button>
      <h1>room</h1>
      <ul class="not-mobile">
        <li>home</li>
        <li>shop</li>
        <li>about</li>
        <li>contact</li>
      </ul>
    </div>
    <div class="line first">
      <div class="slider">
        <img
          v-for="slide in slides"
          :key="slide.title"
          :src="getImgUrl(slide.image)"
          :style="{ transform: `translateX(${-100 * current}% )` }"
          alt="first-image"
        />
        <div class="slider-control mobile">
          <button
            class="btn-arrow"
            type="button"
            :disabled="current === 0"
            @click="current--"
          >
            <img
              src="./assets/images/icon-angle-left.svg"
              alt="left"
            /></button
          ><button
            class="btn-arrow"
            type="button"
            :disabled="current === slides.length - 1"
            @click="current++"
          >
            <img
              src="./assets/images/icon-angle-right.svg"
              alt="right"
            />
          </button>
        </div>
      </div>
      <div class="description">
        <transition name="fade" mode="out-in">
          <div :key="current" class="details">
            <h2>{{ slides[current].title }}</h2>
            <p>{{ slides[current].description }}</p>
            <a href="#" class="shop-link"
              >SHOP NOW
              <ArrowIcon class="arrow-shop" />
            </a>
          </div>
        </transition>
        <div class="slider-control not-mobile">
          <button
            class="btn-arrow"
            type="button"
            :disabled="current === 0"
            @click="current--"
          >
            <img
              src="./assets/images/icon-angle-left.svg"
              alt="left"
            /></button
          ><button
            class="btn-arrow"
            type="button"
            :disabled="current === slides.length - 1"
            @click="current++"
          >
            <img
              src="./assets/images/icon-angle-right.svg"
              alt="right"
            />
          </button>
        </div>
      </div>
    </div>
    <div class="line second">
      <img
        id="img-dark"
        src="./assets/images/image-about-dark.jpg"
      />
      <div class="about-section">
        <div class="text">
          <h2>About our furniture</h2>
          <p>
            Our multifunctional collection blends design and function to suit
            your individual taste. Make each room unique, or pick a cohesive
            theme that best express your interests and what inspires you. Find
            the furniture pieces you need, from traditional to contemporary
            styles or anything in between. Product specialists are available to
            help you create your dream space.
          </p>
        </div>
      </div>
      <img
        id="img-light"
        src="./assets/images/image-about-light.jpg"
      />
    </div>
  </div>
</template>
<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
#page {
  display: flex;
  flex-wrap: wrap;
  font-family: 'Spartan', sans-serif;
  .menu-mobile {
    display: none;
  }
  &.lock-scroll {
    overflow: hidden;
    height: 100vh;
  }
}
.line {
  display: flex;
  width: 100%;
  &.first {
    height: 70vh;
  }

  &.second {
    height: 30vh;
  }
}
.filter {
  position: absolute;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  background: rgba($color: #000000, $alpha: 0.5);
  z-index: 1;
}
.menu {
  position: absolute;
  top: 40px;
  left: 50px;
  display: flex;
  align-items: center;
  color: white;
  z-index: 10;
  h1 {
    margin-right: 60px;
  }
  ul {
    display: flex;
    gap: 40px;
    li {
      list-style: none;
    }
  }
}

.btn-menu {
  display: none;
}

.slider {
  width: 60%;
  display: flex;
  overflow: hidden;
  img {
    min-width: 100%;
    max-height: 100%;
    transition: transform 0.5s;
  }
}
.description {
  width: 40%;
  display: flex;
  flex-direction: column;
  .details {
    margin: auto;
    width: 60%;
    & > * {
      margin-bottom: 36px;
    }
    h2 {
      font-size: 36px;
      font-weight: 700;
    }
    p {
      font-size: 14px;
      color: hsl(0, 0%, 63%);
    }
    .shop-link {
      color: black;
      text-decoration: none;
      letter-spacing: 10px;
      display: flex;
      margin: 0;
      align-items: center;
      text-align: center;
      .arrow-shop {
        transition: all 0.5s;
        margin-left: 50px;
      }
      &:hover {
        color: hsl(0, 0%, 63%);
        .arrow-shop {
          path {
            fill: hsl(0, 0%, 63%);
          }
        }
      }
    }
  }
}
#img-dark {
  width: 30%;
}
#img-light {
  width: 30%;
}
.slider-control {
  width: 10vw;
  height: 5vw;
  .btn-arrow {
    background-color: black;
    border: none;
    width: 50%;
    height: 100%;
    &:hover {
      background-color: hsl(0, 0%, 27%);
    }
  }
}
.about-section {
  width: 40%;
  display: flex;
  flex-direction: column;
  .text {
    h2 {
      margin-bottom: 10px;
    }
    p {
      font-size: 14px;
      color: hsl(0, 0%, 63%);
    }
    margin: auto;
    width: 80%;
  }
}

@media screen and (max-width: 768px) {
  #page {
    flex-direction: column;
    .menu-mobile {
      top: 0;
      left: 0;
      width: 100%;
      height: 0;
      z-index: 9999;
      position: absolute;
      background-color: white;
      display: block;
      overflow: hidden;
      transition: height 0.5s;
      &.open {
        height: 120px;
      }

      .content {
        height: 120px;
        width: 100%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        background-color: white;
        ul {
          display: flex;
          gap: 24px;
          margin-right: 24px;
          li {
            list-style: none;
            font-weight: bold;
            font-size: 14px;
          }
        }
        .btn-close {
          margin-right: auto;
          margin-left: 24px;
          background-color: transparent;
          border: none;
          cursor: pointer;
          img {
            width: 24px;
            height: 24px;
          }
        }
      }
    }
  }
  .menu {
    width: 100%;
    left: 0;
    h1 {
      margin: auto;
    }
    .btn-menu {
      display: block;
      position: absolute;
      left: 24px;
      background-color: transparent;
      border: none;
      cursor: pointer;
      img {
        width: 36px;
        height: 24px;
      }
    }
  }
  .line {
    &.first {
      height: auto;
    }
    &.second {
      height: auto;
    }
    flex-wrap: wrap;
  }
  .slider {
    width: 100%;
    height: 285px;
    position: relative;
    img {
      min-width: 100%;
      max-height: 100%;
    }

    .slider-control.mobile {
      width: 125px;
      height: 75px;
      position: absolute;
      bottom: 0;
      right: 0;
      .btn-arrow {
        background-color: black;
        border: none;
        width: 50%;
        height: 100%;
        padding: 25px;
      }
    }
  }
  .description {
    width: 100%;
    padding: 50px 30px;
    .details {
      width: 100%;
      h2 {
        font-size: 24px;
      }
      p {
        font-size: 12px;
      }
    }
  }
  .not-mobile {
    display: none !important;
  }
  #img-dark {
    width: 100%;
  }
  #img-light {
    width: 100%;
  }
  .about-section {
    width: 100%;
    padding: 50px 30px;
    .text {
      width: 100%;
      h2 {
        font-size: 24px;
      }
      p {
        font-size: 12px;
      }
    }
  }
}
</style>
