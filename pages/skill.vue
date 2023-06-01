<template lang="">
  <!-- mt-nn -->
  <div class="w-full pt-12 mt-8 px-[2%] pb-8">
    <TitleText title="스킬" /> <!-- 각 페이지 별 타이틀을 컴포넌트 화해서 props 방식으로 동시 적용 -->
    <div class="max-w-7xl mx-auto mt-8">
      <div class="bg-white rounded-md border darkMode p-5 mb-8 last:mb-0">
        <div class="w-full h-20" v-for="e in ProgressList" :key="e">
          <div class="w-full h-5 bg-[#e0e0de] rounded-[50px]">
            <div class="h-full bg-slate-700 duration-1000 ease-in-out rounded-[50px] text-right relative mb-3 first:mt-10" :style="{width: `${e.progressBefore}%`}">
              <p class="absolute -top-6 md:-top-7 left-1 text-sm md:text-lg">{{ e.testList }}</p>
              <span class="text-sm pr-2 relative -top-0.5 text-white dark:text-[#d9d9d9]">{{ e.progressBefore }}%</span>
            </div>
            <p class="text-sm md:text-base pl-1">{{ e.desc }}</p>
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
      ProgressList:[
        {
          testList: "HTML",
          // 0에서 시작 -> 30까지 차는 모습을 보이기위해 Before와 Ater값을 주며, 바가 채워져있는 상태로 시작한다면 Before값 삭제
          progressBefore: 0,
          progressAter: 60,
          desc: "웹 표준에 준수하여, 마크업을 할 수 있다. float가 아닌 flex 및 grid를 활용한 레이아웃 구성을 할 수 있다."
        },
        {
          testList: "CSS",
          progressBefore: 0,
          progressAter: 50,
          desc: "가상 선택자와 스와이퍼 슬라이드를 이용한 페이지 스타일링"
        },
        {
          testList: "Js",
          progressBefore: 0,
          progressAter: 40,
          desc: "메뉴 구성, 스크롤 등의 여러가지 페이지 동작 구현."
        },
        {
          testList: "Jquery",
          progressBefore: 0,
          progressAter: 40,
          desc: "제이쿼리를 이용하여 컨텐츠 페이드 인/아웃 구성."
        },
        {
          testList: "Vue",
          progressBefore: 0,
          progressAter: 40,
          desc: "반복/조건문(v-for/v-if,else)을 사용하여 레이아웃에 데이터 유무 구분."
        },
        {
          testList: "React",
          progressBefore: 0,
          progressAter: 20,
          desc: "description."
        }
      ]
    }
  },
  mounted(){
    this.ProgressList.forEach((e)=>{
      setTimeout(() => {
        e.progressBefore = e.progressAter
      }, 400);
    })
  }
}
</script>
