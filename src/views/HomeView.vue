<script setup>
import { RouterLink } from 'vue-router'
</script>
<template>
  <!-- Masthead -->
  <header class="masthead">
      <div class="container px-4 px-lg-5 d-flex h-100 align-items-center justify-content-center">
                <div class="d-flex justify-content-center">
                    <div class="text-center">
                        <h1 class="mx-auto my-0 text-uppercase">Weather</h1>
                        <h2 class="text-white-50 mx-auto mt-2 mb-5">สภาพอากาศเป็นอย่างไรบ้าง?</h2>
                        <RouterLink to="/weather"><button class="btn btn-primary">Check it</button></RouterLink>
                    </div>
                </div>
            </div>
    </header>
</template>