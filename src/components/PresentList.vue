<template>
  <ScrollArea class="h-full">
    <div class="grid grid-cols-2 md:grid-cols-3 gap-8">
      <div v-for="category in categories" :key="category.title" class="bg-white p-6 rounded-lg shadow">
        <h2 class="text-lg font-semibold mb-4 text-center border-b border-gray-300 pb-2">{{ category.title }}</h2>
        <ul class="space-y-2">
          <li v-for="item in category.items" :key="item" class="flex items-center">
            <span class="mr-2">•</span>
            <span>{{ item }}</span>
          </li>
        </ul>
      </div>
    </div>
  </ScrollArea>
</template>

<script setup>
import { ScrollArea } from '@/components/ui/scroll-area'

const categories = [
  {
    title: "Cozinha",
    items: [
      "Abridor de lata", "Açucareiro", "Formas e assadeiras", "Afiador de facas",
      "Panela de pressão", "Descanso de panelas", "Conjunto de xícaras", "Porta condimentos",
      "Espremedor", "Leiteira", "Copo de medida", "Ralador", "Saca rolhas",
      "Pegador de macarrão", "Porta papel toalha", "Porta guardanapo", "Manteigueira",
      "Panos de prato", "Avental", "Lixeiras de cozinha", "Chaleira", "Colher de pau",
      "Colher de sorvete", "Concha", "Jogo de panelas, pratos e talheres", "Cortador de queijo",
      "Escorredor de louça/macarrão/talheres", "Escumadeira", "Faca de pão", "Frigideira",
      "Tábua para cortes", "Potes multiuso", "Jarra", "Garrafa térmica", "Luva térmica",
      "Porta detergente e esponja", "Pano de chão tipo saco", "Conjunto para sobremesa",
      "Toalha de mesa", "Rodinho de pia", "Ralador", "Saleiro", "Jogo americano"
    ]
  },
  {
    title: "Sala",
    items: [
      "Cortina para sala", "Mesa de centro", "Prateleiras", "Luminária",
      "Mantas e almofadas", "Tapete", "Quadros decorativos", "Suporte para televisão",
      "Capa para sofá"
    ]
  },
  {
    title: "Banheiro",
    items: [
      "Porta escova de dentes", "Tapete antiderrapante para box", "Cortina para banheiro",
      "Toalha para mãos", "Toalhas de banho", "Toalhas de rosto", "Capacho",
      "Cesto para roupa", "Escova para vaso sanitário", "Lixeira", "Saboneteira", "Roupão"
    ]
  },
  {
    title: "Área de Serviço",
    items: [
      "Baldes de plástico", "Pá de lixo", "Pano de chão", "Porta sabão",
      "Pregadores de roupa", "Rodo", "Vassouras", "Esfregão", "Escovinha de limpeza"
    ]
  },
  {
    title: "Itens Decorativos",
    items: [
      "Espelhos", "Almofadas", "Luminárias", "Relógio de parede", "Porta chaves",
      "Aparador de livros", "Porta retrato", "Vela aromatizadora", "Difusor", "Vasos decorativos"
    ]
  }
]
</script>

<style scoped>
</style>
