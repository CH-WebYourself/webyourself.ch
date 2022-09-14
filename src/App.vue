<script setup lang="ts">
import { ref } from "vue";
import { useClipboard } from "@vueuse/core";
import { isDark, toggleTheme } from "./services/useDarkMode";

const email = ref("info@webyourself.ch");
const { isSupported, copy, copied } = useClipboard();
</script>

<template>
  <div class="webyourself h-screen w-full grid place-items-center bg-base-300">
    <div class="card w-full sm:w-96 bg-base-100 shadow-xl">
      <figure class="px-10 pt-10">
        <div
          class="w-full h-36 grid place-items-center rounded-xl bg-wy box"
          :class="{ circle: isDark }"
        >
          <img
            src="./assets/webyourself.png"
            alt="Webyourself Logo"
            class="w-32"
          />
        </div>
      </figure>
      <div class="card-body items-center text-center">
        <h2 class="card-title">Webseiten für alle!</h2>
        <p>
          Unser Team nimmt im Moment keine Aufträge an. Für Fragen geben wir
          gerne per Email auskunft. Klicken Sie dazu auf den untenstehenden
          Knopf, um unsere Email-Adresse zu kopieren.
        </p>

        <div class="card-actions mt-5">
          <div v-if="isSupported">
            <button class="btn btn-outline" @click="copy(email)">
              <svg
                v-if="!copied"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 mr-2"
              >
                <path
                  stroke-linecap="round"
                  d="M16.5 12a4.5 4.5 0 11-9 0 4.5 4.5 0 019 0zm0 0c0 1.657 1.007 3 2.25 3S21 13.657 21 12a9 9 0 10-2.636 6.364M16.5 12V8.25"
                />
              </svg>

              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 mr-2"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                />
              </svg>

              <span v-if="!copied">Email-Adresse kopieren</span>
              <span v-else>Email-Adresse kopiert</span>
            </button>
          </div>
          <p v-else>Ihr Browser unterstützt die Clipboard API nicht</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.box {
  clip-path: circle(75%);
  transition: clip-path 0.25s;
}

.circle {
  clip-path: circle(25%);
}
</style>
