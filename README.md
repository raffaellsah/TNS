# TNS


<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;700&display=swap" rel="stylesheet" />

  <link rel="shortcut icon" href="./images/favicon.ico" type="image/x-icon" />


  <!-- Carousel -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Glide.js/3.4.1/css/glide.core.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Glide.js/3.4.1/css/glide.theme.min.css
">
  <link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css" />

  <!-- Custom StyleSheet -->
  <link rel="stylesheet" href="./css/style.min.css" />

  <title>Phone</title>
</head>

<body>

<script>

const navOpen = document.querySelector(".nav__hamburger"),
  navClose = document.querySelector(".close__toggle"),
  menu = document.querySelector(".nav__menu"),
  scrollLink = document.querySelectorAll(".scroll-link"),
  navContainer = document.querySelector(".nav__menu");
navOpen.addEventListener("click", () => {
  menu.classList.add("open"),
    document.body.classList.add("active"),
    (navContainer.style.left = "0"),
    (navContainer.style.width = "30rem");
}),
  navClose.addEventListener("click", () => {
    menu.classList.remove("open"),
      document.body.classList.remove("active"),
      (navContainer.style.left = "-30rem"),
      (navContainer.style.width = "0");
  });
const popup = document.querySelector(".popup"),
  closePopup = document.querySelector(".popup__close");
popup &&
  (closePopup.addEventListener("click", () => {
    popup.classList.add("hide__popup");
  }),
  window.addEventListener("load", () => {
    setTimeout(() => {
      popup.classList.remove("hide__popup");
    }, 500);
  }));
const navBar = document.querySelector(".navigation"),
  gotoTop = document.querySelector(".goto-top");
Array.from(scrollLink).map(e => {
  e.addEventListener("click", e => {
    e.preventDefault();
    const t = e.currentTarget.getAttribute("href").slice(1),
      n = document.getElementById(t),
      i = navBar.getBoundingClientRect().height,
      o = navBar.classList.contains("fix__nav");
    let s = n.offsetTop - i;
    o || (s -= i),
      window.scrollTo({ left: 0, top: s }),
      (navContainer.style.left = "-30rem"),
      document.body.classList.remove("active");
  });
}),
  window.addEventListener("scroll", e => {
    const t = window.pageYOffset;
    t > navBar.getBoundingClientRect().height
      ? navBar.classList.add("fix__nav")
      : navBar.classList.remove("fix__nav"),
      t > 300
        ? gotoTop.classList.add("show-top")
        : gotoTop.classList.remove("show-top");
  });
const getProducts = async () => {
    try {
      const e = await fetch("/data/products.json");
      return (await e.json()).products;
    } catch (e) {
      console.log(e);
    }
  },
  categoryCenter = document.querySelector(".category__center");
window.addEventListener("DOMContentLoaded", async function () {
  const e = await getProducts();
  displayProductItems(e);
});
const displayProductItems = e => {
    let t = e.map(
      e =>
        ` \n                  <div class="product category__products">\n                    <div class="product__header">\n                      <img src=${e.image} alt="product">\n                    </div>\n                    <div class="product__footer">\n                      <h3>${e.title}</h3>\n                      <div class="rating">\n                        <svg>\n                          <use xlink:href="./images/sprite.svg#icon-star-full"></use>\n                        </svg>\n                        <svg>\n                          <use xlink:href="./images/sprite.svg#icon-star-full"></use>\n                        </svg>\n                        <svg>\n                          <use xlink:href="./images/sprite.svg#icon-star-full"></use>\n                        </svg>\n                        <svg>\n                          <use xlink:href="./images/sprite.svg#icon-star-full"></use>\n                        </svg>\n                        <svg>\n                          <use xlink:href="./images/sprite.svg#icon-star-empty"></use>\n                        </svg>\n                      </div>\n                      <div class="product__price">\n                        <h4>$${e.price}</h4>\n                      </div>\n                      <a href="#"><button type="submit" class="product__btn">Add To Cart</button></a>\n                    </div>\n                  <ul>\n                      <li>\n                        <a data-tip="Quick View" data-place="left" href="#">\n                          <svg>\n                            <use xlink:href="./images/sprite.svg#icon-eye"></use>\n                          </svg>\n                        </a>\n                      </li>\n                      <li>\n                        <a data-tip="Add To Wishlist" data-place="left" href="#">\n                          <svg>\n                            <use xlink:href="./images/sprite.svg#icon-heart-o"></use>\n                          </svg>\n                        </a>\n                      </li>\n                      <li>\n                        <a data-tip="Add To Compare" data-place="left" href="#">\n                          <svg>\n                            <use xlink:href="./images/sprite.svg#icon-loop2"></use>\n                          </svg>\n                        </a>\n                      </li>\n                  </ul>\n                  </div>\n                  `
    );
    (t = t.join("")), categoryCenter && (categoryCenter.innerHTML = t);
  },
  filterBtn = document.querySelectorAll(".filter-btn"),
  categoryContainer = document.getElementById("category");
categoryContainer &&
  categoryContainer.addEventListener("click", async e => {
    const t = e.target.closest(".section__title");
    if (!t) return;
    const n = t.dataset.id,
      i = await getProducts();
    if (n) {
      Array.from(filterBtn).forEach(e => {
        e.classList.remove("active");
      }),
        t.classList.add("active");
      let e = i.filter(e => {
        if (e.category === n) return e;
      });
      displayProductItems("All Products" === n ? i : e);
    }
  });
const pic1 = document.getElementById("pic1"),
  pic2 = document.getElementById("pic2"),
  pic3 = document.getElementById("pic3"),
  pic4 = document.getElementById("pic4"),
  pic5 = document.getElementById("pic5"),
  picContainer = document.querySelector(".product__pictures"),
  zoom = document.getElementById("zoom"),
  pic = document.getElementById("pic"),
  picList = [pic1, pic2, pic3, pic4, pic5];
let picActive = 1;
["mouseover", "touchstart"].forEach(e => {
  picContainer &&
    picContainer.addEventListener(e, e => {
      const t = e.target.closest("img");
      if (!t) return;
      const n = t.id.slice(3);
      changeImage(`./images/products/iPhone/iphone${n}.jpeg`, n);
    });
});
const changeImage = (e, t) => {
    (pic.src = e),
      (zoom.style.backgroundImage = `url(${e})`),
      picList[picActive - 1].classList.remove("img-active"),
      picList[t - 1].classList.add("img-active"),
      (picActive = t);
  },
  btns = document.querySelectorAll(".detail-btn"),
  detail = document.querySelector(".product-detail__bottom"),
  contents = document.querySelectorAll(".content");
detail &&
  detail.addEventListener("click", e => {
    const t = e.target.closest(".detail-btn");
    if (!t) return;
    const n = t.dataset.id;
    if (n) {
      Array.from(btns).forEach(t => {
        t.classList.remove("active"),
          e.target.closest(".detail-btn").classList.add("active");
      }),
        Array.from(contents).forEach(e => {
          e.classList.remove("active");
        }),
        document.getElementById(n).classList.add("active");
    }
  });
const slider1 = document.getElementById("glide_1"),
  slider2 = document.getElementById("glide_2"),
  slider3 = document.getElementById("glide_3"),
  slider4 = document.getElementById("glide_4"),
  slider5 = document.getElementById("glide_5");
slider1 &&
  new Glide(slider1, {
    type: "carousel",
    startAt: 0,
    autoplay: 3e3,
    hoverpause: !0,
    perView: 1,
    animationDuration: 800,
    animationTimingFunc: "linear",
  }).mount(),
  slider2 &&
    new Glide("#glide_2", {
      type: "carousel",
      startAt: 0,
      perView: 4,
      rewin: !1,
      animationDuration: 800,
      animationTimingFunc: "cubic-bezier(0.165, 0.840, 0.440, 1.000)",
      breakpoints: { 1200: { perView: 3 }, 768: { perView: 2 } },
    }).mount(),
  slider3 &&
    new Glide("#glide_3", {
      type: "carousel",
      startAt: 0,
      perView: 4,
      rewin: !1,
      animationDuration: 800,
      animationTimingFunc: "cubic-bezier(0.165, 0.840, 0.440, 1.000)",
      breakpoints: { 1200: { perView: 3 }, 768: { perView: 2 } },
    }).mount(),
  slider4 &&
    new Glide("#glide_4", {
      type: "carousel",
      startAt: 0,
      perView: 1,
      rewin: !1,
      animationDuration: 800,
      animationTimingFunc: "cubic-bezier(0.165, 0.840, 0.440, 1.000)",
    }).mount(),
  slider5 &&
    new Glide("#glide_5", {
      type: "carousel",
      startAt: 0,
      perView: 3,
      rewin: !1,
      autoplay: 3e3,
      animationDuration: 800,
      animationTimingFunc: "cubic-bezier(0.165, 0.840, 0.440, 1.000)",
      breakpoints: { 998: { perView: 2 }, 768: { perView: 1 } },
    }).mount(),
  AOS.init();

  </script>
  

  <!-- Header -->
  <header id="header" class="header">
    <div class="navigation">
      <div class="container">
        <nav class="nav">
          <div class="nav__hamburger">
            <svg>
              <use xlink:href="./images/sprite.svg#icon-menu"></use>
            </svg>
          </div>

          <div class="nav">
           
            <a href="https://icons8.com.br/icon/set/HOT/doodle" class="">
           loja 
              <a>
           
      

          <div class="nav__menu">
            <div class="menu__top">
              <span class="nav__category">kkkkkkk</span>
              <a href="https://icons8.com.br/icon/set/HOT/doodle" class="close__toggle">
               
              </a>
      
          </div>
        </nav>
      </div>
    </div>

    <!-- Hero -->
    <div class="hero">
      <div class="glide" id="glide_1">
        <div class="glide__track" data-glide-el="track">
          <ul class="glide__slides">
            <li class="glide__slide">
              <div class="hero__center">
                <div class="hero__left">
                   <h2 class="">HOT DOG TRADICIONAL</h2>
                  <p>CARNE MO�DA, SALSICHA, MAIONESE, KATCHUP, MILHO, BATATA PALHA</p>
                  <a href="/product.html"><button class="hero__btn">QUERO</button></a>
                </div>
                <div class="hero__right">
                  <div class="hero__img-container">
                    <img class="banner_01" src="https://img.icons8.com/doodle/2x/hot-dog.png" alt="banner2" />
                  </div>
                </div>
              </div>
            </li>
            <li class="glide__slide">
              <div class="hero__center">
                <div class="hero__left">
                  <span>New Inspiration 2020</span>
                  <h2>CELL PHONE TOP DEALS!</h2>
                  <p>Check out the latest deals on cell phones</p>
                  <a href="/product.html"><button class="hero__btn">SHOP NOW</button></a>
                </div>
                <div class="hero__right">
                  <img class="banner_02" src="https://img.icons8.com/doodle/2x/soup-plate.png" alt="banner2" />
                </div>
              </div>
            </li>
          </ul>
        </div>
        <div class="glide__bullets" data-glide-el="controls[nav]">
          <button class="glide__bullet" data-glide-dir="=0"></button>
          <button class="glide__bullet" data-glide-dir="=1"></button>
        </div>

        <div class="glide__arrows" data-glide-el="controls">
          <button class="glide__arrow glide__arrow--left" data-glide-dir="<">
            <svg>
              <use xlink:href="./images/sprite.svg#icon-arrow-left2"></use>
            </svg>
          </button>
          <button class="glide__arrow glide__arrow--right" data-glide-dir=">">
            <svg>
              <use xlink:href="./images/sprite.svg#icon-arrow-right2"></use>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </header>
  <!-- End Header -->

 
      <!-- Latest Products -->
      <section class="section latest__products" id="latest">
        <div class="title__container">
          <div class="section__title active" data-id="Latest Products">
            <span class="dot"></span>
            <h1 class="primary__title">MAIS PEDIDOS</h1>
          </div>
        </div>
        <div class="container" data-aos="fade-up" data-aos-duration="1200">
          <div class="glide" id="glide_2">
            <div class="glide__track" data-glide-el="track">
              <ul class="glide__slides latest-center">
                
                <li class="glide__slide">
                  <div class="product">
                    <div class="product__header">
                      <img src="https://img.icons8.com/doodle/2x/delete-sign.png" alt="product">
                    <div class="product__footer">
                      <h3>HOT 1</h3>
                    
                        <h4>R$7,50</h4>
                     
                      <a href="https://deadsimplechat.com/8plsrfud_"><button type="submit" class="product__btn">QUERO</button></a>
                    </div>
                    
             
                   
             <li class="glide__slide">
                  <div class="product">
                    <div class="product__header">
                      <img src="https://img.icons8.com/doodle/2x/delete-sign.png" alt="product">
                    <div class="product__footer">
                      <h3>HOT1</h3>
                    
                        <h4>R$7,50</h4>
                     
                      <a href="https://deadsimplechat.com/8plsrfud_"><button type="submit" class="product__btn">QUERO</button></a>
                    </div>
                      
                        </a>
                      </li>
                    </ul>
                  </div>

              </ul>
            </div>

            <div class="glide__arrows" data-glide-el="controls">
              <button class="glide__arrow glide__arrow--left" data-glide-dir="<">
                <svg>
                  <use xlink:href="./images/sprite.svg#icon-arrow-left2"></use>
                </svg>
              </button>
              <button class="glide__arrow glide__arrow--right" data-glide-dir=">">
                <svg>
                  <use xlink:href="./images/sprite.svg#icon-arrow-right2"></use>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </section>

     

    <!-- Facility Section -->
    <section class="facility__section section" id="facility">
      <div class="container">
        <div class="facility__contianer" data-aos="fade-up" data-aos-duration="1200">
          <div class="facility__box">
            <div class="facility-img__container">
              <svg>
                <use xlink:href="./images/sprite.svg#icon-airplane"></use>
              </svg>
            </div>
            <p>FREE SHIPPING WORLD WIDE</p>
          </div>

          <div class="facility__box">
            <div class="facility-img__container">
              <svg>
                <use xlink:href="./images/sprite.svg#icon-credit-card-alt"></use>
              </svg>
            </div>
            <p>100% MONEY BACK</p>
          </div>

          <div class="facility__box">
            <div class="facility-img__container">
              <svg>
                <use xlink:href="./images/sprite.svg#icon-credit-card"></use>
              </svg>
            </div>
            <p>MANY PAYMENT GATEWAYS</p>
          </div>

          <div class="facility__box">
            <div class="facility-img__container">
              <svg>
                <use xlink:href="./images/sprite.svg#icon-headphones"></use>
              </svg>
            </div>
            <p>24/7 ONLINE SUPPORT</p>
          </div>
        </div>
      </div>
    </section>
    </div>

 

    <!-- NewsLetter -->
    <section class="section newsletter" id="contact">
      <div class="container" data-aos="fade-up" data-aos-duration="1200">
        <div class="newsletter__content">
          <div class="newsletter__data">
            <h3>SU</h3>
            <p>A short sentence describing what someone will receive by subscribing</p>
          </div>
          <form action="#">
            <input type="email" placeholder="Enter your email address" class="newsletter__email">
            <a class="newsletter__link" href="#">subscribe</a>
          </form>
        </div>
      </div>
    </section>

  </main>

  <!-- End Main -->

 


  <!-- Glide Carousel Script -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/Glide.js/3.4.1/glide.min.js"></script>

  <!-- Animate On Scroll -->
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

  <!-- Custom JavaScript -->
  <script src="./js/bundle.min.js"></script>

</body>

</html>
  
  
   <link rel="stylesheet" href="main.css">
    <script src="https://kit.fontawesome.com/332a215f17.js" crossorigin="anonymous"></script>
    <link href="https://fonts.googleapis.com/css?family=Baloo+Chettan+2:400,700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="./magnific/magnific-popup.css">
</head>
  
   <!---Social Icons-->
   <section id="social-icons">
       <a href="#"><i class="fab fa-facebook facebook"></i></a>
       <a href="#"><i class="fab fa-twitter twitter"></i></a>
       <a href="#"><i class="fab fa-instagram instagram"></i></a>
       <a href="#"><i class="fab fa-google-plus plus"></i></a>
   </section>
   <!--End of Social Icons-->

<style>
  
  :root{--primaryColor:#f1f1f1;--black:#222;--black2:#555;--black3:#252525;--black4:#000;--black5:#212529;--orange:#eb0028;--white:#fff;--grey:#959595;--grey2:#666;--grey3:#ccc;--secondaryColor:#2b1f4d;--yellow:#ffcc00;--green:#59b210}*{margin:0;padding:0;-webkit-box-sizing:inherit;box-sizing:inherit}html{font-size:62.5%;-webkit-box-sizing:border-box;box-sizing:border-box;scroll-behavior:smooth}body,input{font-size:1.6rem;font-weight:400;font-family:Archivo,sans-serif;color:var(--black)}a{text-decoration:none}ul{list-style:none}img{max-width:100%}h3,h4{font-weight:500}.header{position:relative}.container{max-width:117rem;margin:0 auto;padding:0 1.6rem}.navigation{position:relative;height:7rem;-webkit-box-shadow:0 .5rem 1.5rem rgba(0,0,0,.1);box-shadow:0 .5rem 1.5rem rgba(0,0,0,.1)}.nav{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;height:100%;height:7rem;padding:0 1rem}.fix__nav{position:fixed;top:0;left:0;width:100%;background-color:var(--white);z-index:1200}.nav__logo a{font-size:2.5rem;color:var(--black);padding:1.6rem;font-weight:700}.nav__hamburger{display:none;cursor:pointer}.nav__hamburger svg{height:2.3rem;width:2.3rem}.menu__top{display:none}.nav__menu{width:50%}.nav__list{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;height:100%;width:50%}.nav__item:not(:last-child){margin-right:1.6rem}.nav__list .nav__link:link,.nav__list .nav__link:visited{display:inline-block;font-size:1.4rem;text-transform:uppercase;color:var(--black);-webkit-transition:color .3s ease-in-out;transition:color .3s ease-in-out}.nav__list .nav__link:hover{color:var(--orange)}.nav__icons{display:-webkit-box;display:-ms-flexbox;display:flex;position:relative}.nav__icons .icon__item svg{width:1.6rem;height:1.6rem}.nav__icons .icon__item{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;-webkit-box-align:center;-ms-flex-align:center;align-items:center;padding:.7rem;border:1px solid var(--black);border-radius:50%;-webkit-transition:background-color .3s ease-in-out;transition:background-color .3s ease-in-out}.nav__icons .icon__item:link,.nav__icons .icon__item:visited{color:var(--black)}.nav__icons .icon__item:hover{background-color:var(--orange);border:1px solid var(--black)}.nav__icons .icon__item:not(:last-child){margin-right:1rem}.nav__icons #cart__total{font-size:1rem;position:absolute;top:2px;right:-6px;background-color:var(--orange);padding:.2rem .4rem;border-radius:100%;color:var(--primaryColor)}.page__title-area{background-color:var(--primaryColor)}.page__title-container{padding:1rem}.page__titles{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;font-size:1.2rem;color:var(--grey2)}.page__titles a{margin-right:2rem}.page__titles a svg{width:1.8rem;height:1.8rem;fill:var(--grey2)}.page__title{position:relative}.page__title::before{position:absolute;content:"/";top:0;left:-1rem}@media only screen and (max-width:768px){.nav__menu{position:fixed;top:0;left:-30rem;width:0;background-color:var(--white);z-index:9990;height:100%;-webkit-transition:all .5s;transition:all .5s}.nav__menu.open{left:30rem;width:30rem}.nav__logo{width:50%}.nav__hamburger{display:block}.menu__top{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;background-color:var(--orange);padding:1.8rem 1rem}.menu__top svg{height:1.6rem;width:1.6rem;fill:var(--primaryColor)}.nav__category{color:var(--white);font-size:2.3rem;font-weight:700}.nav__list{-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;-webkit-box-align:start;-ms-flex-align:start;align-items:start;padding:1.6rem 1rem}.nav__item:not(:last-child){margin-right:0}.nav__item{width:100%}.nav__list .nav__link:link,.nav__list .nav__link:visited{padding:1.6rem 0;width:100%;color:var(--grey2)}body.active::before{content:"";position:fixed;top:0;left:0;width:100%;height:110%;background:var(--black) none no-repeat 0 0;opacity:.7;z-index:999;-webkit-transition:.8s;transition:.8s}}@media only screen and (max-width:568px){.nav__icons .icon__item svg{width:1.4rem;height:1.4rem}.nav__icons .icon__item{padding:.4rem}}.hero,.hero .glide__slides{background-color:var(--primaryColor);position:relative;width:100%;height:100vh}.hero .glide__bullet{background-color:#222;width:1.2rem;height:1.2rem}.hero .glide__arrow{padding:1.5rem 1.7rem;opacity:0;border:none;background-color:var(--grey);-webkit-transition:all .5s ease-in-out .2s;transition:all .5s ease-in-out .2s}.glide__arrow:hover{background-color:var(--black)}.glide__arrow--left{left:20rem}.glide__arrow--right{position:absolute;right:20rem}.hero:hover .glide__arrow{opacity:1}.hero:hover .glide__arrow--left{left:23rem}.hero:hover .glide__arrow--right{right:23rem}.hero .glide__arrow svg{height:1.8rem;width:1.8rem;fill:var(--primaryColor)}.hero .glide__arrow{border-radius:50%}.hero__center{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;position:relative;max-width:114rem;margin:0 auto;height:100%;padding-top:3rem}.hero__left{padding:0 3rem;-webkit-box-flex:0;-ms-flex:0 0 50%;flex:0 0 50%}.hero__btn{display:inline-block;font-weight:700;font-size:1.4rem;background-color:var(--black);color:var(--primaryColor);cursor:pointer;margin-top:1rem;padding:1.5rem 4rem;border:1px solid var(--black);-webkit-transition:all .3s ease-in-out;transition:all .3s ease-in-out}.hero__btn:focus{outline:0}.hero__left .hero__btn:hover{font-weight:700;background-color:transparent;color:var(--black)}.hero__left h1{margin:1rem 0}.hero__left p{margin-bottom:1rem}.hero__right{-webkit-box-flex:0;-ms-flex:0 0 50%;flex:0 0 50%;position:relative;text-align:center}.hero__right img.banner_03{width:70%}@media only screen and (max-width:999px){.hero__center{-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;text-align:center}.hero__right{top:50%;position:absolute}.hero__left{position:absolute;padding:0 1rem;top:20%}.hero__right img{width:55%}.hero__btn{padding:1.1rem 2.8rem}.hero .glide__arrows{display:none}}@media only screen and (max-width:567px){.hero,.hero .glide__slides{height:60vh}.hero__right{display:none}}.section{padding:3rem 0}.collection{margin:3rem 0}.collection__container{width:100%;padding:0 1.6rem;display:-webkit-box;display:-ms-flexbox;display:flex;height:100%;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between}.collection__box{display:-webkit-box;display:-ms-flexbox;display:flex;-ms-flex-pack:distribute;justify-content:space-around;-webkit-box-align:center;-ms-flex-align:center;align-items:center;padding:1rem;-webkit-box-flex:0;-ms-flex:0 0 48%;flex:0 0 48%;height:30rem;background-color:var(--primaryColor)}.collection__box:not(:last-child){margin-right:1.6rem}.img__container{width:25rem;text-align:center}.collection__box img.collection_01{width:60%}.collection__box img.collection_02{width:75%}.collection__content{-webkit-box-flex:0;-ms-flex:0 0 50%;flex:0 0 50%;height:100%;display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center}.collection__content span{color:var(--black)}.collection__content h1{margin-top:.5rem}.collection__content a:link,.collection__content a:visited{font-weight:700;display:inline-block;padding:1rem 1.4rem;margin-top:1.3rem;border-radius:3rem;border:2px solid var(--secondaryColor);color:var(--primaryColor);background-color:var(--secondaryColor);-webkit-transition:all .3s ease-in-out;transition:all .3s ease-in-out}.collection__content a:hover{background-color:transparent;color:var(--secondaryColor)}@media only screen and (max-width:999px){.collection__container{width:80%;margin:0 auto;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;height:65rem}.collection__box{width:100%;margin:0 auto}.collection__box:not(:last-child){margin:0 0 1.6rem}}@media only screen and (max-width:568px){.collection{margin:0;position:relative}.collection__container{width:100%;height:50rem;text-align:center;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;-ms-flex-pack:distribute;justify-content:space-around}.collection__box{-ms-flex-pack:distribute;justify-content:space-around;height:15rem}.collection__content{-webkit-box-flex:0;-ms-flex:0 0 30%;flex:0 0 30%}.collection__data span{font-size:1.2rem}.collection__data h1{font-size:2rem}}.title__container{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;margin:0 auto 6rem;padding:2rem 0;background-color:var(--primaryColor)}.section__titles:not(:last-child){margin-right:1.5rem}.section__title{display:-webkit-inline-box;display:-ms-inline-flexbox;display:inline-flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;cursor:pointer}.section__title h1{font-size:1.9rem;font-weight:inherit}.section__title:hover .primary__title,.section__title:hover span.dot,.section__title:hover span.dot::before{opacity:1}.section__title .primary__title{opacity:.6;padding-left:.5rem;-webkit-transition:opacity .3s ease-in-out;transition:opacity .3s ease-in-out}span.dot{opacity:.6;padding:.45rem;position:relative;
  border:1px solid var(--black);cursor:pointer;-webkit-transition:opacity .3s ease-in-out;transition:opacity .3s ease-in-out}span.dot::before{content:"";position:absolute;top:0;left:0;right:0;bottom:0;border:1px solid var(--black);background-color:var(--black);margin:1px;opacity:.6}.section__title.active span.dot{opacity:1}.section__title.active span.dot::before{opacity:1}.section__title.active .primary__title{opacity:1}.product{position:relative;text-align:center}.product ul svg{width:1.7rem;height:1.7rem;fill:var(--white)}.product ul{position:absolute;display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;top:35%;left:50%;width:17rem;height:5rem;background-color:rgba(255,255,255,.5);opacity:0;visibility:hidden;-webkit-transform:translate(-50%,-50%) scale(.7);transform:translate(-50%,-50%) scale(.7);-webkit-transition:all .5s ease-in-out;transition:all .5s ease-in-out}.product:hover ul{opacity:1;visibility:visible;-webkit-transform:translate(-50%,-50%) scale(1);transform:translate(-50%,-50%) scale(1)}.product ul li:not(:last-child){margin-right:1.6rem}.product ul a{position:relative;display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;background-color:var(--orange);width:3.5rem;height:3.5rem;cursor:pointer;-webkit-transition:.5s;transition:.5s}.product ul a:hover{background-color:var(--black)}.product ul a::before{content:"";position:absolute;top:-.6rem;left:-.6rem;height:0;width:0;border-top:3px solid var(--orange);border-left:3px solid var(--orange);-webkit-transition:.5s;transition:.5s;opacity:0;z-index:1}.product ul a::after{content:"";position:absolute;bottom:-.6rem;right:-.6rem;width:0;height:0;border-bottom:3px solid var(--orange);border-right:3px solid var(--orange);z-index:1;opacity:0;-webkit-transition:.5s;transition:.5s}.product ul a:hover::before{width:126%;height:126%;border-top:3px solid var(--black);border-left:3px solid var(--black);opacity:1}.product ul a:hover::after{width:126%;height:126%;border-bottom:3px solid var(--black);border-right:3px solid var(--black);opacity:1}@media only screen and (max-width:567px){.title__container{-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column}.section__titles:not(:last-child){margin:0 0 1.3rem}}.product{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;text-align:center;width:25rem}.product__header{height:25rem;padding:.5rem 0;text-align:center}.product__header img{max-width:100%;max-height:100%}.product__footer{padding:1rem 0}.rating svg{width:1.6rem;height:1.6rem;fill:var(--yellow)}.product__footer h3{padding:1rem 0}.product__footer .product__price{padding-bottom:1rem}.product__footer h3{font-size:1.6rem}.product__btn{display:inline-block;font-weight:700;text-transform:uppercase;width:100%;padding:1.4rem 0;border:1px solid var(--black);color:var(--black);cursor:pointer}.product__btn:focus{outline:0}.product__btn:hover{background-color:var(--black);color:var(--primaryColor)}.latest__products .glide__arrow,.related__products .glide__arrow{background-color:transparent;border:1px solid var(--primaryColor);outline:0;border-radius:0;-webkit-box-shadow:0 .25em .5em 0 transparent;box-shadow:0 .25em .5em 0 transparent;top:-7%;left:80%}.latest__products .glide__arrow:hover,.related__products .glide__arrow:hover{background-color:var(--orange);border:1px solid var(--primaryColor)}.latest__products .glide__arrow--left,.related__products .glide__arrow--left{left:75%}.latest__products .glide__arrow--right,.related__products .glide__arrow--right{right:5%}.latest__products .glide__arrow svg,.related__products .glide__arrow svg{width:1.5rem;height:1.5rem;fill:var(--grey)}@media only screen and (max-width:999px){.product__header{height:25rem}.product{width:70%;margin:0 auto}.latest__products .glide__arrow--left,.related__products .glide__arrow--left{left:73%}.latest__products .glide__arrow--right,.related__products .glide__arrow--right{right:7%}}@media only screen and (max-width:768px){.latest__products .glide__arrow--left,.related__products .glide__arrow--left{left:70%}.latest__products .glide__arrow--right,.related__products .glide__arrow--right{right:7%}}@media only screen and (max-width:578px){.product__header{height:20rem}.product__btn:hover{background-color:var(--black);color:var(--primaryColor)}.product__header img{width:20%}.product__footer h3{font-size:1.4rem}.product__btn{width:100%;font-size:1rem;padding:.8rem 0;border:1px solid var(--black)}.product ul a{width:2.7rem;height:2.7rem}.product ul{top:25%;left:50%;width:16rem;height:4rem}.rating svg{width:1.3rem;height:1.3rem}.latest__products .glide__arrow--left,.related__products .glide__arrow--left{left:66%}.latest__products .glide__arrow--right,.related__products .glide__arrow--right{left:85%}}@media only screen and (max-width:460px){.product__header{height:12rem}.product__footer h3{font-size:1.2rem}}.category__center{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:3rem 2rem}@media only screen and (max-width:999px){.category__center{grid-template-columns:1fr 1fr 1fr}}@media only screen and (max-width:568px){.category__center{grid-template-columns:1fr 1fr;gap:1.5rem 1rem}.category__products .product__header{height:10rem}.category__products .product__header img{-o-object-fit:contain;object-fit:contain}}.popup{position:fixed;top:0;left:0;width:100%;height:100vh;background-color:rgba(0,0,0,.3);z-index:9999;-webkit-transition:.3s;transition:.3s;-webkit-transform:scale(1);transform:scale(1)}.popup__content{position:absolute;top:50%;left:50%;width:90%;margin:0 auto;height:55rem;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%);padding:1.6rem;display:table;overflow:hidden;background-color:var(--white)}.popup__close{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;position:absolute;top:2rem;right:2rem;padding:1.5rem;background-color:var(--primaryColor);border-radius:50%;cursor:pointer}.popup__close svg{width:1.7rem;height:1.7rem}.popup__left{display:table-cell;width:50%;height:100%;vertical-align:middle}.popup__right{display:table-cell;width:50%;vertical-align:middle;padding:3rem 5rem}.popup-img__container{width:100%;overflow:hidden}.popup-img__container img.popup__img{display:block;width:60rem;height:45rem;max-width:100%;border-radius:1rem;-o-object-fit:cover;object-fit:cover}.right__content{text-align:center;width:85%;margin:0 auto}.right__content h1{font-size:4rem;color:#000;margin-bottom:1.6rem}.right__content h1 span{color:var(--green)}.right__content p{font-size:1.8rem;color:var(--grey2);margin-bottom:1.6rem}.popup__form{width:100%;padding:2rem 0;text-indent:1rem;margin-bottom:1.6rem;border-radius:3rem;background-color:var(--primaryColor);border:none}.popup__form:focus{outline:0}.right__content a:link,.right__content a:visited{display:inline-block;padding:1.8rem 5rem;border-radius:3rem;font-weight:700;color:var(--white);background-color:var(--black);border:1px solid var(--grey2);-webkit-transition:.3s;transition:.3s}.right__content a:hover{background-color:var(--green);border:1px solid var(--grey2);color:var(--black)}.hide__popup{-webkit-transform:scale(.2);transform:scale(.2);opacity:0;visibility:hidden}.goto-top:link,.goto-top:visited{position:fixed;right:2%;bottom:10%;padding:.8rem 1.4rem;border-radius:1rem;background-color:var(--orange);visibility:hidden;cursor:pointer;-webkit-transition:.3s;transition:.3s;-webkit-animation:bounce 2s ease-in-out infinite;animation:bounce 2s ease-in-out infinite}.show-top:link,.show-top:visited{visibility:visible;z-index:1999}@-webkit-keyframes bounce{0%{-webkit-transform:scale(.5);transform:scale(.5)}50%{-webkit-transform:scale(1.5);transform:scale(1.5)}0%{-webkit-transform:scale(1);transform:scale(1)}}@keyframes bounce{0%{-webkit-transform:scale(.5);transform:scale(.5)}50%{-webkit-transform:scale(1.5);transform:scale(1.5)}0%{-webkit-transform:scale(1);transform:scale(1)}}.goto-top svg{width:1.3rem;height:1.3rem;fill:var(--white)}.goto-top:hover{background-color:var(--black4)}@media only screen and (max-width:1200px){.right__content{width:100%}.right__content h1{font-size:3.5rem;margin-bottom:1.3rem}}@media only screen and (max-width:998px){.popup__right{width:100%}.popup__left{display:none}.right__content h1{font-size:5rem}}@media only screen and (max-width:768px){.right__content h1{font-size:4rem}.right__content p{font-size:1.6rem}.popup__form{width:90%;margin:0 auto;padding:1.8rem 0;margin-bottom:1.5rem}.goto-top:link,.goto-top:visited{right:5%;bottom:5%}}@media only screen and (max-width:568px){.popup__right{padding:0 1.6rem}.popup__content{height:35rem;width:90%;margin:0 auto}.right__content{width:100%}.right__content h1{font-size:3rem}.right__content p{font-size:1.4rem}.popup__form{width:100%;padding:1.5rem 0;margin-bottom:1.3rem}.right__content a:link,.right__content a:visited{padding:1.5rem 3rem}.popup__close{top:1rem;right:1rem;padding:1.3rem}.popup__close svg{width:1.4rem;height:1.4rem}}.facility__section{background-color:var(--primaryColor);padding:6rem 0}.facility__contianer{display:grid;-webkit-box-align:center;-ms-flex-align:center;align-items:center;grid-template-columns:repeat(4,1fr)}.facility-img__container svg{width:3rem;height:3rem;-webkit-transition:1s;transition:1s;-webkit-perspective:4000;perspective:4000}.facility__box{text-align:center}.facility-img__container{position:relative;display:inline-block;line-height:9.5rem;width:8rem;height:8rem;border-radius:50%;border:1.5px solid var(--white);z-index:1;margin-bottom:1.6rem}.facility-img__container::before{content:"";position:absolute;display:inline-block;border-radius:50%;top:0;left:0;right:0;bottom:0;margin:.7rem;background-color:var(--white);z-index:-1}.facility__box:hover svg{-webkit-transform:rotateY(180deg);transform:rotateY(180deg);line-height:9.5rem}@media only screen and (max-width:998px){.facility__contianer{grid-template-columns:1fr 1fr;row-gap:3rem}}@media only screen and (max-width:568px){.facility__contianer{grid-template-columns:1fr}.facility-img__container{width:7rem;height:7rem;line-height:8.5rem}.facility__contianer p{font-size:1.4rem}}.testimonial{position:relative;background:url(images/testimonial.jpg) center/cover no-repeat;height:50rem;padding:5rem 0;z-index:1;text-align:center}.testimonial::before{content:"";position:absolute;width:100%;height:100%;top:0;left:0;background-color:rgba(0,0,0,.9);z-index:-1}.client__image{margin-bottom:3rem}.client__image img{width:7rem;height:7rem;max-width:100%;-o-object-fit:cover;object-fit:cover;border-radius:50%}.testimonial__container{height:100%;padding:1rem}.testimonial__box{width:90%;margin:0 auto;height:100%;color:#ccc}.testimonial__box p{width:70%;margin:0 auto;line-height:2.5rem;font-style:italic;font-size:1.5rem;margin-bottom:3rem}.client__info h3{font-weight:400;font-size:2rem;margin-bottom:1rem}.client__info span{font-size:1.4rem}.testimonial .glide__bullets{bottom:-20%}@media only screen and (max-width:1200px){.testimonial__box{height:100%}.testimonial__box p{width:90%;margin:0 auto;line-height:2.2rem;margin-bottom:3rem}.client__image{margin-bottom:2.5rem}}@media only screen and (max-width:568px){.testimonial{height:100%;padding:4rem 0 5rem;z-index:1;text-align:center}.testimonial__box{height:100%}.testimonial__box p{width:100%;font-size:1.3rem;line-height:2rem;margin-bottom:2rem}.client__image{margin-bottom:1.5rem}.testimonial__box span{margin-bottom:1rem}.testimonial .glide__bullets{bottom:-8%}}.news{padding-bottom:8rem}.new__card{background-color:var(--primaryColor);width:95%;margin:0 auto}.new__card:not(:last-child){margin-right:1rem}.card__footer{padding:3rem 1.4rem}.card__footer h3{font-size:2.5rem;font-weight:600;color:var(--black);margin-bottom:1rem}.card__footer span{display:inline-block;margin-bottom:1rem;color:var(--black2)}.card__footer p{font-size:1.5rem;color:var(--black2);margin-bottom:1.6rem;line-height:2.7rem}.card__footer a:link,.card__footer a:visited{display:inline-block;padding:1.4rem 4rem;border:1px solid var(--black);color:var(--black);-webkit-transition:.3s;transition:.3s}.card__footer a:hover{border:1px solid var(--black);color:var(--white);background-color:var(--black)}.newsletter{padding:6rem 0;border-top:1px solid var(--primaryColor)}.newsletter__content{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between}.newsletter__data h3{font-size:2.4rem;font-weight:inherit;margin-bottom:1rem}.newsletter__data p{font-size:1.5rem;color:var(--black2)}.newsletter__email{font-size:1.4rem;display:inline-block;width:37rem;padding:1.6rem;background-color:var(--primaryColor);border:none;text-indent:1rem}.newsletter__email:focus{outline:0}.newsletter__link:link,.newsletter__link:visited{display:inline-block;padding:1.4rem 3rem;margin-left:-.5rem;background-color:var(--black);color:var(--white);-webkit-transition:.3s;transition:.3s}.newsletter__link:hover{background-color:#000}@media only screen and (max-width:998px){.newsletter{padding:6rem 4rem}.newsletter__content{-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;-webkit-box-align:center;-ms-flex-align:center;align-items:center}.newsletter__email{width:45rem}.newsletter__data{margin-bottom:2rem}}@media only screen and (max-width:768px){.newsletter__content{-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;text-align:center}.newsletter__email{width:45rem;display:block;margin-bottom:1.6rem}}@media only screen and (max-width:568px){.newsletter__email{width:23rem;font-size:1.2rem}.newsletter__data h3{font-size:1.6rem}.newsletter__data p{font-size:1rem}.newsletter__link:link,.newsletter__link:visited{padding:1.2rem 2rem;margin-left:0}}.footer{background-color:var(--black3);padding:6rem 1rem;line-height:3rem}.footer-top__box span svg{width:1.6rem;height:1.6rem;fill:var(--grey3)}.footer-top__box span{margin-right:1rem}.footer__top{display:grid;grid-template-columns:repeat(4,1fr);color:var(--grey3)}.footer-top__box a:link,.footer-top__box a:visited{display:block;color:var(--grey);font-size:1.4rem;-webkit-transition:.6s;transition:.6s}.footer-top__box a:hover{color:var(--orange)}.footer-top__box div{color:var(--grey);font-size:1.4rem}.footer-top__box h3{font-size:1.8rem;font-weight:400;margin-bottom:1rem}@media only screen and (max-width:998px){.footer__top{grid-template-columns:repeat(2,1fr);row-gap:2rem}}@media only screen and (max-width:768px){.footer__top{grid-template-columns:1fr;row-gap:2rem}}.details__container--left,.product-detail__container{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:start;-ms-flex-align:start;align-items:flex-start}.product-detail__container{display:grid;grid-template-columns:repeat(2,1fr);padding:2.5rem 0;margin:0 auto}.product-detail__left{-webkit-box-flex:0;-ms-flex:0 0 50%;flex:0 0 50%;margin-right:2rem}.product-detail__right{-webkit-box-flex:0;-ms-flex:0 0 50%;flex:0 0 50%}.product-detail__container--left img{width:100%;-o-object-fit:cover;object-fit:cover}.product__pictures{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column}.pictures__container{padding:1rem;border:1px solid var(--primaryColor);border-right-color:transparent;cursor:pointer;width:6.2rem;-webkit-transition:.3s;transition:.3s}.pictures__container:not(:last-child){border-bottom-color:transparent}.pictures__container:hover{border:1px solid var(--orange)}.pictures__container img{-webkit-transition:.3s;transition:.3s}.pictures__container:hover img{scale:1.1}.product__picture{width:100%;border:1px solid var(--primaryColor);padding:1rem;display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center}.product-details__btn{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;margin-top:2rem}.product-details__btn a{-webkit-box-flex:0;-ms-flex:0 0 47%;flex:0 0 47%;display:inline-block;padding:1.6rem 3rem;text-align:center;color:var(--black);border:1px solid var(--black)}.product-details__btn svg{width:1.9rem;height:1.9rem;-webkit-transition:.3s;transition:.3s}.product-details__btn .add,.product-details__btn .buy{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center;-webkit-transition:.3s;transition:.3s}.product-details__btn .add span,.product-details__btn .buy span{margin-right:1rem}.product-details__btn .add:hover,.product-details__btn .buy:hover{background-color:var(--black);color:var(--primaryColor)}.product-details__btn .add:hover svg,.product-details__btn .buy:hover svg{fill:var(--primaryColor)}.product-detail__content{width:90%;margin:0 auto}.product-detail__content h3{font-size:2.5rem;margin-bottom:1.3rem}.price{margin-bottom:1rem}.new__price{font-size:2rem;color:var(--orange)}.product-detail__content .product__review{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;margin-bottom:1.6rem;padding-bottom:1.6rem;border-bottom:.5px solid var(--primaryColor)}.rating{margin-right:1rem}.product__review a:link,.product__review a:visited{color:var(--black)}.product-detail__content p{font-size:1.4rem;color:var(--black2);line-height:2.4rem;margin-bottom:1.6rem}.product__info .select{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;margin-bottom:1.6rem}.select .select-box{background:0 0;width:18rem;border:none;padding:.5rem 1rem;border-bottom:1px solid var(--primaryColor)}.select .select-box:focus{outline:0}.select__option label{font-size:1.4rem;color:var(--black3);display:inline-block;padding-bottom:1rem}.input-counter{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center}.input-counter div{display:-webkit-box;display:-ms-flexbox;display:flex}.input-counter li span{font-size:1.4rem;color:var(--black3);margin-right:1rem}.minus-btn,.plus-btn{display:inline-block;border:1px solid var(--primaryColor);padding:.8rem 1rem;margin-right:0;cursor:pointer}.plus-btn{border-left-color:transparent}.minus-btn{border-right-color:transparent}.counter-btn{width:7rem;padding:1rem 0;text-align:center;border:1px solid var(--primaryColor)}.input-counter svg{width:1.8rem;height:1.8rem;fill:var(--grey3)}.product__info li{margin-bottom:1.6rem}.product__info .in-stock{color:var(--green)}.product__info li a{font-size:1.4rem;color:var(--black2)}.product-info__btn span svg{width:1.8rem;height:1.8rem}.product-info__btn{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center}.product-info__btn a{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-align:center;-ms-flex-align:center;align-items:center;font-size:1.2rem;color:var(--black2)}.product-info__btn a:not(:last-child){margin-right:1rem}.detail__content{position:relative;height:55rem}.detail__content .content{position:absolute;-webkit-transform:translate(0,25vh);transform:translate(0,25vh);-webkit-transition:all .6s ease-in-out;transition:all .6s ease-in-out;opacity:0;visibility:hidden;z-index:555}.detail__content .content.active{-webkit-transform:translate(0,0);transform:translate(0,0);opacity:1;visibility:visible}#shipping h3,#shipping p{color:var(--grey2)}#description p,#shipping p{padding:1.6rem 0;line-height:2.8rem}#reviews{font-size:3rem;font-weight:500;color:var(--grey2);border-bottom:1px solid var(--primaryColor)}#description h2,#description li,#description p{color:var(--grey2)}#description h2{font-weight:500;padding:1rem 0}#description li{line-height:3rem;color:vaf}#description ol{padding-left:1.6rem}@media only screen and (max-width:1200px){.detail__content{height:65rem}}@media only screen and (max-width:998px){.detail__content{height:70rem}}@media only screen and (max-width:768px){.detail__content{height:85rem}}@media only screen and (max-width:568px){.detail__content{height:110rem}}@media only screen and (max-width:450px){.detail__content{height:130rem}}@media only screen and (max-width:340px){.detail__content{height:160rem}}@media only screen and (max-width:998px){.select .select-box{width:15rem}.select__option label{display:block}.product-info__btn{-ms-flex-wrap:wrap;flex-wrap:wrap}.product-details__btn a{padding:1rem 2.5rem;font-size:1.4rem}.picture__container{width:90%}}@media only screen and (max-width:768px){.details__container--left{-webkit-box-orient:vertical;-webkit-box-direction:reverse;-ms-flex-direction:column-reverse;flex-direction:column-reverse;text-align:center}.product__pictures{margin-top:2rem;-webkit-box-orient:horizontal;-webkit-box-direction:normal;-ms-flex-direction:row;flex-direction:row;-webkit-box-pack:center;-ms-flex-pack:center;justify-content:center}.pictures__container{width:50%;border-right-color:var(--primaryColor)}.pictures__container:not(:last-child){border-bottom-color:var(--primaryColor)}.product-detail__container{grid-template-columns:1fr;row-gap:5rem}.product__info .select{-webkit-box-align:start;-ms-flex-align:start;align-items:flex-start;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column}.select .select-box{display:block;width:20rem}}@media only screen and (max-width:568px){.select .select-box{width:15rem}.input-counter{-webkit-box-align:start;-ms-flex-align:start;align-items:flex-start;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column}.input-counter div{margin-top:1rem}}@media only screen and (max-width:400px){.product-details__btn a{padding:.7rem 2rem;font-size:1.2rem}.product-details__btn .add span,.product-details__btn .buy span{margin-right:0}.product__review .rating svg{width:1.4rem;height:1.4rem}}.cart__area{padding-bottom:5rem}.product__thumbnail img{width:10rem}.remove__cart-item svg{width:1.6rem;height:1.6rem;fill:var(--grey2);-webkit-transition:all .3s ease-in-out;transition:all .3s ease-in-out}.cart__table{margin-bottom:4rem}.cart__table .table{border-collapse:collapse;width:100%}.cart__table .table th{font-weight:500;font-style:2rem;text-align:left;padding:1.8rem 0}.cart__table .table td{vertical-align:middle;padding:1.8rem 0;border-bottom:1px solid var(--primaryColor)}.cart__table .table thead{border-bottom:1px solid var(--primaryColor)}.product__name a:link,.product__name a:visited{font-size:1.5rem;color:var(--black2)}.product__name small{color:var(--grey);margin-top:1.6rem}.product__subtotal .price{display:inline}.product__price .price .new__price,.product__subtotal .price .new__price{font-size:1.6rem}.remove__cart-item{margin-left:1rem}.remove__cart-item:hover svg{fill:var(--orange)}.cart-btns{display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;border-bottom:1px solid var(--primaryColor);padding-bottom:4rem;margin:3rem 0}.continue__shopping a:link,.continue__shopping a:visited{font-size:1.5rem;padding:1.2rem 3rem;color:var(--black);text-transform:uppercase;border:1px solid var(--black);-webkit-transition:all .4s ease-in-out;transition:all .4s ease-in-out}.continue__shopping a:hover{background-color:var(--black);color:var(--white);border:1px solid var(--black)}.cart__totals{width:60rem;margin:5rem auto 0 auto;color:var(--black5);padding:4rem 5rem;background-color:rgba(255,255,255,.8);-webkit-box-shadow:0 2px 30px 10px rgba(0,0,0,.09);box-shadow:0 2px 30px 10px rgba(0,0,0,.09);border-radius:.5rem}.cart__totals h3{font-weight:500;font-size:1.8rem;margin-bottom:1.6rem}.cart__totals .new__price{font-size:1.5rem}.cart__totals ul{margin-bottom:2.5rem}.cart__totals li{border:1px solid var(--primaryColor);padding:1.4rem .5rem;position:relative}.cart__totals li:not(:last-child){border-bottom-color:transparent}.cart__totals li span{position:absolute;right:1rem}.cart__totals a:link,.cart__totals a:visited{font-size:1.5rem;padding:1.2rem 3rem;color:var(--black);text-transform:uppercase;border:1px solid var(--black);-webkit-transition:all .4s ease-in-out;transition:all .4s ease-in-out}.cart__totals a:hover{background-color:var(--black);color:var(--white);border:1px solid var(--black)}@media only screen and (max-width:1200px){.minus-btn,.plus-btn{padding:.6rem .8rem;margin-right:0}.counter-btn{width:4rem;padding:1rem 0}.input-counter svg{width:1.5rem;height:1.5rem}}


/*==========Social Icons====*/

#social-icons{
 height: 150px;
   background:#fff;
    text-align: center;
   /* clip-path: polygon(0 0, 100% 0, 100% 100%, 0 40%);*/
    padding: 50px 0 50px 0;
}
#social-icons a{
    display: inline-block;
    padding: 5px 10px;
    margin: 0 5px;
    font-size: 40px;
    border-radius:5px;
    transition: transform 2s ease, color 2s ease;
}
#social-icons a:hover{
    transform: translateY(-20px);
}
.facebook{
    color: #3b5998;
}
.twitter{
  color:  #38A1F3;
}
.instagram{
 color:   #e1306c;
}
.plus{
    color:#db4a39;
}
/*====end of Social Icons======*/
  
  </style>
