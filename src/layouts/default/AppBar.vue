<template>
  <div>
    <!-- 上侧应用栏容器 -->
    <v-app-bar
      color="blue"
      dark
    >
      <!-- 控制侧导航栏状态（隐藏/显示） -->

      <!-- 标题 -->
      <v-toolbar-title
        class="hidden-sm-and-down ml-0 pl-4"
        style="width: 300px"
      >
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
      
      <!-- 登录  -->
      <v-dialog>
        <template v-slot:activator="{ props }">
          <v-btn v-bind="props" icon>
            <v-icon>mdi-account</v-icon>
          </v-btn>
        </template>

        <Login/>

      </v-dialog>

    </v-app-bar>

  </div>
  
</template>

<script setup>
import { ref } from 'vue'
import Login from '@/components/Login.vue'
const drawer = ref(false)

const items = [
  { text: '首页', icon: 'mdi-home', link: '/' },
  { text: '文章', icon: 'mdi-file-document', link: '/article' },
  { text: '标签', icon: 'mdi-tag', link: '/tag' },
  { text: '关于', icon: 'mdi-account', link: '/about' },
]

import { useRouter } from 'vue-router';
const router = useRouter()
function goToLoginPage() {
  router.push('/login')
}

</script>
