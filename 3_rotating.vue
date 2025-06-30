<template>
  <div class="container" :class="{ 'show-nav': isNavVisible }">
    <div class="circle-container">
      <div class="circle">
        <button id="close" @click="toggleNav">
          <i class="fas fa-times"></i>
        </button>
        <button id="open" @click="toggleNav">
          <i class="fas fa-bars"></i>
        </button>
      </div>
    </div>

    <div class="content">
      <h1>Amazing Article</h1>
      <small>Florin Pop</small>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Accusantium quia in ratione dolores cupiditate, maxime aliquid impedit dolorem nam dolor omnis atque fuga labore modi veritatis porro laborum minus, illo, maiores recusandae cumque ipsa quos. Tenetur, consequuntur mollitia labore pariatur sunt quia harum aut. Eum maxime dolorem provident natus veritatis molestiae cumque quod voluptates ab non, tempore cupiditate? Voluptatem, molestias culpa. Corrupti, laudantium iure aliquam rerum sint nam quas dolor dignissimos in error placeat quae temporibus minus optio eum soluta cupiditate! Cupiditate saepe voluptates laudantium. Ducimus consequuntur perferendis consequatur nobis exercitationem molestias fugiat commodi omnis. Asperiores quia tenetur nemo ipsa.</p>

      <h3>My Dog</h3>
      <img src="https://images.unsplash.com/photo-1507146426996-ef05306b995a" alt="doggy" />
      <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sit libero deleniti rerum quo, incidunt vel consequatur culpa ullam. Magnam facere earum unde harum. Ea culpa veritatis magnam at aliquid. Perferendis totam placeat molestias illo laudantium? Minus id minima doloribus dolorum fugit deserunt qui vero voluptas, ut quia cum amet temporibus veniam ad ea ab perspiciatis, enim accusamus asperiores explicabo provident. Voluptates sint, neque fuga cum illum, tempore autem maxime similique laborum odio, magnam esse. Aperiam?</p>
    </div>
</div>
    <nav class="{ 'show-nav': isNavVisible }"> <!--非常重要！nav需要在container外部，因为container自己带的唯一会让fix失效-->
      <ul>
        <li><i class="fas fa-home"></i><a href="#"> Home</a></li>
        <li><i class="fas fa-user-alt"></i><a href="https://cn.bing.com/images/search?view=detailV2&ccid=319YjT8m&id=30D304F71F2008620808E8030220B9CC95CE1D9B&thid=OIP.319YjT8mAzDbcd83QKl72wHaEo&mediaurl=https%3A%2F%2Fts1.tc.mm.bing.net%2Fth%2Fid%2FR-C.df5f588d3f260330db71df3740a97bdb%3Frik%3Dmx3Olcy5IAID6A%26riu%3Dhttp%253a%252f%252fwww.quazero.com%252fuploads%252fallimg%252f140412%252f1-140412005948.jpg%26ehk%3DUVmH2F4NdtSlAldhUocNyGGBcIvrIMzndOzSgvqqveY%253d%26risl%3D%26pid%3DImgRaw%26r%3D0&exph=1200&expw=1920&q=%E5%B0%8F%E7%8B%97&simid=608053862840162813&FORM=IRPRST&ck=4BDC83756CB4F3270643FF29012CD802&selectedIndex=0&itb=0&qpvt=%E5%B0%8F%E7%8B%97&cw=1375&ch=751&ajaxhist=0&ajaxserp=0"> About</a></li>
        <li><i class="fas fa-envelope"></i><a href="#"> Contact</a></li>
      </ul>
    </nav>
  
</template>

<script setup>
import { ref } from 'vue'

const isNavVisible = ref(false)

const toggleNav = () => {
  isNavVisible.value = !isNavVisible.value
}
</script>
<style>
body {/*非常重要！对于body的格式，要在style单独列出，因为这是全局的设置*/ 
  font-family: 'Lato', sans-serif;
  background-color: #333;
  color: #222;
  overflow-x: hidden; /*溢出值格式*/
  margin: 0;
}

</style>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.min.css');

* {
  box-sizing: border-box; /*有星号，规定的是全局的大小计算方式*/ 
}



.container {
  background-color: #fafafa;
  transform-origin: top left;
  transition: transform 0.5s linear;
  width: 100vw;
  min-height: 100vh;
  padding:50px;
}


.container.show-nav {
  transform: rotate(-20deg);
}

.circle-container {
  position: fixed;
  top: -100px;
  left: -100px;
}

.circle {
  background-color: #ff7979;
  height: 200px;
  width: 200px;
  border-radius: 50%;
  position: relative;
  transition: transform 0.5s linear;
}

.container.show-nav .circle {
  transform: rotate(-70deg);
}

.circle button {
  cursor: pointer;
  position: absolute;
  top: 50%;
  left: 50%;
  height: 100px;
  background: transparent;
  border: 0;
  font-size: 26px;
  color: #fff;
}

.circle button:focus {
  outline: none;
}

.circle button#open {
  left: 60%;
}

.circle button#close {
  top: 60%;
  transform: rotate(90deg);
  transform-origin: top left;
}


nav {
  position: fixed;
  bottom: 40px;
  left: 0;
  z-index: 100;
}

nav ul {
  list-style-type: none;
  padding-left: 30px;
}

nav ul li {
  text-transform: uppercase;
  color: #fff;
  margin: 40px 0;
  transform: translateX(-100%);
  transition: transform 0.4s ease-in;
}

nav ul li i {
  font-size: 20px;
  margin-right: 10px;
}

nav ul li + li {
  margin-left: 15px;
  transform: translateX(-150%);
}

nav ul li + li + li {
  margin-left: 30px;
  transform: translateX(-200%);
}


.show-nav + nav li {
  transform: translateX(0);
  transition-delay: 0.3s;
}


nav a {
  color: #fafafa;
  text-decoration: none;
  transition: all 0.5s;
}

nav a:hover {
  color: #FF7979;
  font-weight: bold;
}

.content img {
  max-width: 100%;
}

.content {
  max-width: 1000px;
  margin: 50px auto;
}

.content h1 {
  margin: 0;
}

.content small {
  color: #555;
  font-style: italic;
}

.content p {
  color: #333;
  line-height: 1.5;
}
</style>