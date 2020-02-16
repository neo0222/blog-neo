<template>
  <div>
    <div>
      <TheHeader />
    </div>
    <DefaultLayout>
      <nuxt/>
    </DefaultLayout>
  </div>
</template>

<script>
import DefaultLayout from '~/components/DefaultLayout'
import TheHeader from '~/components/TheHeader'

export default {
  components: {
    DefaultLayout,
    TheHeader,
  }
}
</script>
