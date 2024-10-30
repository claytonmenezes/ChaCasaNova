<template>
  <div class="bg-[#a38967]">
    <div class="grid grid-cols-12">
      <div class="col-span-3 items-center grid justify-center">
        <div class="col-span-12">
          <img src="/pote.png" alt="Pote" class="rotate-12">
        </div>
        <div class="col-span-12 flex">
          <img src="/colher de pau.png" alt="Pote" class="w-6/12">
          <img src="/colher ovo.png" alt="Pote" class="w-6/12">
        </div>
      </div>
      <Card class="col-span-6 h-[calc(100vh-2rem)] bg-[#cdc4b3] shadow-[10px_10px_20px_rgba(0,0,0,0.8)] my-4">
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
                <Card class="w-8/12 h-6/6 text-center bg-[#a38967]" style="cursor: pointer;" @click="teste">
                  <div class="pl-4 pr-4">
                    <div class="font-PlayfairDisplay m-4">
                      LISTA DE PRESENTE
                    </div>
                  </div>
                </Card>
              </div>
              <Foto :photos="['/1.jpg', '/2.jpg']"/>
              <Foto class="pl-14" :photos="['/3.jpg']"/>
              <Foto :photos="['4.jpg', '5.jpg']"/>
              <Foto class="pl-10" :photos="['6.jpg']"/>
            </div>
          </div>
        </CardHeader>
        <CardContent>
        </CardContent>
      </Card>
      <div class="col-span-3 grid grid-cols-12 items-center">
        <img src="/folha.png" alt="Pote" class="-rotate-45 col-span-6">
        <img src="/suculenta.png" alt="Pote" class="rotate-12 col-span-6">
        <img src="/pote.png" alt="Pote" class="rotate-12 col-span-12">
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'
import Caderno from '@/components/Caderno.vue'
import Foto from '@/components/Foto.vue'

const mensagemCasal = ref('')

const teste = () => {
  console.log('passei')
}
const lista = ref([{}])
</script>