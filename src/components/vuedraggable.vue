<template>
  <div class="box">
    <div class="left">
      <draggable
        class="list-group"
        :list="list1"
        group="people"
        :move="checkMove"
        @add='addCollection'
        @update='sortCollection'
        @change="addLog"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list1"
          :key="element.name"
        >
          {{ element.name }}
        </div>
      </draggable>
    </div>

    <div class="right">
      <draggable
        class="list-group"
        :list="list2"
        group="people"
        @change="removeLog"
      >
        <div
          class="list-group-item1"
          v-for="(element, index) in list2"
          :key="element.name"
        >
          {{ element.name }}
        </div>
      </draggable>
    </div>

    <!-- <rawDisplayer class="col-3" :value="list1" title="List 1" />

    <rawDisplayer class="col-3" :value="list2" title="List 2" /> -->
  </div>
</template>
<script>
import draggable from "vuedraggable";

export default {
  name: "two-lists",
  display: "Two Lists",
  order: 1,
  components: {
    draggable,
  },
  data() {
    return {
      list1: [
        { name: "上左", id: 1 },
        { name: "上右", id: 2 },
        { name: "下左", id: 3 },
        { name: "下右", id: 4 },
      ],
      list2: [
        { name: "测试1", id: 5 },
        { name: "测试2", id: 6 },
        { name: "测试3", id: 7 },
      ],
      listItem:{}
    };
  },
  methods: {
    addCollection(evt){
      console.log(evt,11111)
    },
    sortCollection(evt){
      console.log(evt,2222)
    },
    add: function () {
      this.list.push({ name: "Juan" });
    },
    replace: function () {
      this.list = [{ name: "Edgard" }];
    },
    clone: function (el) {
      return {
        name: el.name + " cloned",
      };
    },
    log: function (evt) {
      window.console.log(evt, 44444);
      this.list1.splice(evt.added.newIndex, 1);
    },
    addLog(evt) {
      console.log(evt.added, "addLog");
      // this.listItem = this.list1[evt.added.newIndex]
      this.listItem = this.list1.splice(evt.added.newIndex-1,1)
      console.log(this.listItem,'this.listItem')
    },
    removeLog(evt) {
      console.log(evt.removed.oldIndex, "removeLog");
      this.list2.splice(evt.removed.oldIndex,0,this.listItem[0])
    },
    checkMove(e) {
      window.console.log("Future index: " + e.draggedContext.futureIndex);
    },
  },
};
</script>
<style scoped>
.box{
  display: flex;
  width: 100%;
  height: 100%;
}
.left{
  flex: 4;
  height: 100%;
  border-right: 1px solid #cccccc;
}
 .left .list-group{
   height: 100%;
   position: relative;
 }
.right{
  flex: 1;
}
.list-group-item {
  width: 300px;
  height: 50%;
  line-height: 200px;
  border: 1px solid #cccccc;
  margin-top: 8px;
  position: absolute;
}
.list-group-item1 {
  width: 300px;
  height: 300px;
  border: 1px solid #cccccc;
  margin-top: 8px;
}
.list-group-item:nth-child(1){
  left: 0;
  top: 0;
}
.list-group-item:nth-child(2){
  right: 0;
  top: 0;
}
.list-group-item:nth-child(3){
  left: 0;
  bottom: 0;
}
.list-group-item:nth-child(4){
  right: 0;
  bottom: 0;
}
</style>
