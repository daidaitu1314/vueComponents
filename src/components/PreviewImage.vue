<template>
  <div v-show="show" class="previewImage">
    <div class="topBar"><span @click="hidePreview()">返回</span>{{index + 1}}/{{list.length}}</div>
    <div :class="{preview:true,slide:slide}"
         :style="{width:list.length+'00%',transform:'translate3d('+translateX+'px,0px,0px)'}">
      <div class="item" v-for="item in list"
           :style="{backgroundImage:'url('+currentImage+')',width:100/list.length+'%'}"></div>
    </div>
  </div>
</template>
<script>
  export default {
    componentName: 'PreviewImage',
    props: {
      list: {},
      showPreviewImage: {}
    },
    created() {
      this.currentImage = this.list[this.index];
      this.show = this.showPreviewImage;
    },
    data() {
      return {
        currentImage: this.currentImage,
        show: this.show,
        index: 0,
        translateX: 0,
        slide: false
      }
    },
    mounted() {
      var _self = this;
      var width = _self.$el.parentNode.offsetWidth;
      var min = -(this.list.length - 1) * width;
      var max = 0;
      var startX = 0;
      var distanceX = 0;
      var startTime = 0;
      var isMove = false;
      _self.$el.addEventListener('touchstart', function (e) {
        startX = e.touches[0].clientX;
        startTime = Date.now();
      });
      _self.$el.addEventListener('touchmove', function (e) {
        var moveX = e.touches[0].clientX;
        distanceX = moveX - startX;
        var translateX = -_self.index * width + distanceX;
        if (translateX >= min && translateX <= max) {
          _self.slide = false;
          _self.translateX = translateX;
        }
        isMove = true;
      });
      _self.$el.addEventListener('touchend', function (e) {
        if (isMove) {
          var totalTime = Date.now() - startTime;
          var speed = Math.abs(distanceX) / totalTime;
          if (speed > 0.2 || Math.abs(distanceX) > width / 3) {
            if (distanceX > 0) {
              if (_self.index > 0) {
                _self.index--;
              }
            } else {
              if (_self.index < _self.list.length - 1) {
                _self.index++;
              }
            }
          }
          _self.slide = true;
          _self.translateX = -_self.index * width;
        }
        startX = 0;
        distanceX = 0;
        isMove = false;
        startTime = 0;
      });
    },
    methods: {
      hidePreview() {
        this.show = false;
      },
      showPreview() {
        this.show = true;
      }
    }
  }
</script>
<style>
  body {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .previewImage {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
  }

  .previewImage .topBar {
    height: 40px;
    line-height: 40px;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    text-align: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1;
  }

  .previewImage .topBar span {
    position: absolute;
    left: 10px;
    top: 0;
    cursor: pointer;
    font-size: 12px;
  }

  .previewImage .preview {
    width: 100%;
    height: 100%;
    position: relative;
  }

  .previewImage .preview.slide {
    transition: all 0.3s;
  }

  .previewImage .preview .item {
    height: 100%;
    float: left;
    background-color: rgba(0, 0, 0, 0.5);
    background-position: center center;
    background-size: contain;
    background-repeat: no-repeat;
  }
</style>
