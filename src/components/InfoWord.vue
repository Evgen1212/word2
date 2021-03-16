<template>
  <div
    class="parent"
    :class="{ active: isActive }"
    @click="isActive = !isActive"
  >
    <span class="word">{{ keepWord.meta.stems[0] }}</span>
    <span class="fl"> {{ keepWord.fl }} </span>
    <span class="ant_list">"{{ keepWord.def[0].sseq[0][0][1].dt[0][1] }}"</span>
  </div>
</template>

<script>
export default {
  name: "InfoWord",
  props: ["keepWord"],
  data() {
    return {
      isActive: false,
    };
  },
};
</script>

<style scoped>
.parent {
  height: 28px;
  overflow: hidden;
}
.active {
  overflow: auto;
  height: auto;
}
.word {
  font-size: 25px;
  font-weight: 600;
}
.fl {
  font-size: 24px;
  font-style: italic;
  padding: 0 15px;
}
.ant_list {
  font-size: 20px;
}
</style>
