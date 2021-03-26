<template>
  <div class="theme-select">
    <span
      v-for="(item, index) in themeList"
      :key="index"
      @click="changeTheme(item)"
      :class="item.value"
      :title="item.name"
    >
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      themeList: [
        {
          name: '默认',
          value: 'default',
        },
        {
          name: '暗黑',
          value: 'dark',
        }
      ],
    };
  },
  methods: {
    changeTheme(i) {
      const theme = i.value;
      window.zarmTheme = theme;
      try {
        const frame = document.querySelector('#simulatorFrame');
        const frameLocation = frame.contentWindow.location;
        const { origin, hash } = frameLocation;
        if (theme === 'dark') {
          frame.setAttribute('src', `${origin}${window.CONFIG.pathname}dark.html${hash}`);
        } else {
          frame.setAttribute('src', `${origin}${window.CONFIG.pathname}/demo.html${hash}`);
        }
      } catch (e) {
        // console.log(e);
      }
    },
  },
};
</script>

<style scoped lang="scss">
.theme-select {
  > span {
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 1px solid #f2f2f2;
    padding: 2px;
    position: relative;
    box-sizing: border-box;
    margin-right: 10px;
    cursor: pointer;
    vertical-align: middle;

    &:hover {
      border-color: darken(#f2f2f2, 20%);
    }

    &:after {
      content: "";
      display: block;
      width: 14px;
      height: 14px;
      background-color: #12c287;
    }

    &.dark:after {
      background-color: #000;
    }
  }
}
</style>
