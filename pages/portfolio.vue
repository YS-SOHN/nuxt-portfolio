<template lang="">
  <div class="w-full pt-12 mt-16 px-[2%] pb-8">
   <TitleText title="포트폴리오" />
    <div class="max-w-7xl mx-auto mt-8">
      <ul class="flex m-4">
        <li class="mr-4 border darMode bg-white py-2 px-5 rounded-md">
          <button @click="CateName = '전체'" :class="CateName === '전체' && 'font-bold text-orange-500'">전체</button>
        </li>
        <li class="mr-4 border darkMode bg-white py-2 px-5 rounded-md" v-for="e in CateList" :key="e">
          <!-- 삼항 연산자에서 &&가 붙으면 참만 있고 거짓은 없다.. ?와 :가 붙으면 참 거짓 구분-->
          <button @click="CateName = e.type" :class="CateName === e.type && 'font-bold text-orange-500'">{{e.type}}</button>
        </li>
      </ul>
    </div>
    <div class="max-w-7xl mx-auto mt-8">
      <!-- group(공식용어) 속성 - nth시리즈와 동일 -->
      <div v-for="e in CateItem" :key="e" class="bg-white mb-8 pt-12 group px-8 pb-16  rounded-md flex border darkMode flex-wrap">
        <!-- even:짝수 odd:홀수 -->
       <div class="basis-[48%] relative mokup-img group-even:order-1 xl:group-even:order-2">
        <div v-for="e in 3" :key="e">
          <img class="w-full" :src="`/images/mokup-${e}.png`" alt="mokup" />
        </div>
       </div>
       <div class="basis-full md:basis-[52%] pt-10 group-even:order-2 xl:group-even:order-1">
          <h3 class="text-2xl font-bold pt-[10px] pb-[10px] lg:px-[50px]">
            {{ e.descTitle }}
          </h3>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]"> {{ e.desc }}</p>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">키워드 : <span v-for="el in e.Keyword" :key="el" class="mr-2">{{el}}</span></p>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">컬러 : <span v-for="el in e.color" :key="el" class="w-5 h-5 inline-block align-middle mr-2" :style="{backgroundColor: `${el}`}"></span></p>
          <!-- :style함수는 js내장함수, span태그에 내용이 없이 배경만 입히며 css와 별개 -->
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">폰트 : {{ e.font }} </p>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">사용 툴 : <span v-for="el in e.tools" :key="el" class="mr-2 align-middle">{{el}}</span></p>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">작업 기간 : {{ e.date }}</p>
          <p class="text-base pt-[10px] pb-[10px] lg:pl-[50px]">기여도 : {{ e.contribution }}</p>
          <ul class="flex justify-center mt-6">
            <!-- v-if="e.progress !== ''" 와 같음 -->
            <!-- e.progress는 모달창, 디자인 필요 -->
            <li v-if="e.progress"><a :href="e.progress" class="mr-4 py-1 px-8 border rounded-md darkMode text-sm">progress</a></li>
            <!-- 원래 original에만 mx-auto(좌우마진)지만 조건문의 의해 없는 값이 생겨서 붙는 컨텐츠 때문에 1,2번째에 우측마진-4 mr-4를 넣어줌 -->
            <li v-if="e.original"><a :href="e.original" target="_blank" class="mr-4 py-1 px-8 border rounded-md darkMode text-sm">original</a></li>
            <li v-if="e.redesign"><a :href="e.redesign" target="_blank" class="py-1 px-8 border rounded-md darkMode text-sm">{{ e.type === 'Publishing' ? 'Clone' : 'redesign'}}</a></li>
            <!-- 원래는 Redesign, 삼항 연산자를 통해 표현 -->
          </ul>
       </div>
      </div>
    </div>
  </div>
</template>
<script>

export default {

  computed:{
    // 필터 코드 - 자주쓰임
    CateItem(){
    return this.WorkList.filter((data)=>{
      // 전체 버튼 클릭 시 컨텐츠 다 표시

      if(this.CateName !== '전체'){
        return data.type === this.CateName
      }else{
       return data.type 
        }
      })
    },
    CateList(){
      return this.WorkList.filter((item,i)=>{
        return(
          this.WorkList.findIndex((item2)=>{
            return item.type === item2.type
          }) === i
        )
      })
    },
  },

  data() {
    return {
      CateName: '전체',
      WorkList: [
        {
          "img" : "https://via.placeholder.com/500",
          "descTitle" : "XXXX 웹앱",
          "desc" : "API를 활용한 웹앱 개발...",
          "Keyword" : ["#심플함", "#깔끔함", "#tailwind"],
          "color" : ["orange", "orangered", "darkorange"],
          "font" : "Noto Sans KR",
          "tools" : ["PS", "AI", "VS CODE"],
          "date" : "10일(기획1일 / 구상1일 / 제작8일)",
          "contribution" : "100%",
          "type" : "Publishing",
          "progress" : "https://via.placeholder.com/1200x5000",
          "original" : "http://www.naver.com",
          "redesign" : "http://www.kakao.com"
        },
        {
          "img" : "https://via.placeholder.com/500",
          "descTitle" : "XXXX 클론 코딩",
          "desc" : "API를 활용한 웹앱 개발...2",
          "Keyword" : ["#심플함", "#깔끔함", "#tailwind"],
          "color" : ["orange", "orangered", "darkorange"],
          "font" : "Noto Sans KR",
          "tools" : ["PS", "AI", "VS CODE"],
          "date" : "10일(기획1일 / 구상1일 / 제작8일)",
          "contribution" : "100%",
          "type" : "Publishing",
          "progress" : "",
          "original" : "http://www.naver.com",
          "redesign" : ""
        },
        {
          "img" : "https://via.placeholder.com/500",
          "descTitle" : "XXXX 퍼블리싱",
          "desc" : "API를 활용한 웹앱 개발...",
          "Keyword" : ["#심플함", "#깔끔함", "#tailwind"],
          "color" : ["orange", "orangered", "darkorange"],
          "font" : "Noto Sans KR",
          "tools" : ["PS", "AI", "VS CODE"],
          "date" : "10일(기획1일 / 구상1일 / 제작8일)",
          "contribution" : "100%",
          "type" : "Webapp",
          "progress" : "https://via.placeholder.com/1200x5000",
          "original" : "",
          "redesign" : "http://www.kakao.com"
        },
        {
          "img" : "https://via.placeholder.com/500",
          "descTitle" : "XXXX 웹앱 1234",
          "desc" : "API를 활용한 웹앱 개발...",
          "Keyword" : ["#심플함", "#깔끔함", "#tailwind"],
          "color" : ["orange", "orangered", "darkorange"],
          "font" : "Noto Sans KR",
          "tools" : ["PS", "AI", "VS CODE"],
          "date" : "10일(기획1일 / 구상1일 / 제작8일)",
          "contribution" : "100%",
          "type" : "Webapp",
          "progress" : "https://via.placeholder.com/1200x5000",
          "original" : "http://www.naver.com",
          "redesign" : ""
        },
      ]  
    }
  },
}
</script>
<style>
  .mokup-img > div{ position: absolute; overflow:hidden; bottom:0; }

  .mokup-img > div:nth-child(1){ width: 85%; left:50%; transform: translateX(-50%); }
  .mokup-img > div:nth-child(1)::after{ content:''; position: absolute; width: 92%; height: 63%; background: url("/images/preview.jpg") center top no-repeat; left: 19px; top: 20px; background-size: cover; transition: 5s; border-radius: 5px; }
  .mokup-img > div:nth-child(2){ width: 35%; right: 0; }
  .mokup-img > div:nth-child(2)::after{ content:''; position: absolute; width: 86%; height: 82%; background: url("/images/preview.jpg") center top no-repeat; left: 16px; top: 26px; background-size: cover; transition: 5s; border-radius: 5px; }
  .mokup-img > div:nth-child(3){ width: 23%; left: 0; }
  .mokup-img > div:nth-child(3)::after{ content:''; position: absolute; width: 90%; height: 95%; background: url("/images/preview.jpg") center top no-repeat; left: 7px; top: 8px; background-size: cover; transition: 5s; border-radius: 5px;}
  .mokup-img > div:hover::after{ background-position: center bottom; }

  /* 태블릿 */
  @media screen and (max-width: 1200px){ 
    .mokup-img{ flex-basis: 100%; height: 500px;}
    .mokup-img > div:nth-child(1){ width: 550px; }
    .mokup-img > div:nth-child(2){ width: 184px; }
    .mokup-img > div:nth-child(3){ width: 126px; }
    .mokup-img > div:nth-child(1)::after{ top: 23px; height: 62%; left: 21px; width: 87%; }
    .mokup-img > div:nth-child(2)::after{ width: 85%; top: 24px; }
   }
  /* 모바일 */
  @media screen and (max-width: 640px){ 
    .mokup-img{ height: 70.3125vw; }
    .mokup-img > div:nth-child(1){ width: 100%; }
    .mokup-img > div:nth-child(2){ width: 35%; }
    .mokup-img > div:nth-child(3){ width: 20%; }
    .mokup-img > div:nth-child(1)::after{ width: 92.5%; left: 3.8%; top: 3.7%; }
    .mokup-img > div:nth-child(2)::after{ left: 8%; top: 8%; }
    .mokup-img > div:nth-child(3)::after{ height: 92.5%; left: 5.5%; top: 2.5%; }
   }
</style>