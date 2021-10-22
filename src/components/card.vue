<template>
  <v-card
    :loading="loading"
    :class="Products.cardColor"
    max-width="374"
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      :src="Products.img"
    ></v-img>

    <v-card-title class="dark--text">{{Products.title}}</v-card-title>

    <v-card-text>
        <v-chip
      class="ma-2"
      color="green darken-4"
      text-color="white"
    >
       <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :value=Products.star
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        ></v-rating>

        <div class="grey--text ms-4">
         {{Products.star}}
        </div>
      </v-row>
     
    </v-chip>

     <div>
    <v-chip
      class="ma-2"
      color="indigo"
      text-color="white"
    >
      <v-avatar left>
        <v-icon>mdi-currency-usd</v-icon>
      </v-avatar>
      {{Products.price * priceCarp}}
    </v-chip>
    </div>

      <div>{{Products.summary}}.</div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-title>Ayakkabı Numarası</v-card-title>

    <v-card-text>
      <v-chip-group
        v-model="selection"
        active-class="deep-purple accent-4 white--text"
        column
      >
        <v-chip @click="changeSize(2)">37</v-chip>

        <v-chip @click="changeSize(3)">38</v-chip>

        <v-chip @click="changeSize(4)">39</v-chip>

        <v-chip @click="changeSize(5)">40</v-chip>
      </v-chip-group>
    </v-card-text>


    <v-card-actions>
      <v-btn
        color="black"
        text
        @click="AddData"
      >
      <v-icon>mdi-plus-thick</v-icon>
        Sepete Ekle
      </v-btn>
    </v-card-actions>

    <v-snackbar
      v-model="snackbar"
      :color="Products.cardColor"
    >
      <strong>{{ Products.title }} </strong>isimli ürün sepete eklendi

    </v-snackbar>

  </v-card>
</template>

<script>
  export default {
    props:['Products'],
    data: () => ({
      loading: false,
      selection: 1,
      snackbar: false,
      priceCarp : 1
    }),

    methods: {
      AddData() {
        this.loading = true
         this.$emit("AddData", this.Products);
        setTimeout(() => (this.loading = false), 2000)
        this.snackbar = true
        setTimeout(() => {
            this.snackbar = false
        }, 2000);
      },
      changeSize(value){
        this.$emit("newSize",value)
        this.priceCarp = value
      }
    },
  }
</script>