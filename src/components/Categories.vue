<template>
<div class="py-4">
  <h2 align='center' class="pa-3">Top Categories</h2>
  <v-sheet class="d-flex justify-space-around">
    <v-slide-group :show-arrows="$vuetify.breakpoint.mdAndUp" class="pa-2">
      <v-slide-item v-for="category in categories.slice(0, 8)" :key="category.id" class="mx-2 rounded" >
        <router-link :to="`/categories/${category.id}`">
          <v-card align='center' width="100" height="100" elevation="0">
            <v-img 
                class="rounded-circle border"
                :src="$staticUrl+'/product_images/'+category.subCatImage" 
                width="100px"
                height="100">
            </v-img>
            <p height='50' style="color:red; font-family:courier;" class='rounded naming-text px-1'><strong>{{category.name}}</strong></p>
          </v-card>
        </router-link>
      </v-slide-item>
    </v-slide-group>
  </v-sheet>
  <div align='center'>
    <router-link class="my-auto px-1" style='font-weight:bold' to='/categories'>More..</router-link>
  </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      categories: []
    }
  },
  created () {
    this.getCategories();  
  },
  methods: {
    getCategories() {
      this.$http.get(`${this.$apiUrl}/fetch_all_subcats?platform=web`)
      .then((response) => {
        this.categories = response.data
        this.$store.state.categories = this.categories
      });
    },
  },
}
</script>

<style>
  .border{
    border: 1px solid #dddddd;
  }
  .naming-text {
    position:absolute; bottom:0; right:0; background-color:rgb(255, 255, 0); color:black; border:1px solid black; height:1.5rem;
    font-size: .8rem;
  }
</style>