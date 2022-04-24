<template>
  <div class="wrapper">
    <div class="product-image-wrapper">
      <ProductImage :mainImage="changeMainImage" />
      <div>
        <Thumbnailler
          :variant="filteredProduct"
          @image="selectedImage($event)"
        />
      </div>
    </div>
    <div class="product-info-wrapper">
      <div>
        <ProductHeader :productTitle="productTitle" />
        <ProductEvaluation />
      </div>
      <ProductPrice />
      <div v-for="item in selectableAttributes" :key="item.name">
        <ProductFeature
          :item="item"
          :selectedColor="selectedColor"
          :selectedSize="selectedSize"
          @value="handleSize($event)"
          :attributes="attributes"
        />
      </div>
      <div class="total-unit-wrapper">
        <div class="total-price-wrapper">
          <label>{{ unitPriceTitle }} (Adet)</label>:
          <div
            v-for="(barem, i) in baremList"
            :key="i"
            class="barem"
            :style="
              barem.isSelected
                ? { background: '#f6e9c1' }
                : { background: 'none' }
            "
          >
            <ProductTotalPrice :barem="barem" :unit="Number(unit)" />
          </div>
        </div>
        <div class="unit-wrapper">
          <label for="unit">Adet</label>
          <input
            type="number"
            id="unit"
            v-model="unit"
            @change="getUnitInput"
            min="0"
          />
        </div>
      </div>
      <div class="total-amount">
        <div><label class="total">Toplam</label></div>
        :
        <div class="total-amount-info-wrapper">
          <div class="total">{{ totalAmount }} TL</div>
          <div class="content">
            <div>
              <div>Kargo Ücreti:</div>
              <span class="text">Alıcı Öder</span>
            </div>
            <div>
              <button
                @click="handleAddCart"
                :class="[isCompleted ? 'button' : 'button-disabled']"
              >
                Sepete Ekle
              </button>
              <div class="text">Ödeme Seçenekleri</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProductJson from "../product-data.json";
import ProductHeader from "./ProductHeader.vue";
import ProductImage from "./ProductImage.vue";
import ProductEvaluation from "./ProductEvaluation.vue";
import ProductPrice from "./ProductPrice.vue";
import ProductFeature from "./ProductFeature.vue";
import ProductTotalPrice from "./ProductTotalPrice.vue";
import Thumbnailler from "./Thumbnailler.vue";
export default {
  name: "Product",
  props: {},
  components: {
    ProductHeader,
    ProductImage,
    ProductEvaluation,
    ProductPrice,
    ProductFeature,
    ProductTotalPrice,
    Thumbnailler,
  },
  data() {
    return {
      product: {},
      productTitle: "",
      selectableAttributes: [],
      baremList: [],
      unitPriceTitle: "Toptan Fiyat",
      selectedColor: "Siyah",
      selectedSize: "L",
      images: [],
      mainImage: "",
      unit: 0,
      isCompleted: false,
      totalAmount: 0.0,
      selectedId: "",
      attributes: [],
    };
  },
  created() {
    this.fetchProduct();
  },
  computed: {
    filteredProduct() {
      let product = this.productVariants.map((item) => {
        if (
          item.attributes[0].value == this.selectedSize &&
          item.attributes[1].value == this.selectedColor
        ) {
          this.mainImage = item.images[0];
          return item;
        }
      });
      product = product.filter((item) => item != undefined);
      return product;
    },
    changeMainImage() {
      return this.mainImage;
    },
  },
  methods: {
    fetchProduct() {
      this.product = ProductJson;
      this.product.productVariants.forEach((item) => {
        const attributeItem = {
          name: item.attributes[0].value,
          value: item.attributes[1].value,
        };
        this.attributes.push(attributeItem);
      });

      this.productTitle = this.product.productTitle;
      this.selectableAttributes = this.product.selectableAttributes;

      this.baremList = this.product.baremList;
      this.productVariants = this.product.productVariants;

      this.productVariants.forEach((item) => {
        if (
          item.attributes[0].value == this.selectedSize &&
          item.attributes[1].value == this.selectedColor
        ) {
          this.mainImage = item.images[0];
        }
      });
      this.calculateUnit();
    },
    calculateUnit() {
      this.baremList.forEach((item) => {
        if (
          item.maximumQuantity >= this.unit &&
          item.minimumQuantity <= this.unit
        ) {
          this.isCompleted = true;
          item.isSelected = true;
          this.totalAmount = (this.unit * item.price).toFixed(2);
        } else {
          item.isSelected = false;
        }
      });
    },
    handleSize(val) {
      if (val == "Siyah" || val == "Lacivert") {
        this.selectedColor = val;
      } else {
        this.selectedSize = val;
      }
    },
    selectedImage(image) {
      this.mainImage = image;
    },
    handleAddCart() {
      const barem = this.baremList.filter((item) => item.isSelected == true);
      console.log("Selected Product id =>", this.filteredProduct[0].id);
      console.log(
        "Selected Product Barem =>",
        `${barem[0].minimumQuantity}-${barem[0].maximumQuantity}`
      );
    },
    getUnitInput() {
      this.calculateUnit();
    },
  },
};
</script>

<style>
.wrapper {
  display: flex;
}
.product-image-wrapper {
  flex: 1;
}
.product-info-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  flex: 1;
  height: 39rem;
}
.total-price-wrapper {
  display: flex;
  align-items: center;
  gap: 2rem;
  height: 7rem;
}
.total-unit-wrapper {
  background: #f4f4f4;
  width: 34rem;
}
.total-price-wrapper > label {
  width: 6rem;
}
.total-amount {
  display: flex;
  gap: 3rem;
}

.button {
  color: #fff;
  background: #ffc40a;
  padding: 1rem;
  border-radius: 5px;
  border: none;
  font-size: 1rem;
  text-transform: uppercase;
  font-weight: 600;
  cursor: pointer;
}
.button-disabled {
  border: none;
  background-color: #cccccc;
  color: #fff;
  padding: 1rem;
  border-radius: 5px;
  font-size: 1rem;
  text-transform: uppercase;
  font-weight: 600;
  cursor: no-drop;
}
.total-amount-info-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: 1rem;
}
.content {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.content > div {
  display: flex;
  align-items: center;
  gap: 1rem;
}
.total {
  font-size: 1.4rem;
  font-weight: 600;
}
.text {
  color: #3d98d8;
}
.barem {
  padding: 0.4rem;
}
.unit-wrapper {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 7rem;
  width: 34rem;
  padding: 1rem;
}
.unit-wrapper > input {
  width: 5rem;
  padding: 0.4rem;
}
</style>
