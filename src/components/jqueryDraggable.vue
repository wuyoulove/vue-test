<template>
  <div
    id="my-list"
    ref="list"
  >
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
    <li>8</li>
    <li>9</li>
  </div>
</template>
<script src="https://cdn.jsdelivr.net/npm/jquery-sortablejs@latest/jquery-sortable.js"></script>
<script>
// import "jquery-sortablejs";
export default {
  data() {
    return {};
  },
  mounted(){
    this.init()
  },
  methods: {
    init() {
      console.log(document.getElementById("my-list"),'00000')
      document.getElementById("my-list").sortable({
        // SortableJS options go here
        // See: (https://github.com/SortableJS/Sortable#options)

        handle: ".handle",
        invertSwap: true,
        // . . .
      });
    },
  },
};
</script>
<style scoped>
</style>