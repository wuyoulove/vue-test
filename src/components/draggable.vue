<template>
  <div class="box">
    <div class="left">
      <div
        tag="div"
        class="container"
      >
        <div
          class="item left-item"
          v-for="item in items"
          :key="item.key"
          :style="{background:item.color}"
          draggable="true"
          @dragstart="handleDragStart($event, item)"
          @dragover.prevent="handleDragOver($event, item)"
          @dragenter="handleDragEnter($event, item)"
          @dragend="handleDragEnd($event, item)"
        >
          {{item.key}}
        </div>
      </div>
    </div>
    <div class="right">
      <div
        tag="div"
        class="container1"
      >
        <div
          class="item"
          v-for="item in items1"
          :key="item.key"
          :style="{background:item.color}"
          draggable="true"
          @dragstart="handleDragStart1($event, item)"
          @dragover.prevent="handleDragOver1($event, item)"
          @dragenter="handleDragEnter1($event, item)"
          @dragend="handleDragEnd1($event, item)"
        >
          {{item.key}}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Toolbar",
  data() {
    return {
      items: [
        { key: 0, color: "#ffebcc" },
        { key: 1, color: "#ffb86c" },
        { key: 2, color: "#f01b2d" },
        { key: 3, color: "#f01b2f" },
      ],
      items1: [
        { key: 4, color: "#f01b4d" },
        { key: 5, color: "#f01b0d" },
      ],
      dragging: null,
      insideDragging:null,
      handleDragEnteritem: null,
      handleDragEnteritem1: null,
    };
  },
  methods: {
    handleDragStart(e, item) {
      this.insideDragging = item;
      console.log(this.insideDragging,'insideDragging')
    },
    handleDragEnd(e, item) {
      console.log(item,'item-------')
      const newItems = [...this.items];
      const src = newItems.indexOf(this.insideDragging);
      const dst = newItems.indexOf(this.handleDragEnteritem);
      if(src !== -1 && dst !== -1){
        newItems.splice(dst, 1, ...newItems.splice(src, 1,this.handleDragEnteritem));
        this.items = newItems;
      }
      this.handleDragEnteritem = null
    },
    //首先把div变成可以放置的元素，即重写dragenter/dragover
    handleDragOver(e) {
      e.dataTransfer.dropEffect = "move"; // e.dataTransfer.dropEffect="move";//在dragenter中针对放置目标来设置!
    },
    handleDragEnter(e, item) {
      console.log(item, "handleDragEnter-item");
      this.handleDragEnteritem = item;
    },

    handleDragStart1(e, item) {
      this.dragging = item;
    },
    handleDragEnd1(e, item) {
      e.dataTransfer.dropEffect = "";
      console.log(e, item, "e-item");
      const newItems = [...this.items];
      const newItems1 = [...this.items1];
      console.log(newItems, newItems1);
      console.log(this.dragging, "this.dragging", this.handleDragEnteritem);
      const src = newItems1.indexOf(this.dragging);
      let dst = newItems.indexOf(this.handleDragEnteritem);
      console.log(src, dst, "src-dst");
      if(src !== -1 && dst !== -1){
        this.items.splice(dst, 1, ...newItems1.splice(src, 1));
        this.items1.splice(src, 1, this.handleDragEnteritem);
        // this.items = newItems;
      }else{
        dst = newItems1.indexOf(this.handleDragEnteritem1);
        console.log(dst,'---dst',src)
        newItems1.splice(dst, 1, ...newItems1.splice(src, 1,this.handleDragEnteritem1));
        this.items1 = newItems1;
      }
      this.dragging = null;
    },
    //首先把div变成可以放置的元素，即重写dragenter/dragover
    handleDragOver1(e) {
      e.dataTransfer.dropEffect = "move"; // e.dataTransfer.dropEffect="move";//在dragenter中针对放置目标来设置!
    },
    handleDragEnter1(e, item) {
       this.handleDragEnteritem1 = item;
    },
  },
};
</script>
 
<style scoped>
.box {
  width: 100%;
  height: 100%;
  display: flex;
}
.left {
  flex: 4;
  border-right: 1px solid #cccccc;
  height: 100%;
}
.left > .container {
  /* display: flex;
  justify-content: space-around; */
}
.right {
  flex: 1;
  /* border: 1px solid #000; */
  height: 100%;
}
.item {
  width: 300px;
  height: 300px;
  text-align: center;
  line-height: 300px;
  color: #000;
  font-size: 20px;
  /* margin-top: 10px; */
  transition: all linear 0.3s;
}
.container{
  /* position: relative; */
  width: 100%;
  height: 100%;
}
.left-item{
  /* position: absolute; */
}
.left-item:nth-child(1){
  /* left: 0;
  top: 0; */
  transform:translate(0px,0px)
}
.left-item:nth-child(2){
  /* right: 0;
  top: 0; */
  transform:translate(1000px,-300px)
}
.left-item:nth-child(3){
  /* left: 0;
  bottom: 0; */
  transform:translate(0px,0px)
}
.left-item:nth-child(4){
  /* right: 0;
  bottom: 0; */
  transform:translate(1000px,-300px)
}
</style>
