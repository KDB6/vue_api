<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Reference" name2="API" />
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const refers = ref([]);

    const references = () => {
      fetch(
        "https://raw.githubusercontent.com/KDB6/main/vue_api/src/utils/reference.json"
      )
        .then((response) => response.json())
        .then((result) => console.log(result))
        .catch((error) => console.log("error", error));
    };
    references();

    return {
      refers,
      references,
    };
  },
};
</script>
