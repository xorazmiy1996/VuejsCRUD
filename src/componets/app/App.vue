<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCoun="movies.length"
               :favoriteMoviesCount="movies.filter(c => c.favorite).length"
      />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler"/>
        <AppFilter :filterName="filter" :updateFilterHandler="updateFilterHandler" />
      </div>

      <MoveList :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
                @onToggle="onToggleHandler" @onRemove="onRemoveHandler"
      />
      <MoveAddForm @createMovie="createMovie"/>
    </div>


  </div>


</template>

<script>
import AppInfo from "@/componets/app-info/AppInfo.vue";
import SearchPanel from "@/componets/search-panel/SearchPanel.vue";
import AppFilter from "@/componets/app-filtter/AppFilter.vue";
import MoveList from "@/componets/move-list/MoveList.vue";
import MoveAddForm from "@/componets/move-add-form/MoveAddForm.vue";

export default {
  components: {
    MoveAddForm,
    MoveList,
    AppFilter,
    SearchPanel,
    AppInfo,
  },

  data() {
    return {
      movies: [
        {id: 1, name: "Muhammad", viewers: 811, favorite: false, like: true},
        {id: 2, name: "Zafarbek", viewers: 411, favorite: false, like: false},
        {id: 3, name: "Yusufboy ", viewers: 300, favorite: true, like: true},
      ],
      term: '',
      filter: 'all',
    }


  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
    },
    onToggleHandler({id, prop}) {
      this.movies = this.movies.map(item => {
        if (item.id == id) {
          return {...item, [prop]: !item[prop]}
        }
        return item
      })

    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(a => a.id !== id)
    },
    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },
    onFilterHandler(arr, filter) {
      switch (filter) {

        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViewers':
          return arr.filter(c => c.viewers > 500 )
        default:
          return arr

      }

    },

    updateTermHandler(term) {
      this.term = term
    },
    updateFilterHandler(filter){
      this.filter = filter

    },

  },

}

</script>

<style scoped>
.app {
  height: 100vh;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: white;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}

</style>