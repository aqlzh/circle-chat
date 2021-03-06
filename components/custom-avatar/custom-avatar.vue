<template>
  <view
    class="avatar"
    :style="[wrapStyle]"
    :hover-class="clickable ? 'uni-list-item--hover' : ''"
    @click="click"
  >
    <view class="avatar-left">
      <view @click.stop="previewAvatar">
        <u-avatar
          :src="src"
          mode="square"
          size="large"
          :sex-icon="sexIcon"
          :show-sex="showSex"
          style="margin: 0 30rpx"
        >
        </u-avatar>
      </view>
      <view class="info">
        <slot name="content">
          <view
            v-if="title"
            class="text-lg text-black"
            :class="{ 'text-cut': titleCut }"
            style="width: 470rpx"
          >
            {{ title }}
          </view>
          <slot name="bottom">
            <view
              v-if="note"
              class="text-sm text-gray text-cut"
              style="width: 470rpx"
            >
              {{ note }}
            </view>
          </slot>
        </slot>
      </view>
    </view>

    <view v-if="showArrow">
      <uni-icons
        :size="16"
        class="uni-icon-wrapper"
        color="#bbb"
        type="arrowright"
      />
    </view>
  </view>
</template>

<script>
/**
 * custom-avatar 自定义头像组件
 * @description 本组件是适用于本项目的头像组件，一般用于展示头像的地方，如个人中心，或者评论列表页的用户头像展示等场所。
 * @property {String} bg-color 背景颜色（默认#ffffff）
 * @property {String} src 头像路径，如加载失败，将会显示默认头像
 * @property {String} sex-icon 性别图标，man-男，woman-女（默认man）
 * @property {String} show-sex 是否显示性别图标（默认false）
 * @property {Boolean} 	clickable = [true|false] 		是否开启点击反馈
 * @property {Boolean} 	showArrow = [true|false] 		是否显示箭头图标
 * @property {String} 	title 							标题
 * @property {String} 	title-cut 				  是否对标题截断
 * @property {String} 	note 							描述
 *
 * @event {Function} click 头像被点击
 */
export default {
  name: 'custom-avatar',

  props: {
    // 背景颜色
    bgColor: {
      type: String,
      default: '#ffffff'
    },
    // 头像路径
    src: {
      type: String,
      default: ''
    },
    // 右上角性别角标，man-男，woman-女
    sexIcon: {
      type: String,
      default: 'man'
    },
    // 是否显示性别图标
    showSex: {
      type: Boolean,
      default: false
    },
    // 是否开启点击反馈
    clickable: {
      type: Boolean,
      default: false
    },
    // 是否显示箭头图标
    showArrow: {
      type: [Boolean, String],
      default: false
    },
    // 标题
    title: {
      type: String,
      default: ''
    },
    titleCut: {
      type: Boolean,
      default: true
    },
    // 描述
    note: {
      type: [String, Number],
      default: ''
    }
  },

  computed: {
    wrapStyle() {
      let style = {}
      style.backgroundColor = this.bgColor
      return style
    }
  },

  methods: {
    click() {
      this.$emit('click')
    },

    previewAvatar() {
      uni.previewImage({
        current: this.src,
        urls: [this.src]
      })
    }
  }
}
</script>

<style lang="scss">
.avatar {
  width: 100%;
  height: 150rpx;
  padding-right: 30rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;

  .avatar-left {
    display: flex;
    align-items: center;

    .info {
      margin-right: 20rpx;
    }
  }
}

.uni-list-item--hover {
  background-color: $uni-bg-color-hover !important;
}
</style>
