<template>
  <div>
    <div v-if="!ehCelular" class="bg-[#a38967] h-screen">
      <div class="grid grid-cols-12">
        <div class="col-span-3 grid justify-center items-center">
          <div class="col-span-12">
            <img src="/pote.png" alt="Pote" class="rotate-12">
          </div>
          <div class="col-span-12 flex">
            <img src="/colher de pau.png" alt="Pote" class="w-6/12">
            <img src="/colher ovo.png" alt="Pote" class="w-6/12">
          </div>
        </div>
        <div class="col-span-6 col-span-12">
          <Card class="h-[calc(100vh-2rem)] bg-[#cdc4b3] shadow-[10px_10px_20px_rgba(0,0,0,0.8)] my-4">
            <CardHeader>
              <div class="grid grid-cols-3">
                <div>
                  <div class="grid grid-cols-2">
                    <img src="/folha.png" alt="Pote" class="rotate-12">
                    <img src="/pote.png" alt="Pote" class="rotate-12">
                    <img src="/pote.png" alt="Pote" class="rotate-12">
                    <img src="/pote.png" alt="Pote" class="rotate-12">
                  </div>
                  <div class="justify-center">
                    <img src="/pote.png" alt="Pote" class="rotate-12">
                  </div>
                  <div class="grid grid-cols-4">
                    <img src="/suculenta.png" alt="Folha">
                    <img src="/colher de pau.png" alt="Pote" class="rotate-180">
                    <img src="/colher ovo.png" alt="ColherOvo">
                  </div>
                </div>
                <div>
                  <CardTitle class="text-5xl text-nowrap text-center font-PlayfairDisplay flex justify-center items-center">
                    <img src="/buque.png" alt="Folha" class="w-14">
                    CHÁ DE
                    <img src="/buque.png" alt="Folha" class="w-14">
                  </CardTitle>
                  <CardTitle class="text-5xl text-nowrap text-center font-PlayfairDisplay flex justify-center items-center">CASA NOVA</CardTitle>
                  <div class="flex justify-center">
                    <Separator class="my-4 bg-[#856741] w-6/12"/>
                    🥄
                    <Separator class="my-4 bg-[#856741] w-6/12"/>
                  </div>
                  <CardTitle class="text-3xl text-center font-PlayfairDisplay text-nowrap pb-4">IOHANNA & BRUNO</CardTitle>
                  <Card class="bg-[#e4d8c3]">
                    <CardHeader>
                      <CardTitle>
                        Deixe uma mensagem para o casal
                      </CardTitle>
                    </CardHeader>
                    <CardContent>
                      <Caderno class="h-64" v-model="mensagemCasal"/>
                    </CardContent>
                  </Card>
                </div>
                <div>
                  <div class="pl-14 pb-14">
                    <Card class="w-8/12 h-6/6 text-center bg-[#cfb899]" style="cursor: pointer;" @click="teste">
                      <div class="pl-4 pr-4">
                        <div class="font-PlayfairDisplay m-4">
                          LISTA DE PRESENTE
                        </div>
                      </div>
                    </Card>
                  </div>
                  <Foto :photos="['1.jpg', '2.jpg']"/>
                  <Foto class="pl-14" :photos="['3.jpg', '6.jpg']"/>
                  <Foto :photos="['4.jpg', '5.jpg']"/>
                </div>
              </div>
            </CardHeader>
          </Card>
        </div>
        <div class="col-span-3 grid grid-cols-2 items-center">
          <div class="col-span-2 grid place-items-center">
            <img src="/folha.png" alt="Pote" class="rotate-45 w-[calc(100%-10rem)]">
          </div>
          <img src="/suculenta.png" alt="Pote" class="rotate-12 col-span-1 w-[calc(100%-1rem)]">
          <img src="/pote.png" alt="Pote" class="rotate-12 col-span-1 w-[calc(100%-2rem)]">
        </div>
      </div>
    </div>
    <div v-else class="bg-[#a38967] h-screen">
      <Card class="bg-[#cdc4b3] h-screen">
        <CardHeader>
          <CardTitle class="text-5xl text-nowrap text-center font-PlayfairDisplay flex justify-center items-center">
            <img src="/buque.png" alt="Folha" class="w-14">
            CHÁ DE
            <img src="/buque.png" alt="Folha" class="w-14">
          </CardTitle>
          <CardTitle class="text-5xl text-nowrap text-center font-PlayfairDisplay flex justify-center items-center">CASA NOVA</CardTitle>
          <div class="flex justify-center">
            <Separator class="my-4 bg-[#856741] w-6/12"/>
            🥄
            <Separator class="my-4 bg-[#856741] w-6/12"/>
          </div>
          <CardTitle class="text-3xl text-center font-PlayfairDisplay text-nowrap pb-4">IOHANNA & BRUNO</CardTitle>
        </CardHeader>
        <Card class="bg-[#e4d8c3]">
          <CardHeader>
            <CardTitle class="text-center">
              Deixe uma mensagem para o casal
            </CardTitle>
          </CardHeader>
          <CardContent>
            <Caderno class="h-64" v-model="mensagemCasal"/>
          </CardContent>
        </Card>
        <Card class="my-4 text-center bg-[#cfb899]" style="cursor: pointer;" @click="teste">
          <div class="pl-4 pr-4">
            <div class="font-PlayfairDisplay m-4">
              LISTA DE PRESENTE
            </div>
          </div>
        </Card>
      </Card>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'
import Caderno from '@/components/Caderno.vue'
import Foto from '@/components/Foto.vue'

const lista = ref([{}])
const ehCelular = ref(false)

const ehMobile = () => {
  const userAgent = navigator.userAgent || navigator.vendor || window.opera
  ehCelular.value = /android|iphone|ipad|ipod|opera mini|iemobile|wpdesktop/i.test(userAgent.toLowerCase())
}

const mensagemCasal = ref('')

const teste = () => {
  console.log('passei')
}

onMounted(() => {
  ehMobile()
})
</script>