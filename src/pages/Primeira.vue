<script setup>

</script>

<template>
  <div class="flex flex-col justify-between bg-green-600 w-full min-h-screen">
    <div class="text-center mt-12 w-full">
      <span class="text-center font-bold text-transparent bg-clip-text bg-gradient-to-b from-lime-300 to-yellow-300 text-[7rem] sm:text-[10rem] lg:
      text-[13rem]">IBAMA</span>

      <div class="text-center flex h-full mb-12">
        <span class="font-bold text-5xl mx-auto text-lime-300 lg: text-4xl">
          Instituto Brasileiro do Meio Ambiente e dos Recursos Naturais
          Renovaveis
        </span>
      </div>
    </div>
    <div class="flex justify-center mb-4 lg: mb-0">
      <router-link
        to="/inf"
        class="btn w-40 h-16 text-white border border-solid border-white text-lg"
        >Saiba mais</router-link
      >
    </div>
    <div class="flex justify-between p-4 flex-col sm:flex-row items-center">
      <img src="../assets/ibama-logo-1.png" class="mt-auto w-32 h-32 mb-7 sm:mb-0" />
      <img src="../assets/efcf9caf-6d29-4c24-8266-0b7366ea3a40.png" class="mt-auto w-72" />
    </div>
  </div>
</template>

<style scoped></style>
