<template>
<!--
  <amplify-greetings></amplify-greetings>
  -->
  <div v-if="isSignedIn">
    <amplify-greetings></amplify-greetings>
   <router-link custom v-slot="{ navigate }" :to="{ name: 'AlbumIndex' }">
     <button @click="navigate">TOP</button>
   </router-link>    
  </div>

  <router-view/>
</template>

<script>
export default {
  computed: {
    isSignedIn(){
      return this.$store.state.user !== null;
    },
  },
};
</script>

