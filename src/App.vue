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
                <Input placeholder="Seu nome" v-model="convidado.nome" class="bg-white"/>
                <Caderno class="h-64" v-model="convidado.mensagem"/>
              </CardContent>
              <Label>Estará presente no dia?</Label>
              <RadioGroup v-model="convidado.presente" orientation="horizontal">
                <div class="flex justify-center items-center space-x-2 pb-4">
                  <RadioGroupItem :value="true" />
                  <Label for="r1">Sim</Label>
                  <RadioGroupItem :value="false" />
                  <Label for="r2">Não</Label>
                </div>
              </RadioGroup>
              <div class="flex justify-center gap-4 mb-6">
                <Button @click="abrirListaPresente">Lista de Presente</Button>
                <Button @click="enviar">Enviar</Button>
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
          <div class="flex justify-center">
            Selecione um ou mais presente(s)
          </div>
        </DialogDescription>
      </DialogHeader>
      <ScrollArea>
        <div class="grid grid-cols-12 gap-4">
          <Card v-for="(grupo, index) in lista" :key="index" class="col-span-12 md:col-span-4">
            <CardContent>
              <h2 class="text-lg font-semibold text-center pb-2">{{ grupo.nome }}</h2> 
              <div v-for="(presente, indexPresente) in grupo.presentes" :key="indexPresente" class="flex items-center gap-2 pb-2">
                <Checkbox :id="`presente${indexPresente}`" v-model:checked="presente.selecionado" :disabled="presente.disabled" @update:checked="aoSelecionarPresente(presente.id)"/>
                <div :for="`presente${indexPresente}`" class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70">{{ presente.nome }} </div>
              </div>
            </CardContent>
          </Card>
        </div>
      </ScrollArea>
      <div class="flex justify-center">
        <Button @click="dialogListaPresente = false" class="w-2/6">Ok</Button>
      </div>
    </DialogContent>
  </Dialog>
  <Dialog v-model:open="alerta">
    <DialogContent class="bg-[#cdc4b3] font-PlayfairDisplay">
      <DialogHeader>
        <DialogTitle class="text-center">Alerta!</DialogTitle>
      </DialogHeader>
      <DialogDescription>
        Esta pessoa já foi cadastrada. Deseja editar as informações deste cadastro?
      </DialogDescription>
      <div class="flex justify-center gap-4">
        <Button @click="alerta = false" class="w-2/6 bg-red-300">Não</Button>
        <Button @click="editarConvidado" class="w-2/6 bg-green-300">Sim</Button>
      </div>
    </DialogContent>
  </Dialog>
  <Dialog v-model:open="alertaOk">
    <DialogContent class="bg-[#cdc4b3] font-PlayfairDisplay">
      <DialogHeader>
        <DialogTitle class="text-center">Cadastrado com sucesso!</DialogTitle>
      </DialogHeader>
      <div class="flex justify-center gap-4">
        <Button @click="alertaOk = false" class="w-2/6">Ok</Button>
      </div>
    </DialogContent>
  </Dialog>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription } from '@/components/ui/dialog'
import { Checkbox } from '@/components/ui/checkbox'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import { ScrollArea } from '@/components/ui/scroll-area'
import { Label } from '@/components/ui/label'
import { RadioGroup, RadioGroupItem } from '@/components/ui/radio-group'
import Caderno from '@/components/Caderno.vue'
import Foto from '@/components/Foto.vue'
import { createClient } from '@supabase/supabase-js'

const lista = ref([])
const dialogListaPresente = ref(false)
const screenWidth = ref(window.innerWidth)
const screenHeight = ref(window.innerHeight)
const alerta = ref(false)
const alertaOk = ref(false)
const ehEditar = ref(false)
const convidado = ref({
  nome: '',
  mensagem: '',
  presente: true,
  presentes: []
})

const aoSelecionarPresente = (presenteId) => {
  const index = convidado.value.presentes.findIndex(p => p === presenteId)
  if (index === -1) {
    convidado.value.presentes.push(presenteId)
  } else {
    convidado.value.presentes.splice(index, 1)
  }
}
const abrirListaPresente = () => {
  dialogListaPresente.value = true
}
const supabase = createClient('https://acfrcmkzzabbqtwchiow.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFjZnJjbWt6emFiYnF0d2NoaW93Iiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTczMDQ3NzE3OCwiZXhwIjoyMDQ2MDUzMTc4fQ.ZoWVFkjTxFJL5ox3Zb-R4hgk7t6ia9T639aJEFZF4js')

const agruparPorGrupo = (presentes) => {
  return presentes.reduce((acc, presente) => {
    const {id, grupo, nome, qtde } = presente
    if (!acc[grupo]) {
      acc[grupo] = { nome: grupo, presentes: [] }
    }
    acc[grupo].presentes.push({id, nome, qtde: ref(qtde), selecionado: ref(qtde === 0), disabled: ref(qtde === 0)})
    return acc
  }, {})
}
const enviar = async () => {  
  let convidadoInterno
  if (ehEditar.value) {
    const { data, error } = await supabase.from('convidado').update({ mensagem: convidado.value.mensagem, presente: convidado.value.presente }).eq('nome', convidado.value.nome).select()
    await supabase.from('convidadoPresente').delete().eq('convidadoId', data[0].id)
    convidadoInterno = data[0]
  } else {
    const { data, error } = await supabase.from('convidado').insert([{ nome: convidado.value.nome, mensagem: convidado.value.mensagem, presente: convidado.value.presente }]).select()
    if (error && error.code === '23505' ) {
      alerta.value = true
      return
    }
    convidadoInterno = data[0]
  }
  await supabase.from('convidadoPresente').insert(convidado.value.presentes.map(p => ({convidadoId: convidadoInterno.id, presenteId: p})))
  convidado.value = {
    nome: '',
    mensagem: '',
    presente: true,
    presentes: []
  }
  ehEditar.value = false
  await desabilitaPresente()
  alertaOk.value = true
}
const desabilitaPresente = async () => {
  const { data: convidadosPresentes } = await supabase.from('convidadoPresente').select("*")
  for (const convidadoPresente of convidadosPresentes) {
    for (const key in lista.value) {
      const presentes = lista.value[key].presentes
      const presentesConvidado = presentes.filter(p => p.id === convidadoPresente.presenteId)
      for (const presente of presentesConvidado) {
        presente.qtde -= 1
        if (ehEditar && convidado.value.presentes.some(p => p === presente.id)) {
          presente.selecionado = true
          presente.disabled = false
        } else if (presente.qtde <= 0) {
          presente.selecionado = true
          presente.disabled = true
        }
      }
    }
  }
}
const editarConvidado = async () => {
  ehEditar.value = true
  const { data: convidadoData } = await supabase.from('convidado').select("*").eq('nome', convidado.value.nome)
  const convidadoInterno = convidadoData[0]
  const { data: convidadoPresenteData } = await supabase.from('convidadoPresente').select("*").eq('convidadoId', convidadoInterno.id)
  const presentes = convidadoPresenteData.map(cp => (cp.presenteId))
  convidado.value = {
    nome: convidadoInterno.nome,
    mensagem: convidadoInterno.mensagem,
    presente: convidadoInterno.presente,
    presentes
  }
  for (const item in lista.value) {
    for (const item2 of lista.value[item].presentes) {
      const index = presentes.findIndex(p => p === item2.id)
      if (index >= 0) {
        item2.selecionado = true
      }
    }
  }
  await desabilitaPresente()
  dialogListaPresente.value = true
  alerta.value = false
}
onMounted(async () => {
  window.addEventListener('resize', () => {
    screenWidth.value = window.innerWidth
    screenHeight.value = window.innerHeight
  })
  const { data, error } = await supabase.from('presente').select('*').order('nome')
  lista.value = agruparPorGrupo(data)
  await desabilitaPresente()
})
</script>