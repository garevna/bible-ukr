<template>
  <v-menu
    v-model="show"
    :position-x="event.x"
    :position-y="event.y + 8"
    absolute
    offset-y
  >
    <div class="homefone">
      <div v-for="(menuItem, menuItemIndex) in menuItems" :key="menuItemIndex" class="clicked-item">
        <span @click.stop="selectItem(menuItem)">{{ menuItem.text }}</span>
      </div>
    </div>
  </v-menu>
</template>

<script>

export default {
  name: 'DropdownMenu',

  props: ['event', 'selected', 'menuItems', 'showMenu'],

  computed: {
    show: {
      get () {
        return this.showMenu
      },
      set (val) {
        this.$emit('update:showMenu', val)
      }
    }
  },

  watch: {
    event (value) {
      console.log('EVENT:\n', value)
    }
  },

  methods: {
    selectItem (item) {
      console.log(item)
      this.$emit('update:selected', item.value || item.title || item.text || item)
      this.show = false
    }
  }
}
</script>

<style scoped>

.homefone {
  background: #fbfbfb;
  padding: 8px 0;
  /* padding: 16px; */
}

.clicked-item {
  padding: 4px 16px;
  cursor: pointer;
  font-size: 13px;
}

.clicked-item:hover {
  background: #ddd;
}
</style>
