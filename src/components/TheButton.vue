<template>
  <button class="bg-transparent border rounded py-2 px-4" :class="typeClasses" v-on="listeners">
    <slot></slot>
  </button>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import { Prop } from 'vue-property-decorator';

@Component({})
export default class TheButton extends Vue {

  @Prop({ default: false })
  public primary!: boolean;

  @Prop({ default: false })
  public secondary!: boolean;

  private types: any = {
    primary: 'bg-indigo hover:bg-indigo-light hover:border-indigo-light text-white border-indigo',
    secondary: 'text-grey-dark border-grey hover:bg-indigo hover:border-indigo hover:text-white',
    default: 'text-grey-dark border-grey',
  };

  get typeClasses() {
    const buttonType = Object.keys(this.$props).filter((k: string) => this.$props[k])[0];
    return this.types[buttonType] || this.types.default;
  }

  get listeners() {
    return {
      ...this.$listeners,
    };
  }

}
</script>

