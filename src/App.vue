<template>
  <div id="app">
    <div class="header">
      <div>
        <input type="radio" id="keep" value="Word Keeper" v-model="picked" />
        <label for="keep"> Word Keeper</label>
      </div>
      <div>
        <input type="radio" id="starr" value="Starred Words" v-model="picked" />
        <label for="starr"> Starred Words</label>
      </div>
    </div>

    <div v-if="picked == 'Word Keeper'" class="content">
      <div class="content_wrap">
        <div class="search_wrap">
          <div class="word_search">
            <input type="text" v-model="searchWord" @input="GetData()" />
          </div>
        </div>
        <div
          class="word_list"
          v-if="!(keepWords == 'Word is required.' || keepWords == '')"
        >
          <div
            class="word_item"
            v-for="(item, index) in keepWords"
            :key="index"
          >
            <div class="word_hint" v-if="!item.meta" @click="SetWord">
              {{ item }}
            </div>

            <div v-if="item.meta" class="word_info">
              <InfoWord :keepWord="item" />
              <input type="checkbox" :value="item" v-model="saveWords" />
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-if="picked == 'Starred Words'" class="content">
      <div class="content_wrap">
        <div class="search_wrap">
          <div class="word_search">
            <input v-model="searchStarredWord" type="text" />
          </div>
          <label class="word_searching"
            ><input type="checkbox" value="adjective" v-model="showWord" />
            adjective</label
          >
          <label class="word_searching"
            ><input type="checkbox" value="noun" v-model="showWord" />
            noun</label
          >
          <label class="word_searching"
            ><input type="checkbox" value="verb" v-model="showWord" />
            verb</label
          >
        </div>
        <div class="word_list">
          <div v-if="showWord.length == 0">
            <draggable v-model="saveWords">
              <transition-group>
                <div
                  class="word_item"
                  v-for="item in saveWords"
                  :key="item.meta.id"
                >
                  <div v-show="item.meta.id.indexOf(searchStarredWord) >= 0">
                    <div class="word_info">
                      <InfoWord :keepWord="item" />
                      <input
                        type="checkbox"
                        :value="item"
                        v-model="saveWords"
                      />
                    </div>
                  </div>
                </div>
              </transition-group>
            </draggable>
          </div>
          <div v-else>
            <draggable v-model="saveWords">
              <transition-group>
                <div
                  class="word_item"
                  v-for="item in saveWords"
                  :key="item.meta.id"
                >
                  <div
                    v-show="
                      item.meta.id.indexOf(searchStarredWord) >= 0 &&
                      showWord.includes(item.fl)
                    "
                  >
                    <div class="word_info">
                      <InfoWord :keepWord="item" />
                      <input
                        type="checkbox"
                        :value="item"
                        v-model="saveWords"
                      />
                    </div>
                  </div>
                </div>
              </transition-group>
            </draggable>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import InfoWord from "@/components/InfoWord.vue";
import draggable from "vuedraggable";
export default {
  name: "App",
  components: { InfoWord, draggable },
  data() {
    return {
      picked: "",
      searchWord: "",
      keepWords: null,
      searchStarredWord: "",
      saveWords: [],
      showWord: [],
    };
  },
  // watch: {
  //   picked() {
  //     localStorage.setItem("picked", this.picked);
  //   },
  //   saveWords() {
  //     localStorage.setItem("save-words", JSON.stringify(this.saveWords));
  //   },
  //   searchWord() {
  //     localStorage.setItem("search-word", this.searchWord);
  //   },
  //   showWord() {
  //     localStorage.setItem("show-word", JSON.stringify(this.showWord));
  //   },
  // },
  // created() {
  //   this.saveWords = JSON.parse(localStorage.getItem("save-words"));
  //   this.searchWord = localStorage.getItem("search-word");

  //   this.picked = localStorage.getItem("picked");
  //   this.GetData();
  //   this.showWord = JSON.parse(localStorage.getItem("show-word"));
  // },
  methods: {
    GetData() {
      this.$axios
        .get(
          "https://dictionaryapi.com/api/v3/references/thesaurus/json/" +
            this.searchWord +
            "?key=a1c59a22-cd0f-4c34-bd07-9cd3bc9b076c"
        )
        .then((response) => {
          console.log(response.data);
          //"выдача первых 10 слов списком"
          if (
            response.data.length >= 10 &&
            response.data !== "Word is required."
          ) {
            this.keepWords = response.data.slice(0, 10);
          } else this.keepWords = response.data;
        });
    },
    SetWord(e) {
      this.searchWord = e.target.innerText;
      this.GetData();
    },
  },
  computed: {},
};
</script>

<style>
.red {
  background: red;
}
#app {
  max-width: 1000px;
  margin: 0 auto;
  background: rgb(234 231 231 / 66%);
}
.header {
  font-family: "Times New Roman", Times, serif;
  font-size: 28px;
  color: aliceblue;
  display: flex;
  justify-content: space-between;
  background-color: #03a8f4a2;
  border-radius: 5px;
  padding: 15px 100px;
}
.content {
  margin-top: 25px;
}
.content_wrap {
  display: flex;
  justify-content: space-between;
}
.search_wrap {
  padding: 25px;
  background: rgb(234 231 231 / 66%);
}
.word_list {
  display: flex;
  flex-direction: column;
}
.word_item {
  max-width: 700px;
}
.word_searching {
  display: block;
  font-size: 24px;

  padding: 0 15px;
}
.word_info {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 5px 15px;
  margin: 5px 0px;
  background: white;
}
.word_hint {
  cursor: pointer;
  margin-right: 250px;
  font-size: 25px;
  font-weight: 600;
  font-family: sans-serif;
  font-style: inherit;
  color: #31333585;
}
</style>
