<template>
  <div class="v-header">
      <div class="content-wrapper">
          <div class="avatar">
              <img width="64" height="64" :src="headerSeller.avatar">
          </div>
          <div class="content">
              <div class="title">
                  <span class="brand"></span>
                  <span class="name">{{headerSeller.name}}</span>
              </div>
              <div class="description">
                  {{headerSeller.description}}/{{headerSeller.deliveryTime}}分钟送达
              </div>
              <div class="support" v-if="headerSeller.supports">
                  <span class="icon" :class="classMap[headerSeller.supports[0].type]"></span>
                  <span class="text">{{headerSeller.supports[0].description}}</span>
              </div>
          </div>
          <div class="support-count" v-if="headerSeller.supports" @click="showDetail">
              <span class="count">{{headerSeller.supports.length}}个</span>
              <i class="icon-keyboard_arrow_right"></i>
          </div>
      </div>
      <div class="bulletin-wrapper" @click="showDetail">
          <span class="bulletin-title"></span>
          <span class="bulletin-text">{{headerSeller.bulletin}}</span>
          <i class="icon-keyboard_arrow_right"></i>
      </div>
      <div class="background">
          <img :src="headerSeller.avatar" width="100%" height="100%">
      </div>
      <transition name="fade">
          <div class="detail" v-show="detailShow">
              <div class="detail-wrapper clearfix">
                  <div class="detail-content">
                      <h1 class="name">{{headerSeller.name}}</h1>
                      <div class="star-wrapper">
                        <star :size="48" :score="headerSeller.score"></star>
                      </div>
                      <div class="title">
                        <div class="line"></div>
                        <div class="text">优惠信息</div>
                        <div class="line"></div>
                      </div>
                      <ul class="supports" v-if="headerSeller.supports">
                        <li class="supports-item" v-for="(item,index) in headerSeller.supports" :key="changeToString(item)">
                            <span class="icon" :class="classMap[headerSeller.supports[index].type]"></span>
                            <span class="text">{{headerSeller.supports[index].description}}</span>
                        </li>
                      </ul>
                      <div class="title">
                          <div class="line"></div>
                          <div class="text">商家公告</div>
                          <div class="line"></div>
                      </div>
                      <div v-if="headerSeller.bulletin" class="bulletin">
                        <p class="content">{{headerSeller.bulletin}}</p>
                    </div>
                  </div>
                  <div class="detail-close" @click="closeDetail">
                      <i class="icon-close"></i>
                  </div>
              </div>
          </div>
      </transition>
  </div>
</template>

<script>
import star from '../star/star'

export default {
  props: {
    headerSeller: {
      type: Object
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow = true
    },
    closeDetail () {
      this.detailShow = false
    },
    changeToString (item) {
      item.toString()
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    star
  }
}
</script>

<style lang="stylus">
@import "../../common/stylus/mixin.styl"
@import '../../stylus/header/header.styl';
</style>
