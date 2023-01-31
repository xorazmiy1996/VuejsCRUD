<template>
  <div class="btn-group">
    <buttton v-for="btn in filterButtons" :key="btn.name" class="btn"
             :class="[filterName == btn.name ? 'btn-dark':'btn-outline-dark']"
             @click="filterHandler(btn.name)"

    >
      {{ btn.title }}
    </buttton>
    <!--    <button class="btn"-->
    <!--            type="button"-->
    <!--            @click="filterHandler('all')"-->
    <!--            :class="[filterName == 'all' ? 'btn-dark':'btn-outline-dark']"-->
    <!--    >-->
    <!--      Barcha kinolar-->
    <!--    </button>-->
    <!--    <button class="btn"-->
    <!--            type="button"-->
    <!--            @click="filterHandler('popular')"-->
    <!--            :class="[filterName == 'popular' ? 'btn-dark':'btn-outline-dark']"-->
    <!--    >-->
    <!--      Mashxur kinolar-->
    <!--    </button>-->
    <!--    <button class="btn"-->
    <!--            type="button"-->
    <!--            @click="filterHandler('mostViewers')"-->
    <!--            :class="[filterName == 'mostViewers' ? 'btn-dark':'btn-outline-dark']"-->
    <!--    >-->
    <!--      Eng ko'p ko'rilgan kinolar-->
    <!--    </button>-->

  </div>
</template>

<script>
export default {
  name: "AppFilter",
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    }
  },
  data() {
    return {
      filter: 'all',
      filterButtons: [
        {name: 'all', title: "Barcha kinolar"},
        {name: 'popular', title: "Mashxur kinolar"},
        {name: 'mostViewers', title: " Eng ko'p ko'rilgan kinolar"},
      ],
    }
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter
      this.updateFilterHandler(this.filter)


    }
  }
}
</script>

<style scoped>

</style>