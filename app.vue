<template>
  <TheNavbar />
  <TheTopimage />
  <div class="NuxtPage">
    <NuxtPage />
  </div>
  <div class="TheFooter">  
    <TheFooter />
  </div>

</template>
<script setup lang="ts">
useHead({
  title: 'ConcoursPhoto StudioImageIn',
  meta :[ {property:"og:url",           content:"http://concours-studioimagein.com:3000"},
  {property:"og:type",          content:"website"},
  {property:"og:title",         content:"Concours Photo Studio Image In"},
  {property:"og:description",   content:"Venez participer au concours photo de Studio Image In"},
  {property:"og:image",         content:"https://www.your-domain.com/path/image.jpg"}] ,
  link : [{
                href:"https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css",
                rel:"stylesheet",
                integrity:"sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC",
                crossorigin:"anonymous" 
            }],
            script :[
                {
                    src:"https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js",
                    crossorigin:"anonymous"
                }
            ]
            
})
</script>

<style scoped>
.NuxtPage {
  margin-top: 5%;
}
.TheFooter {
  margin-top: 10%;
}


</style>