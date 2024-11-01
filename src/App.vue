<template>
  <div>
    <div v-if="!ehCelular" class="bg-[#a38967] h-screen">
      <div class="grid grid-cols-12">
        <div class="col-span-3">
          <img src="/juntas.png" alt="Pote" style="object-fit: cover" class="h-screen">
        </div>
        <div class="col-span-6">
          <Card class="h-screen bg-[#cdc4b3] shadow-[10px_10px_20px_rgba(0,0,0,0.8)]">
            <CardHeader>
              <div class="grid grid-cols-12">
                <div class="col-span-4">
                  <div class="grid grid-cols-2">
                    <div class="pt-10 2xl:pt-0">
                      <img src="/colher de pau 2.png" alt="Pote" class="rotate-45 w-14 ml-8">
                      <img src="/prato.png" alt="Pote" class="rotate-12 w-32 ">
                    </div>
                    <div class="pt-10 2xl:pt-0">
                      <img src="/bule 2.png" alt="Pote" class="rotate-12 lg:pr-6">
                      <img src="/xicara.png" alt="Pote" class="rotate-12">
                    </div>
                  </div>
                  <div class="justify-center pt-10 2xl:pt-0">
                    <img src="/taboaCarne.png" alt="Pote" class="rotate-12">
                  </div>
                </div>
                <div class="col-span-4">
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
                  <Card class="bg-[#e4d8c3] w-64 2xl:w-full">
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
                <div class="col-span-4">
                  <div class="pl-14 pb-28 2xl:pb-10">
                    <Card class="w-8/12 h-6/6 text-center bg-[#cfb899]" style="cursor: pointer;" @click="teste">
                      <div class="">
                        <div class="font-PlayfairDisplay m-4">
                          LISTA DE PRESENTE
                        </div>
                      </div>
                    </Card>
                  </div>
                  <Foto class="pl-10 2xl:pl-0 pb-6 2xl:pb-0" :photos="['1.jpg', '2.jpg']"/>
                  <Foto class="pl-14 pb-6 2xl:pb-0" :photos="['3.jpg', '6.jpg']"/>
                  <Foto class="pl-10 2xl:pl-0" :photos="['4.jpg', '5.jpg']"/>
                </div>
              </div>
            </CardHeader>
            <CardContent class="text-center">
              asdasdasdasdasdasd
            </CardContent>
          </Card>
        </div>
        <div class="col-span-3">
          <img src="/juntas.png" alt="Pote" style="object-fit: cover" class="h-screen">
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