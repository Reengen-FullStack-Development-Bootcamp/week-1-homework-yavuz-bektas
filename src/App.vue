<template>
  <v-app id="inspire">
    <v-app-bar class="pink lighten-4" app color="white" flat>
      <v-container class="py-0 fill-height">
        <p>Fake</p>
        <v-avatar class="mr-10" size="32"
          ><img src="https://cdn.dsmcdn.com/web/logo/ty-logo.svg"
        /></v-avatar>

        <div class="text-center">
          <v-menu offset-y>
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="purple" dark v-bind="attrs" v-on="on">
                <v-icon>mdi-cart </v-icon>
                SEPET
                {{ checkAllItems }}
              </v-btn>
            </template>
            <v-list v-if="checkAllItems > 0" color="purple">
              <!-- <v-list-item v-for="(item, index) in ShopCard" :key="index">
                <v-list-item-title class="text-white">{{
                  item.title
                }}</v-list-item-title>
              </v-list-item> -->
              <v-list-item v-for="(i, index) in ShopCard" :key="i.id">
                <v-list-item-title class="text-white">
                  <v-avatar color="indigo" size="36">
                    <span class="white--text text-h5">{{ i.count }}</span>
                  </v-avatar>
                  {{ i.title }}
                </v-list-item-title>
                <div>
                  <v-chip class="ma-2" color="indigo" text-color="white">
                    <v-avatar left>
                      <v-icon>mdi-currency-usd</v-icon>
                    </v-avatar>
                    <h3>{{ i.price * i.count }}</h3>
                  </v-chip>
                </div>

                <v-btn @click="decrease(i, index)" color="warning">
                  -
                </v-btn>
                <v-btn @click="increase(i, index)" color="success">
                  +
                </v-btn>
                <v-btn @click="deleteall(i, index)" color="error">
                  Sil
                </v-btn>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
        <v-spacer></v-spacer>
      </v-container>
    </v-app-bar>

    <v-main class="pink lighten-3">
      <v-container>
        <v-row>
          <v-col v-for="(product, i) in Products" :key="i">
            <Card
              @AddData="IncomingData"
              :Products="product"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({}),
};
</script>

<script>
import Card from "./components/card";
export default {
  data: () => ({
    items: [
      { title: "Click Me" },
      { title: "Click Me" },
      { title: "Click Me" },
      { title: "Click Me 2" },
    ],
    Products: [
      {
        id: "15",
        title: "Nike 907257-602 Star Runner (Gs) Unısex Yürüyüş Koşu Ayakkabı",
        summary: "Bu ürün iste-shop tarafından gönderilecektir.",
        category: "Sneaker",
        price: "300",
        secondPrice: "300",
        star: 5,
        sizes: "35,36,37,38",
        img:
          "https://cdn.dsmcdn.com/ty64/product/media/images/20210129/18/58448728/61096485/1/1_org_zoom.jpg",
        cardColor: "pink",
      },
      {
        id: "16",
        title: "Nike Air Force 1 Gtx Boot Ct2815-200 Erkek Bot CT2815-200",
        summary: "Bu ürün PashaGiyim tarafından gönderilecektir.",
        category: "Sneaker",
        price: "2000",
        star: 3.5,
        sizes: "35,36,37,38",
        img:
          "https://cdn.dsmcdn.com/ty153/product/media/images/20210806/19/116360207/223164567/1/1_org_zoom.jpg",
        cardColor: "yellow",
      },
      {
        id: "17",
        title: "Bartrobe Kadın Mavi Bağcıklı Sneaker Aic270",
        summary: "Bu ürün Ayakkabıhobim tarafından gönderilecektir.",
        category: "Spor",
        price: "123",
        star: 4.5,
        sizes: "35,36,37,38",
        img:
          "https://cdn.dsmcdn.com/ty109/product/media/images/20210503/17/85222592/170268805/1/1_org_zoom.jpg",
        cardColor: "blue",
      },
      {
        id: "18",
        title:
          'Nike Aır Max 97 (gs) "have A Nıke Day" Spor Ayakkabı 923288-300',
        summary: "Bu ürün FENOMENSPOR tarafından gönderilecektir.",
        category: "Spor",
        price: "870",
        star: 2.5,
        sizes: "35,36,37,38",
        img:
          "https://cdn.dsmcdn.com/ty66/product/media/images/20210319/13/73533292/81633649/1/1_org_zoom.jpg",
        cardColor: "green",
      },
    ],
    ShopCard: [],
  }),
  components: {
    Card,
  },
  methods: {
    IncomingData(value) {
      // this.ShopCard.push(value);
      let dups = this.ShopCard.filter((el) => el.id === value.id).length;
      if (dups) {
        // this.ShopCard.push({ ...value, count: dups + 1 });
        let index = this.ShopCard.findIndex((el) => el.id === value.id);
        this.ShopCard[index].count++;
      } else {
        this.ShopCard.push({ ...value, count: 1 });
      }
    },
    increase(value) {
      let index = this.ShopCard.findIndex((el) => el.id === value.id);
      this.ShopCard[index].count++;
    },
    decrease(value, index) {
      if (this.ShopCard[index].count > 1) {
        let index = this.ShopCard.findIndex((el) => el.id === value.id);
        this.ShopCard[index].count--;
      } else {
        this.ShopCard.splice(index, 1);
      }
    },
    deleteall(value, index) {
      this.ShopCard.splice(index, 1);
    },
  },
  computed: {
    checkAllItems() {
      let qty = 0;
      for (let i = 0; i < this.ShopCard.length; i++) {
        qty += this.ShopCard[i].count;
      }
      return qty;
    },
  },
};
</script>
