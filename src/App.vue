<template>
  <div :class="`flex justify-center items-center bg-[#a38967] ${screenHeight >= 840 ? 'h-screen' : ''}`" style="background-image: url('/juntas.png')">
    <Card class="bg-[#cdc4b3] shadow-[10px_10px_20px_rgba(0,0,0,0.8)] xl:w-[50%]">
      <CardHeader>
        <div class="grid grid-cols-12">
          <div class="hidden 2xl:col-span-3 xl:col-span-2 xl:grid 2xl:grid-cols-2 xl:grid-cols-1 content-center sm:content-none">
            <img src="/colher ovo.png" alt="Pote" class="rotate-45">
            <img src="/colher de pau.png" alt="Pote" class="rotate-45">
            <img src="/pote.png" alt="Pote" class="rotate-45">
            <img src="/prato.png" alt="Pote" class="rotate-12">
            <img src="/bule 2.png" alt="Pote" class="-rotate-12">
            <img src="/xicara.png" alt="Pote" class="rotate-12">
            <img src="/taboaCarne.png" alt="Pote" class="rotate-12 col-span-2">
          </div>
          <div class="2xl:col-span-6 xl:col-span-8 col-span-12">
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
            <CardTitle class="text-3xl text-center font-PlayfairDisplay pb-4">IOHANNA & BRUNO</CardTitle>
            <Card class="bg-[#e4d8c3] text-center">
              <CardHeader>
                <CardTitle class="text-center">
                  Deixe uma mensagem para o casal
                </CardTitle>
              </CardHeader>
              <CardContent>
                <Input placeholder="Seu nome" v-model="nomePessoa" class="bg-white"/>
                <Caderno class="h-64" v-model="mensagemCasal"/>
              </CardContent>
              <div class="flex justify-center gap-4 mb-6">
                <Button @click="abrirListaPresente">Lista de Presente</Button>
                <Button>Enviar</Button>
              </div>
            </Card>
          </div>
          <div class="hidden xl:grid 2xl:col-span-3 xl:col-span-2 content-center sm:content-none">
            <Foto class="xl:pb-4 xl:h-32" :photos="['1.jpg', '2.jpg']"/>
            <Foto class="xl:pb-4 xl:h-32" :photos="['3.jpg', '6.jpg']"/>
            <Foto class="xl:pb-4 xl:h-32" :photos="['4.jpg', '5.jpg']"/>
            <Foto class="xl:pb-4 xl:h-32" :photos="['7.jpg', '8.jpg']"/>
            <Foto class="xl:pb-4 xl:h-32" :photos="['9.jpg', '10.jpg']"/>
          </div>
        </div>
      </CardHeader>
      <div class="flex justify-center">
        <Separator class="my-4 bg-[#856741] w-4/12"/>
        🥄
        <Separator class="my-4 bg-[#856741] w-4/12"/>
      </div>
      <CardContent class="text-center font-PlayfairDisplay text-3xl">
        Rua Elias Antonio Zogbi, 150 - Santo Amaro - São Paulo - SP
        <br>
        Salão de Festa - a partir das 14h
      </CardContent>
    </Card>
  </div>
  <Dialog v-model:open="dialogListaPresente">
    <DialogContent class="bg-[#cdc4b3] font-PlayfairDisplay h-[90%] max-w-5xl">
      <DialogHeader>
        <DialogTitle class="text-6xl text-center">Lista de Presente</DialogTitle>
        <DialogDescription>
          <div class="flex justify-center">
            <Separator class="my-4 bg-[#856741] w-6/12"/>
            🥄
            <Separator class="my-4 bg-[#856741] w-6/12"/>
          </div>
          Selecione um ou mais presente(s)
        </DialogDescription>
      </DialogHeader>
      <ScrollArea>
        <div class="grid grid-cols-12 gap-4">
          <Card v-for="(grupo, index) in lista" :key="index" class="col-span-12 md:col-span-4">
            <CardContent>
              <h2 class="text-lg font-semibold text-center border-b border-gray-300 pb-2">{{ grupo.nome }}</h2> 
              <div v-for="(presente, indexPresente) in grupo.presentes" :key="indexPresente" style="cursor: pointer;">
                <span class="mr-2">•</span>
                <span class="text-sm">{{ presente.nome }}</span>
              </div>
            </CardContent>
          </Card>
        </div>
      </ScrollArea>
      <DialogFooter>
        <Button @click="dialogListaPresente = false">Ok</Button>
      </DialogFooter>
    </DialogContent>
  </Dialog>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription, DialogFooter } from '@/components/ui/dialog'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import { ScrollArea } from '@/components/ui/scroll-area'
import Caderno from '@/components/Caderno.vue'
import Foto from '@/components/Foto.vue'
import { createClient } from '@supabase/supabase-js'


const lista = ref([])
const nomePessoa = ref('')
const dialogListaPresente = ref(false)
const screenWidth = ref(window.innerWidth)
const screenHeight = ref(window.innerHeight)
const cardPrincipal = ref(null)
const isMobile = ref(false)

const mensagemCasal = ref('')

const abrirListaPresente = () => {
  dialogListaPresente.value = true
}
const checkDevice = () => {
  const userAgent = navigator.userAgent || navigator.vendor || window.opera
  isMobile.value = /android|iphone|ipad|ipod|opera mini|iemobile|wpdesktop/i.test(userAgent.toLowerCase())
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
  window.addEventListener('resize', () => {
    screenWidth.value = window.innerWidth
    screenHeight.value = window.innerHeight
  })
  checkDevice()
  const { data, error } = await supabase.from('presente').select('*')
  lista.value = agruparPorGrupo(data)
})
</script>