<template>
  <div>
    <nuxt-link
      :to="{ name: 'index' }"
      style="display: flex; justify-content: center;">PC</nuxt-link>
    <p style="padding: 0px 10px;display: flex; justify-content: center;">  |  </p> 
    <nuxt-link
      :to="{ name: 'sp' }"
      style="display: flex; justify-content: center;">SP</nuxt-link>
  </div>
</template>