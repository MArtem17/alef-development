<template>
  <v-app>
    <v-app-bar fixed app dense color="white" height="76px">
      <v-img src="logo-header.svg" alt="logo-header" class="header__img"></v-img>

      <v-list class="menu">
        <v-list-item class="menu__item" v-for="(item, i) in items" :key="i" :to="item.to" router exact>
          <v-list-item-content>
            <v-list-item-title>{{
              item.title
            }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-app-bar>
    <v-main width="100%">
      <div class="custom-container">
        <Nuxt />
      </div>
    </v-main>
    <v-footer :absolute="!fixed" app height="76px" color="rgba(11,11,11,0.1)">
      <span style="width:100%" class="text-center">all rights reserved</span>
    </v-footer>
  </v-app>
</template>

<style>
.header__img {
  position: absolute;
  z-index: 2;
  left: 5vw;
  max-width: 93px;
  height: auto;
}

.menu {
  display: flex;
  margin: auto;
  padding: 0px;
}

.menu__item {
  width: 100px;
  padding: auto;
  text-align: center;
  color: rgba(11, 11, 11, 0.48);
  font-size: 14px;
  line-height: 24px;
  font-weight: 400;
}

.custom-container {
  max-width: 616px;
  padding: 5px;
  margin: 30px auto;
}
</style>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      fixed: false,
      items: [
        {
          title: 'Форма',
          to: '/'
        },
        {
          title: 'Превью',
          to: '/preview'
        }
      ],
    }
  }
}
</script>
