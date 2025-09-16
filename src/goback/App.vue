<template>
  <card-with-logo>
    <template v-slot:header>
      <div class="md-title">{{ randomImage.text }}</div>
    </template>
    <template v-slot:media>
      <img id="go-back-image" :src="randomImage.path" />
    </template>
  </card-with-logo>
</template>

<script>
import { localStorage } from "../chromeApiHelpers";
import CardWithLogo from "../sharedComponents/CardWithLogo";

const supportedLangs = ['en', 'fr', 'it'];
let langCode = navigator.language.slice(0, 2);
const userLang = supportedLangs.includes(langCode) ? langCode : 'en';

export default {
  name: "App",
  components: { CardWithLogo },
  mounted() {
    this.getRandomImage();
  },
  data() {
    return {
      imagesObjects: [
        {
          path: "images/access-blocked-websites.jpg",
          text: {
            en: "",
            fr: "",
            it: ""
          }
        },
        {
          path: "images/angry-monkey.jpg",
          text: {
            en: "Go Back to work now!",
            fr: "Retourne travailler !",
            it: "Torna al lavoro adesso!"
          }
        },
        {
          path: "images/Black-Girl-Wat.jpg",
          text: {
            en: "WAT are you doing here? Go to work",
            fr: "Qu'est-ce que tu fais ici ? Retourne travailler",
            it: "Cosa stai facendo qui? Torna al lavoro"
          }
        },
        {
          path: "images/troll.jpg",
          text: {
            en: "you didn't learn your lesson right? Go to work",
            fr: "Tu n'as pas retenu la leçon, n'est-ce pas ? Au travail !",
            it: "Non hai imparato la lezione? Torna al lavoro"
          }
        },
        {
          path: "images/angry-white-monkey.jpg",
          text: {
            en: "Goooooo!",
            fr: "Goooooo !",
            it: "Goooooo!"
          }
        },
        {
          path: "images/coffin-dance.jpg",
          text: {
            en: "Go to work or dance with us!",
            fr: "Travaille ou danse avec nous !",
            it: "Lavora o balla con noi!"
          }
        },
        {
          path: "images/spongebob.jpg",
          text: {
            en: "",
            fr: "",
            it: ""
          }
        },
        {
          path: "images/baby.jpg",
          text: {
            en: "",
            fr: "",
            it: ""
          }
        },
        {
          path: "images/can-you-please-just-go-away.png",
          text: {
            en: "",
            fr: "",
            it: ""
          }
        },
        {
          path: "images/we-dont-do-that-here.png",
          text: {
            en: "When you open a blocked website instead of working.",
            fr: "Quand tu ouvres un site bloqué au lieu de travailler.",
            it: "Quando apri un sito bloccato invece di lavorare."
          }
        },
        {
          path: "images/Surprised-Joey.jpg",
          text: {
            en: "When I see you trying to open a blocked website",
            fr: "Quand je te vois essayer d'ouvrir un site bloqué",
            it: "Quando ti vedo provare ad aprire un sito bloccato"
          }
        },
        {
          path: "images/ross.jpg",
          text: {
            en: "When I see you trying again and again to open a blocked website",
            fr: "Quand je te vois essayer encore et encore d'ouvrir un site bloqué",
            it: "Quando ti vedo provare ancora e ancora ad aprire un sito bloccato"
          }
        },
        {
          path: "images/chandler-oh-my-god.jpg",
          text: {
            en: "when you don't learn the lesson and break your work again",
            fr: "Quand tu ne retiens pas la leçon et recommences à ne pas travailler",
            it: "Quando non impari la lezione e rompi di nuovo il tuo lavoro"
          }
        },
        {
          path: "images/chandler-laugh.jpg",
          text: {
            en: "My face when I block a website for you",
            fr: "Ma tête quand je bloque un site pour toi",
            it: "La mia faccia quando blocco un sito per te"
          }
        }
      ],
      selectedImageIndex: 0,
      lang: userLang
    };
  },
  computed: {
    randomImage() {
      const img = this.imagesObjects[this.selectedImageIndex];
      return {
        path: img.path,
        text: img.text[this.lang] || img.text['en'] || ""
      };
    }
  },
  methods: {
    getRandomImage() {
      localStorage.get("settings").then(settings => {
        if (settings.allowFunnyGoBackImages) {
          this.selectedImageIndex = Math.floor(
            Math.random() * this.imagesObjects.length
          );
        }
      });
    }
  }
};
</script>

<style scoped>
#go-back-image {
  width: 95%;
}
</style>
