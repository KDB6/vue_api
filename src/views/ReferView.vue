<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Reference" name2="API" />

    <section className="cont__refer">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list">
            <li v-for="refer in refers" :key="refer.cssRefer">
              <a href="/">
                <span class="num">{{ refer.num }}</span>
                <span class="name">{{ refer.title }}</span>
                <span class="desc">{{ refer.desc }}</span>
                <span class="star">{{ refer.descStar }}</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </section>

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
        "https://raw.githubusercontent.com/KDB6/react_api/main/src/utils/reference.json"
      )
        .then((response) => response.json())
        // .then((result) => console.log(result.cssRefer))
        .then((result) => (refers.value = result.cssRefer))
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

<style lang="scss">
.refer__inner {
  font-family: "JejuMyeongjo";
  padding-bottom: 100px;

  h2 {
    font-size: 30px;
    color: var(--dark);
    font-family: var(--font-main);
  }
}

.refer__list {
  border: 1px solid var(--bg-dark-border);

  li {
    border-bottom: 1px solid var(--bg-dark-border);

    a {
      display: flex;
      align-items: center;
      width: 100%;
      color: var(--dark);
      font-family: var(--font-main);

      span {
        display: inline-block;
        padding: 15px 20px;
      }

      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-dark-border);
      }
      .name {
        flex: 1 1 20%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-dark-border);
        font-family: var(--font-kor);
      }
      .star {
        flex: 1 1 10%;
        text-align: center;
      }
    }
  }
}
</style>
