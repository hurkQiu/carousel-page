<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->

<template>
  <div class="container">
    <nav>
      <div></div>
      <ul class="menu">
        <li :class="['item', { active: page === 0 }]">Home</li>
        <li :class="['item', { active: page === 1 }]">Food</li>
        <li :class="['item', { active: page === 2 }]">Festivals</li>
        <li :class="['item', { active: page === 3 }]">Flights</li>
        <li :class="['item', { active: page === 4 }]">Stays</li>
        <li :class="['item', { active: page === 5 }]">Contact</li>
        <li class="language">
          <div class="svg-container">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M12 21a9.004 9.004 0 008.716-6.747M12 21a9.004 9.004 0 01-8.716-6.747M12 21c2.485 0 4.5-4.03 4.5-9S14.485 3 12 3m0 18c-2.485 0-4.5-4.03-4.5-9S9.515 3 12 3m0 0a8.997 8.997 0 017.843 4.582M12 3a8.997 8.997 0 00-7.843 4.582m15.686 0A11.953 11.953 0 0112 10.5c-2.998 0-5.74-1.1-7.843-2.918m15.686 0A8.959 8.959 0 0121 12c0 .778-.099 1.533-.284 2.253m0 0A17.919 17.919 0 0112 16.5c-3.162 0-6.133-.815-8.716-2.247m0 0A9.015 9.015 0 013 12c0-1.605.42-3.113 1.157-4.418"
              ></path>
            </svg>
          </div>
          <div>language</div>
        </li>
      </ul>
    </nav>
    <div id="carousel-container">
      <div
        class="carousel"
        v-for="(item, index) in data"
        :key="index"
        v-bind:style="{ 'background-image': 'url(' + item.imgSrc + ')' }"
      >
        <div class="content">
          <div class="title">{{ item.title }}</div>
          <div class="description">{{ item.description }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onUnmounted, onMounted, ref } from "vue";
const data = [
  {
    title: "Kenting National Park",
    description:
      "Kenting National Park , commonly known as Kenting , is a national park located on the Hengchun Peninsula of Pingtung County, Taiwan, covering Hengchun, Checheng, and Manzhou Townships. Established on 1 January 1984,it is Taiwan's oldest and the southernmost national park on the main island, covering the southernmost area of the Taiwan island along Bashi Channel. Administered by the Executive Yuan's Ministry of the Interior, this national park is well known for its tropical climate and sunshine, scenic mountain and beach, the Spring Scream rock-band festival held in every March, and has long been one of the most popular tourist destinations in Taiwan with 5.84 million visitors in 2016.",
    imgSrc:
      "https://taiwanstartshere.com/wp-content/uploads/2020/05/Kenting-National-Park.jpg",
  },
  {
    title: "Sun Moon Lake",
    description:
      "Sun Moon Lake is a lake in Yuchi Township, Nantou County, Taiwan. It is the largest body of water in Taiwan. The area around the lake is home to the Thao tribe, one of Taiwan's aboriginal tribes. Sun Moon Lake surrounds a tiny island called Lalu. The east side of the lake resembles a sun while the west side resembles a moon, hence the name.",
    imgSrc: "https://www.sunmoonlake.gov.tw/zh-tw/social-article/3177",
  },
  {
    title: "Alishan National Scenic Area",
    description:
      "Alishan is 415 square kilometres (41,500 ha) in area. Notable characteristics include mountain wilderness, four villages, waterfalls, high altitude tea plantations, the Alishan Forest Railway, and a number of hiking trails. The area is popular with tourists and mountain climbers. Alishan, itself has become one of the major landmarks associated with Taiwan. The area is famous for its production of high mountain tea and wasabi.",
    imgSrc:
      "https://www.hotelscombined.com/rimg/dimg/22/9f/f5016547-lm-170291-17e92ead742.jpg?width=1366&height=768&xhint=1377&yhint=908&crop=true&watermarkposition=lowerright",
  },
  {
    title: "Tamsui",
    description:
      "Tamsui District is a seaside district in New Taipei City, Taiwan adjacent to the Tamsui River and overlooking the Taiwan Strait. The name of the district means `fresh water in Chinese. Although modest in size (population 189,271), Tamsui plays a significant role in Taiwanese history and culture. ",
    imgSrc:
      "https://upload.wikimedia.org/wikipedia/commons/8/89/Tamsui_Fisherman%27s_Wharf_2012.jpg",
  },
  {
    title: "Jiufen",
    description:
      "Jiufen, also spelled Jioufen or Chiufen, is a seaside mountain area in Ruifang District, New Taipei City, Taiwan.Jiufen Old Street is a narrow, winding alleyway with shops, teahouses, and restaurants that offers tourists a view of traditional Taiwanese life. ",
    imgSrc:
      "https://newtaipei.travel/content/images/attractions/27525/1024x768_attractions-image-fwfaxumoiegq42wwkiwkpg.jpg",
  },
  {
    title: "Liuqiu Island",
    description:
      "Liuqiu, also known by several other names, is a coral island in the Taiwan Strait about 13 kilometers (8 mi) southwest of the main island of Taiwan. It has an area of 6.8 km2 (2.6 sq mi) and approximately 12,200 residents, the vast majority of whom share only 10 surnames. It is administered as a township of Pingtung County in Taiwan Province, Republic of China. As of 2019 the township chief is Chen Lung-chin.",
    imgSrc:
      "https://storage.googleapis.com/smiletaiwan-cms-cwg-tw/article/201904/article-5cb9e9d42c591.jpg",
  },
];
const select = ref(0);
const page = ref(0);
const carouselTimeout = () => {
  const container = document.getElementById("carousel-container");
  const items = document.querySelectorAll(".carousel");
  setInterval(() => {
    container.append(items[select.value]);
    select.value += 1;
    if (select.value > 5) select.value = 0;
  }, 5000);
};
onMounted(() => {
  carouselTimeout();
});
onUnmounted(() => {
  clearInterval(carouselTimeout);
});
</script>

<style>
* {
  padding: 0;
  margin: 0;
  font-family: inter, Arial, Helvetica, sans-serif;
}
nav {
  display: flex;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 10;
  justify-content: space-between;
  color: white;
  font-size: 16px;
  font-weight: bold;
  padding: 20px 20px;
}
.menu {
  display: flex;
  position: relative;
  gap: 20px;
  list-style: none;
}
.item {
  display: flex;
  position: relative;
  cursor: pointer;
}
.menu .item:hover::after {
  content: "";
  width: 100%;
  position: absolute;
  bottom: -5px;
  height: 3px;
  left: 0;
  background-color: orange;
  border-radius: 50px;
}
.menu .active::after {
  content: "";
  width: 100%;
  position: absolute;
  bottom: -5px;
  height: 3px;
  left: 0;
  background-color: orange;
  border-radius: 50px;
}
.menu {
  &.last-child {
    gap: 2px;
  }
}
.language {
  display: flex;
  width: 100px;
  cursor: pointer;
}
.svg-container {
  width: 20px;
  height: 20px;
}
.container {
  width: 100%;
  height: 100vh;
  position: relative;
  overflow: hidden;
}
.content {
  width: min(40vw, 500px);
  max-height: 400px;
  position: absolute;
  top: 60%;
  left: 5%;
  opacity: 0;
  transform: translateY(-50%);
  & .description {
    color: rgb(255, 255, 255);
    text-align: justify;
    line-height: 1.2;
    font-size: 18px;
    background: rgba(104, 104, 104, 0.5);
  }
}
.title {
  display: flex;
  justify-content: center;
  font-size: 48px;
  font-weight: bold;
  text-align: start;
  color: white;
  font-style: italic;
}
.carousel {
  width: 220px;
  height: 300px;
  background-size: cover;
  background-position: center;
  position: absolute;
  top: 70%;
  transform: translateY(-50%);
  transition: transform 0.1s, left 0.75s, top 0.75s, width 0.75s, height 0.75s;
  &:nth-child(1),
  &:nth-child(2) {
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    transform: none;
  }
  &:nth-child(3) {
    --child-index: 0;
  }
  &:nth-child(4) {
    --child-index: 1;
  }
  &:nth-child(5) {
    --child-index: 2;
  }
  &:nth-child(6) {
    --child-index: 3;
  }
  left: calc(50% + var(--child-index) * 230px);
}
.carousel:nth-of-type(2) .content {
  display: block;
  animation: show 0.5s ease-in-out 0.3s forwards;
}
@keyframes show {
  0% {
    opacity: 0.2;
    transform: translateY(calc(-50% + 80px));
  }
  100% {
    opacity: 1;
  }
}
</style>
