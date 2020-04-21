<template>
  <div class="box" id="file">
    <div class="ims">
      <img src="../assets/44.gif" alt class="is" />
    </div>
    <div class="main">
      <!-- <div class="main_hd">
        <img src="../assets/user.png" alt />
        <div class="main_bd">
          <div class="main__bd_spn">舒肤佳</div>
          <p>洗澡刷子搓软毛刷背不求人长柄背刷</p>
          <div class="main_tl">
            <span>3元券</span>
          </div>
        </div>
        <div class="main_fd">
          <div class="main_fd_left">￥16.9</div>
          <div class="main_fd_right">看相似</div>
        </div>
      </div>-->
      <div class="main_hd" v-for="item in this.goods" :key="item.id">
        <img :src="item.url.split(',')[0]" alt />
        <div class="main_bd">
          <div class="main__bd_spn">舒肤佳</div>
          <p>{{item.goodsname}}</p>
          <div class="main_tl">
            <span>3元券</span>
          </div>
        </div>
        <div class="main_fd">
          <div class="main_fd_left">
            ￥{{item.price}} 元 &nbsp; &nbsp;
            <del>{{item.price+12}} 元</del>
          </div>
          <div class="main_fd_right">看相似</div>
        </div>
      </div>
    </div>
    <transition name="cli">
      <div class="fixed" v-if="yx"></div>
    </transition>
    <div class="down" v-if="bd" @click="add" id="scrollTop"></div>
    <div
      class="file"
      v-if="wq"
      ref="fls"
      id="file"
      @touchstart="files"
      @touchmove="fl($event)"
      @touchend="end()"
    ></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      goods: [],
      loading: false, //控制是否显示懒加载
      finished: false,
      clientY: null,
      yx: false,
      bd: false,
      yy: true,
      wq: false,
      x: '',
      y: '',
      e: '',
      cury: '',
      curx: '',
      position: { x1: 0, y1: 0 },
      flag: true,
      x1: '',
      y1: '',
      w: '',
      h: '',
      l: '',
      t: '',
      r: '',
      b: ''
    }
  },
  created() {
    this.goodslist()
    //    this.che()
  },

  methods: {
    goodslist() {
      this.$axios.post('/goods/list', { type: 0 }).then(res => {
        console.log(res.data.message[0].url.split(',')[0])
        this.goods = res.data.message
      })
    },
    onLoad() {
      this.loading = false
      this.finished = true
    },
    che(e) {
      console.log(e)
      this.clientY = e.pageYOffset
    },
    handleScroll(e) {
      if (window.pageYOffset > 118) {
        this.yx = true
        this.bd = true
        this.wq = true
      } else if (window.pageYOffset < 118) {
        this.yx = false
        this.bd = false
      }
      let a = 2000
      if (window.pageYOffset > a) {
        // this.yx=true
      } else if (window.pageYOffset < a) {
        // this.yx=false
      }
      // console.log(e.path[1].mouseEvent,'滚动了')
    },
    add() {
      console.log('22')
      var c =
        document.documentElement.scrollTop ||
        document.body.scrollTop ||
        this.clientY
      //  alert(c)
      this.yy = setInterval(() => {
        c -= 100
        if (c >= 0) {
          document.documentElement.scrollTop = c
          document.body.scrollTop = c
        } else if (c < 60) {
          //  document.documentElement.scrollTop=c
          //  document.body.scrollTop=c
          return c
        } else if (c == 0) {
          // console.log(c,'cc')
          this.yy = false
          clearInterval(this.yy)
        }
        console.log('定时器停了没有')
      }, 20)
      // alert(c)
      // location.reload()
      this.clientY = c
      return c
      // this.goodslist()
      console.log(c)
    },
    files(e) {
    //  console.log(e)
      let file = document.querySelector('.file')
      //   console.log(this.$refs.fls.style)
      this.position.x = file.offsetLeft
      this.position.y = file.offsetTop
      // console.log(
      //   e.touches[0].target.offsetTop,
      //   e.touches[0].clientY,
      //   e.touches[0]
      // )
      // //   console.log(e.touches[0].target.offsetLeft)
      this.x = e.touches[0].clientY - e.touches[0].target.offsetTop
      this.y = e.touches[0].clientX - e.touches[0].target.offsetLeft
    //  console.log(this.x, this.y)
      e.stopPropagation()
      e.preventDefault()
    },
    fl(e) {
      // this.files(this.e)
   //   console.log(e)
      let file = document.querySelector('.file')
      e.preventDefault()
      e.stopPropagation()
      let touch = e.changedTouches[0]
      this.curx = touch.clientX - this.x
      this.cury = touch.clientY - this.y
      //   this.curx=Math.abs(this.curx)
      //   this.cury=Math.abs(this.cury)
      //   // console.log(x)
      // var flag=true
    //  console.log(touch.target.offsetLeft, touch.pageX, touch.target.offsetTop)
      if (
        touch.target.offsetLeft == 0 ||
        touch.target.offsetLeft >= 350 ||
        touch.target.offsetTop >= 630 ||
        touch.target.offsetTop <= 10
      ) {
        this.flag = false
      }
      if (this.flag) {
        // this.$refs.fls.style.left = this.curx + 'px'
        // this.$refs.fls.style.top = this.cury + 'px'
        file.style.left = this.curx + 'px'
        file.style.top = this.cury + 'px'
        //this.$refs.fls.style.transform = `translate(${this.curx}px,${this.cury}px)`
        // console.log(file)
      } else {
        var l, r
        if (touch.target.offsetLeft >= 350 || touch.target.offsetTop >= 630) {
          l = 349
          r = 629
        } else if (touch.target.offsetLeft <= 10) {
          l = 70
        } else if (touch.target.offsetTop <= 10) {
          r = 11
        }
      //  console.log(r, 'r')
        this.$refs.fls.style.left = `${l}` + 'px'
        this.$refs.fls.style.top = `${r}` + 'px'
     //   console.log('不走了吗')
        this.flag = true
      }
    },
    end(e) {}
  },
  mounted() {
    let moveDiv = document.querySelector('#file')
    this.w = document.documentElement.clientWidth || document.body.clientWidth
    this.h = document.documentElement.clientHeight || document.body.clientHeight
    this.x1 = moveDiv.offsetWidth
    this.y1 = moveDiv.offsetHeight
    this.l = moveDiv.offsetLeft
    this.t = moveDiv.offsetTop
    this.r = this.w - this.l - this.x1
    this.b = this.h - this.t - this.y1
    // file.addEventListener('touchstart', this.files, { passive: false })
    // file.addEventListener('touchmove', this.fl, { passive: false })
    // file.addEventListener('touchend', this.end, { passive: false })
    //file.addEventListener('touchend', this.end, { passive: false })
    window.addEventListener('scroll', this.handleScroll, true)
    //console.log( window.addEventListener('mousewheel', this.debounce(this.handleScroll,300), true)||window.addEventListener("DOMMouseScroll",this.debounce(this.handleScroll,300),false))
  },
  watch: {
    clientY(newVal) {
      // console.log(newVal,'newVal')
    }
  }
}
</script>
<style lang="less" scoped>
.box {
  width: 100%;
  display: flex;
  flex-direction: column;
  background: transparent;
}
.box > .ims {
  flex: 1;
  height: 90px;
  background-color: transparent;
  // background-color: #f60933;
  .is {
    width: 100%;
    height: 100%;
    // z-index: -9999;
    background: transparent;
    background-color: #f60933;
    opacity: 1;
  }
}
.main {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  //   margin: 0 5px;

  .main_hd {
    width: 48%;
    display: flex;
    height: 300px;
    flex-direction: column;
    // align-items: center;
    box-shadow: 3px 3px 3px #ccc;
    margin: 5px 4px;
    background-color: #fff;
    img {
      align-items: center;
      width: 152px;
      height: 152px;
      margin: 10px 20px;
    }
    .main_bd {
      height: 73px;
      display: flex;

      flex-direction: column;
      justify-content: flex-start;
      padding: 0 11px;
      .main__bd_spn {
        // align-items: flex-start;
        //  text-align: left;
        width: 80px;
        font-size: 14px;
        color: #fff;
        font-weight: 500;
        background-color: chocolate;
        height: 20px;
      }
      p {
        // border: 1px solid #ccc;
        overflow: hidden;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        // -webkit-box-orient: vertical;
        margin: 0;
      }
      .main_tl {
        height: 16px;
        display: flex;
        justify-content: flex-start;
        span {
          margin-top: 2px;
          width: 40px;
          height: 20px;
          font-size: 14px;
          color: #f60933;
          border: 1px solid #f60933;
        }
      }
    }
    .main_fd {
      height: 33px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      line-height: 33px;
      // align-items: flex-start;
      .main_fd_left {
        margin-left: 11px;
        font-size: 16px;
        font-weight: 700;
        color: #ff0000;
        del {
          color: #ccc;
          font-weight: 400;
          font-size: 14px;
        }
      }
      .main_fd_right {
        height: 25px;
        border-radius: 10px;
        background-color: pink;
        color: #f60933;
        font-size: 14px;
        margin-top: 5px;
        padding: 0 4px;
        line-height: 25px;
      }
    }
  }
  .main_hd:hover {
  }
}
.fixed {
  position: fixed;
  bottom: 50px;
  left: 0%;
  border: 1px solid #ff0000;
  //box-shadow: 2px 2px 2px #ff0000;
  width: 30%;
  height: 40px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 20px;
  // transform: translateX(-100%);
  transition: 2s;
}
.fixed:hover {
  //  left: 30%;
  // transform: translateX(100%)
}
.cli-enter {
  transform: translateX(-100%);
}
.cli-leave-to {
  transform: translateX(-100%);
}
.cli-enter-active,
.cli-leave-active {
  transition: all 0.5s ease;
}
.down {
  position: fixed;
  bottom: 60px;
  right: 5%;
  width: 30px;
  height: 30px;
  background-color: #696969;
  border-radius: 50%;
}
.down::before {
  content: '';
  position: absolute;
  left: 32%;
  top: 37%;
  width: 10px;
  height: 10px;
  transform: translate(-50%);
  border-top: 2px solid #fff;
  border-left: 2px solid #fff;
  transform: rotate(-313deg);
}
.file {
  width: 70px;
  height: 60px;
  border: 1px solid #333;
  position: fixed;
  right: 15px;
  top: 75%;
  touch-action: none;
}
</style>