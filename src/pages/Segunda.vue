<script setup>
import { ref, onMounted, computed, watch } from "vue";
import Grafico from "../components/Grafico.vue";
import dadosIbama from "../assets/Ibama.json";
import imagem from "../assets/ibama-logo-1.png";
import imagem01 from "../assets/fiscalizacao.jpg";
import imagem02 from "../assets/mulherIbama.jpg";
import imagem03 from "../assets/ibama3.png";
import imagem04 from "../assets/fiscamato.jpg";
import imagem05 from "../assets/Presidente.jpg";
import imagem06 from "../assets/policia.jpg";

const dados = dadosIbama;
const tiposReceita = ref([]);
const receitaSelecionada = ref("Selecione o tipo de receita");

//função que separa e seleciona as receitas
const separaReceita = () => {
  //pega um array com todos os tipos de receita
  dados.data.forEach((item) => {
    if (!tiposReceita.value.includes(item.receita)) {
      tiposReceita.value.push(item.receita);
    }
  });
  //coloca só os tipos de receita que tem mais de 7 anos
  let newTiposReceita = [];
  tiposReceita.value.forEach((item) => {
    let selecionada = dados.data.filter((i) => i.receita == item);
    if (selecionada.length >= 8) {
      newTiposReceita.push(item);
    }
  });
  //coloca os tipos de receita no ref
  tiposReceita.value = newTiposReceita;
};

//computed para pegar os anos de cada receita selecionada
const xAxis = computed(() => {
  if (receitaSelecionada.value != "Selecione o tipo de receita") {
    return dados.data
      .filter((item) => item.receita == receitaSelecionada.value)
      .map((item) => item.ano);
  }
  return [];
});

//computed para pegar os valores de cada receita selecionada
const yAxis = computed(() => {
  if (receitaSelecionada.value != "Selecione o tipo de receita") {
    return dados.data
      .filter((item) => item.receita == receitaSelecionada.value)
      .map((item) => item.valor);
  }
  return [];
});

//array de botoes para o texto do corpo
const botoes = ref([
  {
    nome: "Proteção animal",
    estado: true,
    classe: "",
  },
  {
    nome: "Proteção Da Flora",
    estado: false,
    classe: "",
  },
  {
    nome: "Atuação Politica",
    estado: false,
    classe: "",
  },
]);

//array de texto do corpo
const textoBotoes = ref([
  {
    classe: "flex flex-col p-6 border border-solid border-white rounded-md text-center border border-solid rounded-lg border-yellow-300",
    estado: true,
    textos: [
      {
        texto:
          "Uma das principais atribuições do Ibama é combater o tráfico ilegal de animais silvestres, uma atividade criminosa que ameaça a biodiversidade e coloca em risco diversas espécies. O instituto atua na fiscalização de criadores, comerciantes e transportadores de animais silvestres, bem como na repressão de atividades ilícitas e na apreensão dos animais contrabandeados.",
        classeTexto: "flex text-xl text-white mb-14 items-center",
        srcImagem: imagem01,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg ml-5",
      },
      {
        texto:
          "Além disso, o Ibama também é responsável por autorizar e regulamentar atividades que envolvam a captura, criação e manejo de animais silvestres em cativeiro, com o objetivo de garantir o bem-estar dos animais e evitar práticas prejudiciais à sua saúde e integridade.",
        classeTexto: "flex flex-row-reverse text-xl text-white items-center",
        srcImagem: imagem02,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg mr-5",
      },
    ],
  },
  {
	    classe: "flex flex-col p-6 border border-solid border-white rounded-md text-center border border-solid rounded-lg border-yellow-300",
    estado: false,
    textos: [
	{
        texto:
          "IBAMA tem um papel fundamental na proteção da flora no Brasil, órgão atua na conservação dos ecossistemas, no combate ao desmatamento ilegal, na promoção do uso sustentável dos recursos florestais e na preservação de espécies ameaçadas.",
        classeTexto: "flex text-xl text-white mb-14 items-center",
        srcImagem: imagem03,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg ml-5",
      },
      {
        texto:
          "Trabalha em conjunto com outros órgãos, como o Instituto Chico Mendes de Conservação da Biodiversidade, e estabelece parcerias com instituições e comunidades locais para fortalecer a proteção da flora no Brasil.",
        classeTexto: "flex flex-row-reverse text-xl text-white items-center",
        srcImagem: imagem04,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg mr-5",
      },
    ],
  },
  {
    classe: "flex flex-col p-6 border border-solid border-white rounded-md text-center border border-solid rounded-lg border-yellow-300",
    estado: false,
    textos: [
	{
        texto:
          "Uma das principais formas de atuação política do Ibama é na elaboração de regulamentações e normas ambientais. O instituto contribui na criação de leis e decretos relacionados à proteção da fauna, à conservação dos ecossistemas, ao controle da poluição e a outras questões ambientais relevantes. Essas normas são fundamentais para orientar ações governamentais e estabelecer diretrizes para a proteção animal e a preservação ambiental.",
        classeTexto: "flex text-xl text-white mb-14 items-center",
        srcImagem: imagem05,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg ml-5",
      },
      {
        texto:
          "Outra forma de atuação política do Ibama é por meio da participação em fóruns, conferências e negociações internacionais relacionadas ao meio ambiente. O instituto representa o Brasil em discussões sobre biodiversidade, mudanças climáticas, conservação marinha e outras pautas ambientais de relevância global. Essa participação permite ao Ibama contribuir para a definição de políticas internacionais e a adoção de medidas que promovam a proteção dos animais e do meio ambiente em escala global.",
        classeTexto: "flex flex-row-reverse text-xl text-white items-center",
        srcImagem: imagem06,
        classImagem: "w-65 h-48 hover:scale-110 rounded-lg mr-5",
      },
    ],
  },
]);

//função para mudar o estado do botão
const mudaEstado = (val, index) => {
  for (var i = 0; i < val.length; i++) {
    if (i == index) {
      val[i].estado = true;
      continue;
    }
    val[i].estado = false;
  }
};

onMounted(() => {
  separaReceita();
  mudaEstado(botoes.value, 0);
});
</script>

<template>
  <div class="bg-gray-950 min-h-screen h-full pb-96">
    <RouterLink
      to="/"
      class="sticky top-4 ml-4 btn font-bold rounded-full bg-gray-100 text-black normal-case text-xl hover:bg-white z-50 mt-4"
      >{{ "<" }}</RouterLink
    >
    <div
      class="flex flex-col justify-between content-center px-12 text-white text-xl"
    >
      <h2 class="text-green-500 text-center text-3xl font-bold mb-28">
        O QUE É O IBAMA?
      </h2>
	  
      <div class="flex flex-col justify-around mb-40 items-center m-0 sm:flex-row">
        <p class="w-[70%] leading-10 text-justify text-2xl">
          O Instituto Brasileiro do Meio Ambiente e dos Recursos Naturais
          Renováveis <strong class="text-green-500">(IBAMA)</strong> foi criado
          em 1989, por meio da Lei nº 7.735, com o objetivo de unificar e
          fortalecer as ações de proteção e conservação do meio ambiente no
          Brasil. Desde sua criação, o IBAMA tem desempenhado um papel essencial
          na
          <strong class="text-green-500">proteção ambiental do país.</strong> O
          órgão atua em âmbito nacional, sendo vinculado ao Ministério do Meio
          Ambiente, e possui uma estrutura descentralizada, com escritórios
          regionais em todo o território brasileiro. Ao longo de sua história, o
          IBAMA tem enfrentado diversos
          <strong class="text-green-500">desafios</strong> e desenvolvido ações
          para combater crimes ambientais, promover a conservação da
          biodiversidade e assegurar o uso sustentável dos recursos naturais.
        </p>
        <img src="../assets/brasil.png" alt="brasil" class="w-44 h-44 mt-12 sm:mt-0" />
      </div>
      <div class="flex m-4  justify-around flex-col items-center sm:flex-row items-baseline">
        <div class="flex relative top-7">
          <span class="text-green-500 font-bold text-5xl text-center"
            >1.87<br />BILHÃO</span
          >
          <span class="text-green-500 font-bold text-8xl ml-2">R$</span>
        </div>
        <div class="flex flex-col w-full">
          <p class="w-full text-2xl leading-10 mb-10 ml-6 m-4 mt-20 sm:mt-0">
            O orçamento do IBAMA é direcionado para diversas áreas fundamentais
            na preservação do meio ambiente. Mas como esse recurso é dividido?
            Explore o gráfico abaixo para compreender melhor a distribuição das
            receitas do IBAMA durante os anos.
          </p>
          <div class="flex w-full h-full justify-center m-4">
            <div class="flex justify-center">
              <select
                v-model="receitaSelecionada"
                class="select select-bordered w-full max-w-xs mr-2 text-black"
              >
                <option disabled selected>Selecione o tipo de receita</option>
                <option
                  v-for="(tipoReceita, index) in tiposReceita"
                  :key="index"
                >
                  {{ tipoReceita }}
                </option>
              </select>
              <Grafico
                :xAxis="xAxis"
                :yAxis="yAxis"
                :label="receitaSelecionada"
                :key="receitaSelecionada"
              />
            </div>
          </div>
        </div>
      </div>

      <div class="flex flex-col items-center mt-24">
        <h2 class="text-yellow-300 text-3xl font-bold">ATUAÇÕES DO IBAMA</h2>
        <p class="mt-16 text-2xl w-[90%] leading-10">
          O IBAMA, Instituto Brasileiro do Meio Ambiente e dos Recursos Naturais
          Renováveis, é responsável por implementar e fazer cumprir as políticas
          ambientais do Brasil. Sua atuação é vasta, incluindo proteção da fauna
          e flora, bem como representação política. Clique nos botões abaixo
          para entender melhor sobre cada uma das
          <strong class="text-yellow-300">ações principais</strong> do IBAMA.
        </p>
      </div>

      <div class="flex flex-col mt-12 mb-44">
        <div class="flex justify-around mb-12 flex-col sm:flex-row">
          <button
            v-for="(botao, index) in botoes"
            @click="mudaEstado(botoes, index), mudaEstado(textoBotoes, index)"
            :class="(botao.estado ? 'bg-white text-black' : '' ) + botao.classe "
            class="btn m-3 sm:m-0"
          >
            {{ botao.nome }}
          </button>
        </div>
        <div v-for="(texto, index) in textoBotoes" :key="index" class="flex">
          <transition
            enter-active-class="duration-200 ease-out"
            enter-from-class="transform opacity-0"
            enter-to-class="opacity-200"
            leave-active-class="duration-200 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="transform opacity-0 "
          >
            <div
              class="absolute w-[calc(100vw-100px)]"
              v-show="texto.estado"
              :class="texto.classe"
              :key="index"
            >
              <div v-for="(bloco, index) in texto.textos" :key="index" :class="bloco.classeTexto">
                <span class="w-[90%]"
                  >{{ bloco.texto }}
                </span>
                <img :src="bloco.srcImagem" :class="bloco.classImagem" />
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
