<template>
  <div>
    <!-- 侧导航栏 -->
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
    >
      <router-link v-for="item in items" :key="item.text" :to="item.link">
        <v-list-item
          link
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          
          <v-list-item-content>
            <v-list-item-title>
              {{ item.text }}
            </v-list-item-title>
          </v-list-item-content>

        </v-list-item>
      </router-link>
    </v-navigation-drawer>

    <!-- 上侧应用栏容器 -->
    <v-app-bar
      color="blue"
      dark
    >
      <!-- 控制侧导航栏状态（隐藏/显示） -->
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <!-- 标题 -->
      <v-toolbar-title
        class="hidden-sm-and-down ml-0 pl-4"
        style="width: 300px"
      >
        <!-- <span style="cursor:pointer" @click="goToHome()">{{ this.$store.state.webInfo.name }}</span> -->
      </v-toolbar-title>

      <!-- 搜索框 -->
      <v-text-field
        flat
        solo-inverted
        hide-details
        prepend-inner-icon="mdi-magnify"
        label="搜索"
      />
      <v-spacer />
      
      <v-btn icon>
        <v-icon>mdi-bell</v-icon>
      </v-btn>
      
      <!-- 登录按钮 -->
      <v-btn icon>
        <v-icon>mdi-account</v-icon>
      </v-btn>
    </v-app-bar>

  </div>
  
</template>

<script setup>
import { ref } from 'vue'
const drawer = ref(false)

const items = [
  { text: '首页', icon: 'mdi-home', link: '/' },
  { text: '文章', icon: 'mdi-file-document', link: '/article' },
  { text: '标签', icon: 'mdi-tag', link: '/tag' },
  { text: '关于', icon: 'mdi-account', link: '/about' },
]

</script>
