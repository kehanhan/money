<template>
  <header class="money-header">
    <ul>
      <li :class="type === '-' && 'selected'" @click="selectType('-')">
        <strong>支出</strong>
      </li>
      <li :class="type === '+' && 'selected'" @click="selectType('+')">
        <strong>收入</strong>
      </li>
    </ul>
  </header>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Type extends Vue {
  @Prop({ default: "-" }) readonly type!: string;

  selectType(type: "+" | "-") {
    this.$store.setType(type);
    this.$emit("update:type", type);
  }
}
</script>

<style lang="scss" scoped>
@import "src/assets/style/helper.scss";

.money-header {
  background: $color-theme;

  position: relative;

  > ul {
    height: 60px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    > li {
      margin-left: 25px;
      margin-right: 25px;
      font-size: 18px;
      font-family: $font-hei;
      position: relative;

      &.selected {
        color: $color-highlight-green;
      }

      &.selected::after {
        content: "";
        position: absolute;
        bottom: -10px;
        left: 0;
        height: 4px;
        width: 100%;
        background: $color-highlight-green;
      }

      &:last-child.selected {
        color: $color-highlight-red;
      }

      &:last-child.selected::after {
        background: $color-highlight-red;
      }
    }
  }
}
</style>
