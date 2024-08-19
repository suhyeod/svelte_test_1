<script>
  import Slider from "./slider.svelte";
    let cart = [];
    function addToCart(productId) {
        cart = [
            ...cart,
            productId
        ];
    }
    let relatedProducts = [
        {
            id: 'react-book',
            name: 'React-Book',
            price: 30000
        }, {
            id: 'vue-book',
            name: 'Vue Book',
            price: 30000
        }, {
            id: 'angular-book',
            name: 'Angular-Book',
            price: 30000
        }
    ];
    let product = {
        id: 'svelte-book',
        name: 'Svelte-Book',
        price: 30000,
        image:[
          '/svelte-book-frist-tutorial/src/img/img_1.jpeg',
          '/svelte-book-frist-tutorial/src/img/img_2.jpeg',
          '/svelte-book-frist-tutorial/src/img/img_3.jpg',
        ],
    };
    let sliderCenterInedx = 0;
    let sliderLeftIndex = product.image.length -1;
    let sliderRightIndex = 1;
    function sliderMoveLeft(){
      const length = product.image.length;
      sliderCenterInedx = (sliderCenterInedx - 1 + length) % length;
      sliderLeftIndex = (sliderCenterInedx - 1 + length) % length;
      sliderRightIndex = (sliderCenterInedx +1 ) % length;
    }
    function sliderMoveRight(){
      const length = product.image.length;
      sliderCenterInedx = (sliderCenterInedx + 1) % length;
      sliderLeftIndex = (sliderCenterInedx -1 + length) % length;
      sliderRightIndex = (sliderCenterInedx + 1) % length;
    }
</script>
<header class="header">
    <a href="/" class="header-title">Svelte Site</a>
    <nav>
        <ul class="header-links">
            <li>안녕하세요 게스트님</li>
            <li>
                <a href="/cart">장바구니</a>
            </li>
        </ul>
    </nav>
</header>

<article class="product">
    <div class="product-main">
        <div class="image-container">
            <div class="slider">
              <img src="{product.image[sliderLeftIndex]}" alt="sliderImage(left)" class="slider-item left">
              <img src="{product.image[sliderCenterInedx]}" alt="sliderImag" class="slider-item">
              <img src="{product.image[sliderRightIndex]}" alt="sliderImage(right)" class="slider-item right">
            </div>
            <button class="slider-left-button" on:click={sliderMoveLeft}>
              -Prev-
            </button>
            <button class="slider-right-button" on:click={sliderMoveRight}>
              -Next-
            </button>
        </div>
        <div>
            <h2>
                {product.name}
            </h2>
            <dl style="display: flex;">
                <dt>금액</dt>
                <dd>{product.price}</dd>
            </dl>
            <div>
                {#if !cart.includes('svelte-book')}
                    <button on:click={()=> addToCart('svelte-book')}>장바구니 담기</button>
                {:else}
                    <button disabled>장바구니 담기 완료</button>
                {/if}
            </div>
        </div>
    </div>
    <footer>
        <h3>관련상품</h3>
        <ul>
            {#each relatedProducts as product}
                <li>
                    <a href="/products/{product.id}">
                        {product.name}
                    </a>
                    {product.price}원
                </li>
            {/each}
        </ul>
    </footer>
</article>
<style>
    :global(body) {
        margin: 0;
        background-color: #eee;
        padding: 0;
    }
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0 auto;
        background-color: #fff;
        padding: 0 15px;
        width: 100%;
        max-width: 800px;
        height: 50px;
    }
    .header-title {
        font-weight: bold;
    }
    .header-links {
        display: flex;
        gap: 10px;
        margin: 0;
        padding: 0;
        list-style: none;
    }
    .product {
        margin: 0 auto;
        background-color: #fff;
        padding: 15px;
        width: 100%;
        max-width: 800px;
    }
    .product-main{
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
    }
    .image-container {
        width: 100%;
        max-width: 400px;
        overflow: hidden;
    }
    .image-container img {
        width: 400px;
    }
    .slider {
      position: relative;
      width: 80%;
      margin: 0 10%;
    }
    .slider-item{
      width: 100%;
    }
    .slider-item.left{
      position: absolute;
      top: 0;
      right: 100%;
    }
    .slider-item.right{
      position: absolute;
      top: 0;
      left: 100%;
    }
    .slider-left-button {
      position: absolute;
      top: 50%;
      right: 100%;
    }
    .slider-right-button{
      position: absolute;
      top: 50%;
      left: 100%;
    }
</style>