<template>
  <div>
    <NuxtLayout>
        <NuxtPage/>
    </NuxtLayout>
    <Footer />
  </div>
</template>

<style>
html,body {height:100%;}
body {animation:alternate-reverse background2 9s infinite;}
.dark-mode .darkMode {
  background-color :#272929;
  border-color:#3b3b3b;
  color : #d9d9d9;
}

@keyframes background{
  0%{background-color:#f7f8f9}
  50%{background-color:#f5f9fd}
  100%{background:#f1f0f5}
}
</style>
