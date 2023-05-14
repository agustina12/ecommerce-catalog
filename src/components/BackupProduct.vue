<template>
  <div class="product">
    <div
      :class="isSelectedCategoryMen ? 'bg-men' : 'bg-women'"
      v-if="dataFormApi">
      <!-- ini warna background-->
      <div class="bg-pettern">
        <div class="container">
          <div class="row">
            <div class="col-5">
              <div class="img-product">
                <img :src="dataFormApi.image" alt="img_product" />
              </div>
            </div>
            <div class="col-7">
              <div class="text-product">
                <!-- ini warna text-->
                <h1>{{ dataFormApi.title }}</h1>
                <div class="sub-text">
                  <p>{{ dataFormApi.category }}</p>
                  <div class="ratings">
                    <p style="margin-right: 3px">
                      {{ dataFormApi?.rating?.rate }}/5
                    </p>
                    <div class="group-rounded">
                      <span class="dot"></span>
                      <span class="dot"></span>
                      <span class="dot"></span>
                      <span class="dot"></span>
                      <span class="dot"></span>
                    </div>
                  </div>
                </div>
                <hr />
                <div class="product-description">
                  <p>
                    {{ dataFormApi.description }}
                  </p>
                </div>
                <hr />
                <p class="price">{{ dataFormApi.price }}</p>
                <div class="button-group">
                  <button class="buy_now">Buy Now</button>
                  <button class="next_product" @click="fakestoreAPI()">
                    Next Product
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="bg-non">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <div class="no-product">
                <p>This product is unavailable to show</p>
                <button class="next_product" @click="fakestoreAPI()">
                  Next Product
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BackupProduct",
  data: function () {
    return {
      isActive: true,
      dataFormApi: {},
      currentId: 0,
      isSelectedCategoryMen: false,
    };
  },
  methods: {
    async fakestoreAPI() {
      if (this.currentId == 20) {
        this.currentId = 1;
      } else {
        this.currentId = this.currentId + 1;
      }
      const api = await fetch(
        `https://fakestoreapi.com/products/${this.currentId}`
      );
      const data = await api.json();
      if (
        data.category == "men's clothing" ||
        data.category == "women's clothing"
      ) {
        this.dataFormApi = data;
        this.isSelectedCategoryMen = data.category == "men's clothing";
      } else {
        this.dataFormApi = null;
      }
      console.log(this.dataFormApi);
    },
  },
  mounted() {
    this.fakestoreAPI();
    // const api = await fetch("https://fakestoreapi.com/products/1");
    // const data = await api.json();
    // this.dataFormApi = data;
  },
};
</script>

<style scoped>
/* .men-product .bg-men {
  background-color: var(--color-background-men);
  background-image: url("../assets/images/bg-pattern.svg");
  height: 25rem;
} */
.product .bg-men {
  background-color: var(--color-background-men);
  background-image: url("../assets/images/bg-pattern.svg");
  height: 25rem;
}
.bg-men {
  background-color: var(--color-background-men);
  background-image: url("../assets/images/bg-pattern.svg");
  height: 25rem;
}

.bg-women {
  background-color: var(--color-background-women);
  background-image: url("../assets/images/bg-pattern.svg");
  height: 25rem;
}
.bg-non {
  background-color: var(--color-background-available);
  height: 25rem;
}
.men-product h1 {
  color: var(--color-text);
}
.img-product img {
  width: 100%;
}

.product .container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding-top: 5rem;
}

.row {
  background-color: var(--color-background);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding: 3rem;
  width: 80%;
  height: 50%;
  display: flex;
}

.col-5 {
  width: 30%;
  margin-right: 2rem;
}
.col-7 {
  width: 70%;
}

.col-7 .text-product h1 {
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
  color: var(--color-text-men);
  margin: -0.7rem 0 1rem 0;
}

.sub-text {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 0 1rem 0;
}

.sub-text p {
  font-weight: 400;
  font-size: 18px;
  line-height: 22px;
  color: var(--color-text-sub);
}

.ratings {
  display: flex;
}

.group-rounded .dot {
  border-radius: 50%;
  height: 16px;
  width: 16px;
  background-color: var(--color-rounded-men);
  display: inline-block;
  margin-right: 1px;
}

hr {
  border: 1px solid var(--color-border);
}

.product-description p {
  margin: 2rem 0 3rem 0;
  font-weight: 400;
  font-size: 18px;
  line-height: 24px;
  color: var(--color-text);
}

.price {
  color: var(--color-text-men);
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
  margin: 1rem 0 1rem 0;
}

.button-group {
  display: flex;
  column-gap: 0.6rem;
}

.button-group button {
  font-weight: 600;
  font-size: 18px;
  line-height: 24px;
  width: 50%;
  height: 2.6rem;
  border-radius: 4px;
}

.button-group button:hover {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.button-group .buy_now {
  background-color: var(--color-button-men);
  border: var(--color-button-men);
  color: var(--color-text-light);
}

.button-group .next_product {
  border-radius: 4px;
  background: var(--color-background);
  border: 2px solid var(--color-button-men);
  color: var(--color-button-men);
}

/* bg-women */

.bg-women .col-7 .text-product h1 {
  color: var(--color-text-women);
}

.bg-women .group-rounded .dot {
  border-radius: 50%;
  height: 16px;
  width: 16px;
  background-color: var(--color-rounded-women);
  display: inline-block;
  margin-right: 1px;
}

.bg-women .price {
  color: var(--color-text-women);
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
  margin: 1rem 0 1rem 0;
}

.bg-women .button-group .buy_now {
  background-color: var(--color-button-women);
  border: var(--color-button-women);
  color: var(--color-text-light);
}

.bg-women .button-group .next_product {
  border-radius: 4px;
  background: var(--color-background);
  border: 2px solid var(--color-button-women);
  color: var(--color-button-women);
}

/* end bg-women */

/* bg-non */
.bg-non .row .col-12 {
  background-image: url("../assets/images/sad-face.svg");
  height: 25rem;
  width: 100%;
  background-size: cover;
  background-repeat: no-repeat;
}

.bg-non .row .no-product {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 10rem;
}
.bg-non .row .no-product p {
  margin: 0 0 2rem 0;
  font-weight: 400;
  font-size: 20px;
  line-height: 24px;
  color: var(--color-text);
}
.bg-non .row .no-product button {
  font-weight: 600;
  font-size: 18px;
  line-height: 24px;
  width: 50%;
  height: 2.6rem;
  border-radius: 4px;
}
.bg-non .row .no-product button:hover {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
.bg-non .row .no-product button {
  border-radius: 4px;
  background: var(--color-background);
  border: 2px solid var(--color-border-available);
  color: var(--color-border-available);
}
</style>
