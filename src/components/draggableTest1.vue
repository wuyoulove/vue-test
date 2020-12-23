<template>
  <div>
    <div>
      <draggable
        :group='{name: "menu", put: true}'
        @add='addCollection'
        @update='sortCollection'
        :value="collections"
      >
        <div
          v-for='collection in collections'
          :key='collection.id'
        >
          <collection-item
            @delete='deleteCollection'
            :deletable='modified'
            :collection='collection'
          ></collection-item>
        </div>
      </draggable>
    </div>
    <!-- 未收藏 -->
    <div>
      <draggable
        :group='{name: "menu", put: false}'
        :sort='false'
        :value="notCollectedMenus"
      >
        <div
          v-for='menu in notCollectedMenus'
          :key='menu.id'
        >
          <menu-item :menu='menu'></menu-item>
        </div>
      </draggable>
    </div>
  </div>
</template>
<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
  },
  data() {
    return {
      collections: [{
        id:1
      }],
      availableMenus: [],
    };
  },
  computed: {
    notCollectedMenus() {
      return this.availableMenus.filter((menu) => {
        let collection = this.collections.find(
          (collection) => collection.menu.id === menu.id
        );
        return collection == undefined ? true : false;
      });
    },
  },
  methods: {
    deleteCollection(collectionToBeDeleted) {
      let index = this.collections.findIndex(
        (collection) => collection.id == collectionToBeDeleted.id
      );
      this.collections.splice(index, 1);
    },
    addCollection(evt) {
      let newCollectionIndex = evt.newIndex;
      let menuIndex = evt.oldIndex;

      let menu = this.notCollectedMenus[menuIndex];
      let newCollection = {};
      newCollection.menu = menu;
      newCollection.username = this.username;
      this.collections.splice(newCollectionIndex, 0, newCollection);
    },
    sortCollection(evt) {
      let newIndex = evt.newIndex;
      let oldIndex = evt.oldIndex;

      let collection = this.collections[oldIndex];
      this.collections.splice(oldIndex, 1);
      this.collections.splice(newIndex, 0, collection);
    },
  },
};
</script>