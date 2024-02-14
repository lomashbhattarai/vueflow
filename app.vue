<script setup></script>

<template>
  <div class="node-graph-container">
    <!-- <NuxtWelcome /> -->
    <header>
      <nav>
        <ul>
          <li><NuxtLink to="/node">node graph</NuxtLink></li>
        </ul>
      </nav>
    </header>
    <NuxtPage />
  </div>
</template>

<style>
.node-graph-container {
  width: 100%;
  height: 100vh;
}
</style>
