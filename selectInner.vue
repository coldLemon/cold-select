<template>
  <div class="select_inner">
    <ul class="menu fllil">
      <li>
        <p @click="showList = true">{{ selected.label }}</p>
        <ul class="sub-menu">
          <li
            v-for="item in pageInner"
            :key="item.id"
            @click="handleChoose(item)"
          >
            <span class="text-desc">
              {{ item.label }}
            </span>
          </li>
        </ul>
      </li>
    </ul>
    <div class="clear"></div>
  </div>
</template>

<script>
export default {
  name: 'selectInner',
  data() {
    return {
      pageInner: [],
      selected: 'xx',
      showList: false
    }
  },
  methods: {
    handleChoose(val) {
      this.selected = val
      this.$emit('callback', val.value)
    }
  },
  mounted() {
    if (this.pageData.length !== 0) {
      this.pageInner = this.pageData.map(i => {
        console.log(i)
        return {
          id: i[this.keey],
          label: i[this.label],
          value: i[this.value]
        }
      })
      this.selected = this.pageInner[0]
    }
  },
  props: {
    pageData: {
      type: Array,
      default: () => {
        return []
      }
    },
    label: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    keey: {
      type: String,
      default: ''
    }
  },
  watch: {
    pageData(val) {
      return val
    }
  }
}
</script>

<style scoped lang="scss">
.select_inner {
  max-width: 300px;
  margin: 0 auto;
  font-weight: 700px;
  border: 1px dashed #eee;
  border-radius: 8px;
  box-sizing: border-box;

  .text-desc {
    // padding: 10px;
  }
}
.select_inner .menu {
  width: 100%;
  display: flex;
}

.select_inner li {
  line-height: 30px;
  padding: 0 20px;
  background: #09f;
  color: #fff;
  position: relative;
  cursor: pointer;
}

.select_inner li ul {
  width: 100%;
  position: absolute;
  left: 0;
  top: 30px;
  height: 0;
  max-height: 700px;
  overflow: hidden;
}

.select_inner li ul li {
  float: none;
  /*过渡代码*/
  transition: all 0.3s;
  background: #fff;
  color: rgb(158, 142, 142);
  padding: 10px;
  text-align: center;
  // opacity: 0;
}
/*奇数项初始往右边偏移100%*/
.select_inner li ul li:nth-of-type(1n) {
  transform: translate3d(100%, 0, 0);
}
/*偶数项初始往左边偏移100%*/
.select_inner li ul li:nth-of-type(2n) {
  transform: translate3d(-100%, 0, 0);
}

.select_inner li:hover ul {
  overflow: visible;
}
/*透明度和互动同时进行*/
.select_inner li:hover ul li {
  opacity: 1;
  transform: translate3d(0, 0, 0);
}

.select_inner li ul li:hover {
  background-color: #eee;
  color: #000;
}
</style>
