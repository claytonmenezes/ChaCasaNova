<template>
  <div class="grid grid-cols-12 items-center justify-center bg-[#a38967] h-screen" style="background-image: url('/juntas.png')">
    <div v-if="!ehCelular" class="col-span-3"></div>
    <Card class="bg-[#cdc4b3] shadow-[10px_10px_20px_rgba(0,0,0,0.8)] col-span-6">
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
                <CardTitle class="text-center">
                  Deixe uma mensagem para o casal
                </CardTitle>
              </CardHeader>
              <CardContent>
                <Input placeholder="Seu nome" v-model="nomePessoa" class="bg-white"/>
                <Caderno class="h-64" v-model="mensagemCasal"/>
              </CardContent>
            </Card>
          </div>
          <div class="col-span-4">
            <Card class="ml-14 2xl:ml-0 mb-28 2xl:mb-10 font-PlayfairDisplay bg-[#cfb899]" style="cursor: pointer;" @click="abrirListaPresente">
              <CardHeader>
                <CardTitle class="text-center">
                  LISTA DE PRESENTE
                </CardTitle>
              </CardHeader>
            </Card>
            <Foto class="pl-10 2xl:pl-0 pb-6 2xl:pb-0" :photos="['1.jpg', '2.jpg']"/>
            <Foto class="pl-14 pb-6 2xl:pb-0" :photos="['3.jpg', '6.jpg']"/>
            <Foto class="pl-10 2xl:pl-0" :photos="['4.jpg', '5.jpg']"/>
          </div>
        </div>
      </CardHeader>
      <CardContent class="text-center">
        asdasdasdasdasdasdasdasd
      </CardContent>
    </Card>
  </div>
  <Dialog v-model:open="dialogListaPresente">
    <DialogContent class="bg-[#cdc4b3] font-PlayfairDisplay h-screen max-w-4xl">
      <DialogHeader>
        <DialogTitle class="text-6xl text-center">Lista de Presente</DialogTitle>
        <DialogDescription/>
        <div class="flex justify-center">
          <Separator class="my-4 bg-[#856741] w-6/12"/>
          🥄
          <Separator class="my-4 bg-[#856741] w-6/12"/>
        </div>
      </DialogHeader>
      <PresentList :grupos="lista"/>
    </DialogContent>
  </Dialog>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription } from '@/components/ui/dialog'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import Caderno from '@/components/Caderno.vue'
import Foto from '@/components/Foto.vue'
import { createClient } from '@supabase/supabase-js'
import PresentList from '@/components/PresentList.vue'

const lista = ref([])
const nomePessoa = ref('')
const ehCelular = ref(false)
const dialogListaPresente = ref(false)
const ehMobile = () => {
  const userAgent = navigator.userAgent || navigator.vendor || window.opera
  ehCelular.value = /android|iphone|ipad|ipod|opera mini|iemobile|wpdesktop/i.test(userAgent.toLowerCase())
}

const mensagemCasal = ref('')

const abrirListaPresente = () => {
  dialogListaPresente.value = true
}
const supabase = createClient('https://acfrcmkzzabbqtwchiow.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFjZnJjbWt6emFiYnF0d2NoaW93Iiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTczMDQ3NzE3OCwiZXhwIjoyMDQ2MDUzMTc4fQ.ZoWVFkjTxFJL5ox3Zb-R4hgk7t6ia9T639aJEFZF4js')

const agruparPorGrupo = (presentes) => {
  return presentes.reduce((acc, presente) => {
    const { grupo, nome, qtde } = presente

    // Se o grupo ainda não existe no acumulador, cria um novo
    if (!acc[grupo]) {
      acc[grupo] = { nome: grupo, presentes: [] }
    }

    // Adiciona o nome do item ao array de itens do grupo
    acc[grupo].presentes.push({nome, qtde})

    return acc
  }, {})
}

onMounted(async () => {
  ehMobile()
  const { data, error } = await supabase.from('presente').select('*')
  lista.value = agruparPorGrupo(data)
})
</script>