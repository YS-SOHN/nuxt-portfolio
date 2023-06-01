<template>
  <div>
    <div class="w-full px-[2%] sticky top-0 bg-white py-2.5 z-50 darkMode">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
      <nuxt-link to="/">
          <img src="https://via.placeholder.com/120x50" alt="logo">
      </nuxt-link>


      <div class="basis-3/4 hidden md:block">
        <ul class="flex justify-around">
          <li v-for="e in NavList" :key="e">
            <!-- 'section-' +인덱스번호 -->
            <nuxt-link :to="e.link">{{e.name}}</nuxt-link>
            <!--  -->
          </li>
          <!-- <li v-for="(e, index) in NavList[0]" :key="e">
            <router-link :to="NavList[1][index]">{{ e }}</router-link>
          </li>  router 링크-->
          <!-- <li><router-link to="/profile">프로필</router-link></li>
          <li><router-link to="/profile">스킬</router-link></li>
          <li><router-link to="/profile">포트폴리오</router-link></li> -->
        </ul>
      </div>
      
      <div class="basis-1/12 hidden md:block">
        <ul class="flex justify-between">
          <li class="basis-2/4 text-center cursor-pointer">
            <!-- emit()괄호 안에 이름은 작명 -->
            <font-awesome-icon :icon="['fas',isDark ? 'moon' : 'sun']" @click="toggleTheme" />
          </li>
          <li class="basis-2/4 text-center cursor-pointer relative group">
            <font-awesome-icon :icon="['fas','glove']" />
            <ul class="absolute -left-3 top-8 bg-white w-20 group-hover:border rounded-md group-hover:h-20 transition-all h-0 overflow-hidden">
              <li @click="$emit('lang',0); SelectLang(0)" class="py-3 pb-0 hover:font-bold"><button>한국어</button></li>
              <li @click="$emit('lang',1); SelectLang(1)" class="py-2.5 hover:font-bold"><button>영어</button></li>
              <!-- SelectLang 는 로컬 스토리지에 저장하는거, 새로고침 했을때 언어 변경이 되지 않게 하기위함 -->
            </ul>
          </li>
        </ul>
      </div>

      <div>
        <font-awesome-icon :icon="['fas','bars']" class="!text-3xl cursor-pointer md:!hidden" @click="isOpen === false ? isOpen = true : isOpen = false"/>
      </div>
<!-- 질문 1 : md:hidden  768px 보다 더 커져있을때는 숨김 -->
<div class="w-72 h-full fixed darkMode bg-gray-100 z-50 p-12 box-border transition-all duration-500 top-0 -right-80 md:hidden" :class="isOpen == true && '!right-0'">
  <!-- 질문 2 :  true 일때 -right-80 만큼 들어간다. 면적은 w-72 다. false 일때 각각 실행되는 내용-->
  <!--  !right-0 은 임폴턴트 이므로 right-0 과 같은 내용을 가진다. -->
        <font-awesome-icon :icon="['fas','xmark']" class="absolute top-5 right-5 !text-3xl cursor-pointer md:hidden" @click="isOpen = false" />

        <div class="text-center mt-6">
          <img src="https://via.placeholder.com/100" alt="img" class="mx-auto rounded-full mb-4">
          <p>프론트엔드 개발자 손유상</p>
          <ul class="mt-12">
            <li class="py-5 border-5" v-for="e in NavList" :key="e">
              <font-awesome-icon :icon="['fas','e.icon']" class="mr-1" />
              <nuxt-link  @click="isOpen = false" :to="e.link">{{e.name}}</nuxt-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
data() {
  return {
    isDark : this.$colorMode.preference === 'dark',
    isOpen : false,
    NavList : [
      {
        name: "프로필",
        link : "/about",
        icon: "user"
      },
      {
        name: "스킬",
        link : "/skill",
        icon: "code"
      },
      {
        name: "포트폴리오",
        link : "/portfolio",
        icon: "folder-open"
      }
    ]
  }
},
methods : {
  toggleTheme(){
    this.$colorMode.preference = this.isDark ? 'light' : 'dark';
    this.isDark = !this.isDark;
  }
},
}
</script>

<style>
.dark-mode body {
  /* background-color :#091a28 */
  animation : infinite 9s background alternate-reverse
}

@keyframes background{
  0%{background-color:#091a28}
  50%{background-color:#08131b}
  100%{background:#030507}
}
</style>