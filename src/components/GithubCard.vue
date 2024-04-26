<script setup>
import { ref } from 'vue';
const user = ref(null);
const props = defineProps({
  username: {
    type: String,
    required: true,
  },
});
// fetching data
fetch(`https://api.github.com/users/${props.username}`)
  .then(async (res) => {
    user.value = await res.json();
  }).catch((err) => {
    console.log(err);
  });
</script>

<template>
  <div v-if="user" class="m-5 card card-side bg-base-100 shadow-xl">
    <figure>
      <img
        :src="user.avatar_url"
        alt="Avatar Image"
      />
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ user.name }}</h2>
      <p>
        <strong>Seguidores:</strong> {{ user.followers }}
        <strong>Siguiendo:</strong> {{ user.following }}
      </p>
      <div class="card-actions justify-end">
        <a :href="user.html_url" class="btn btn-primary">Ver Perfil</a>
      </div>
    </div>
  </div>
</template>