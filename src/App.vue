<script setup lang="ts">
import { ref } from "vue";
import { useClipboard } from "@vueuse/core";
import {
  CheckCircleIcon,
  AtSymbolIcon,
  SunIcon,
  MoonIcon,
} from "@heroicons/vue/24/outline";
import { isDark, toggleTheme } from "./services/useDarkMode";

const email = ref("info@webyourself.ch");
const { isSupported, copy, copied } = useClipboard();
</script>

<template>
  <div class="webyourself h-screen w-full grid place-items-center bg-base-300">
    <div class="absolute top-5 right-5">
      <button class="btn btn-ghost btn-square" @click="toggleTheme()">
        <MoonIcon v-if="isDark" class="h-6 w-6" />
        <SunIcon v-else class="h-6 w-6" />
      </button>
    </div>

    <div class="card w-full sm:w-96 bg-base-100 shadow-xl">
      <figure class="px-10 pt-10">
        <div
          class="w-full h-56 grid place-items-center rounded-xl bg-wy box"
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
              <AtSymbolIcon v-if="!copied" class="h-6 w-6 mr-2" />

              <CheckCircleIcon v-else class="h-6 w-6 mr-2" />

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
