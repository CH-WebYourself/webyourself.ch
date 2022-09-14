<script setup lang="ts">
import { ref } from "vue";
import { useClipboard } from "@vueuse/core";
import {
  CheckCircleIcon,
  AtSymbolIcon,
  SunIcon,
  MoonIcon,
  XMarkIcon,
} from "@heroicons/vue/24/outline";
import { isDark, toggleTheme } from "./services/useDarkMode";

const email = ref("info@webyourself.ch");
const { isSupported, copy, copied } = useClipboard();
</script>

<template>
  <div class="drawer">
    <input id="impressum-drawer" type="checkbox" class="drawer-toggle" />
    <div class="drawer-content">
      <div class="webyourself h-screen grid place-items-center bg-base-300">
        <div class="absolute top-5 right-5">
          <button class="btn btn-ghost btn-square" @click="toggleTheme()">
            <MoonIcon v-if="isDark" class="h-6 w-6" />
            <SunIcon v-else class="h-6 w-6" />
          </button>
        </div>

        <div class="absolute bottom-5 right-5">
          <label for="impressum-drawer" class="btn btn-ghost drawer-button">
            Impressum
          </label>
        </div>

        <div class="card w-full sm:w-96 bg-base-100 shadow-xl">
          <figure class="px-10 pt-10">
            <div
              class="w-full h-40 sm:h-56 grid place-items-center rounded-xl bg-wy box"
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
                  <span v-else>Erfolgreich kopiert</span>
                </button>
              </div>
              <p v-else>Ihr Browser unterstützt die Clipboard API nicht</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="drawer-side">
      <label for="impressum-drawer" class="drawer-overlay"></label>

      <div
        class="p-8 overflow-y-auto w-full sm:w-128 bg-base-100 text-base-content"
      >
        <div class="flex justify-between">
          <h2 class="text-2xl mb-5">Impressum</h2>
          <label
            for="impressum-drawer"
            class="btn btn-ghost btn-square drawer-button"
          >
            <XMarkIcon class="h-6 w-6" />
          </label>
        </div>

        <p class="mb-5">
          <span class="text-lg font-bold"> Kontakt </span>
          <br />
          <span>Webyourself</span><br />
          <span>Thomas Iseli</span><br />
          <span>Ali Shala</span>
        </p>

        <p class="mb-5">
          <span class="text-lg font-bold"> Technischer Kontakt </span>
          <br />
          <span class="mr-1">Thomas Iseli</span>
          <a
            href="https://github.com/CH-WebYourself/webyourself.ch"
            class="link link-hover"
            target="_blank"
            >GitHub
          </a>
          <br />
          <a
            href="https://webyourself.ch"
            class="link link-hover"
            target="_blank"
            >www.webyourself.ch
          </a>
        </p>

        <p class="mb-5">
          <span class="text-lg font-bold"> Haftungsausschluss </span>
          <br />
          Der Autor übernimmt keinerlei Gewähr hinsichtlich der inhaltlichen
          Richtigkeit, Genauigkeit, Aktualität, Zuverlässigkeit und
          Vollständigkeit der Informationen. Haftungsansprüche gegen den Autor
          wegen Schäden materieller oder immaterieller Art, welche aus dem
          Zugriff oder der Nutzung bzw. Nichtnutzung der veröffentlichten
          Informationen, durch Missbrauch der Verbindung oder durch technische
          Störungen entstanden sind, werden ausgeschlossen. Alle Angebote sind
          unverbindlich. Der Autor behält es sich ausdrücklich vor, Teile der
          Seiten oder das gesamte Angebot ohne gesonderte Ankündigung zu
          verändern, zu ergänzen, zu löschen oder die Veröffentlichung zeitweise
          oder endgültig einzustellen.
        </p>

        <p class="mb-5">
          <span class="text-lg font-bold"> Datenverwaltung </span>
          <br />
          Wir erheben keine personenbezogenen Daten, ausser nicht
          kateregorisierbaren Email-Adressen. Diese werden lediglich dazu
          verwendet, den registrierten Otaku-Mitgliedern eine Email mit einem
          Umfrageformular zukommen zu lassen.
        </p>
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
