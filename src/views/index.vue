<template>
  <div style="width: 100vw; height: 100vh">
    <div class="startForm">
      <div class="startLetter">
        <div class="contentLetter"></div>
        <img
          class="myAI"
          src="../assets/image/cute-young-boy-kid-wearing-vest-and-hat-free-png.png"
          alt=""
        />
        <div class="sticker" @click="onClick1()"></div>
        <button class="recieve" @click="onClick2()"><i class="fa-solid fa-gift"></i></button>
      </div>
    </div>

    <div class="backgroundParty">
      <img class="balloon1 balloon" src="" alt="" />
      <img class="balloon2 balloon" src="../assets/image/PNGkhothietke.net-02776.png" alt="" />
      <img
        class="bannerParty"
        src="../assets/image/makeupspa-kit-theme-happy-birthday-bunting-paper-banner-party-supply-261454.png"
        alt=""
      />
      <div class="letterForm">
        <input type="checkbox" id="mess" v-model="value" />
        <div class="content">
          <div class="mainContent"></div>
          <div class="img1">
            <img class="img" src="../assets/image/b4bbdb54b7152338d7143cb444a77f09.png" alt="" />
          </div>
        </div>
        <label class="designBox" for="mess"></label>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      contentLetterSrart_actived: 'Chúc mừng sinh nhật Hường',
      width: null,
      height: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      document.querySelector('#mess').addEventListener('change', function (event) {
        //Hiệu ứng gõ chữ cho phần nội dung của bức thư
        const mainContentLetter =
          'Chúc mừng sinh nhật bạn Hường! Hôm nay là ngày đặc biệt để ăn mừng sự tồn tại của bạn trong cuộc sống này. Tôi hy vọng bạn có một ngày sinh nhật tràn đầy niềm vui, hạnh phúc và những kỷ niệm đáng nhớ. Chúc bạn thành công trong mọi lĩnh vực, luôn mạnh khỏe, hạnh phúc và được bao bọc bởi tình yêu thương. Hãy tận hưởng ngày sinh nhật của bạn một cách tuyệt vời nhất!' //Nội dung của bức thư
        if (event.currentTarget.checked) {
          document.querySelector('.content').classList.add('actived')
          const splitMainContentLetter = mainContentLetter.split('')

          splitMainContentLetter.forEach((val, index) => {
            setTimeout(() => {
              document.querySelector('.mainContent').innerHTML += val
              if (index == mainContentLetter.length - 1) {
                document.querySelector('.img1').setAttribute('style', 'opacity: 1; transition: .5s')
              }
            }, 50 * index)
          })
          this.isFirst = false
        } else {
          document.querySelector('.content').classList.remove('actived')
          document.querySelector('.img1').setAttribute('style', 'opacity: 0; transition: .5s')
          document.querySelector('.mainContent').innerHTML = ''
        }
      })
      // Animation Drop light _ Tạo hiệu ứng kim tuyến rơi
      //Bạn có thể thiết kế lại để trông chân thật hơn nhé, thiết kế của mình hơi bị cứng và thiếu sự tự nhiên
      const getBackground = document.querySelector('.backgroundParty')
      this.width = getBackground.offsetWidth
      this.height = getBackground.offsetHeight
    })
  },
  methods: {
    onClick1() {
      //Hiệu ứng gõ chữ cho phần mở đầu của bức thư
      document.querySelector('.contentLetter').innerHTML = ''
      document.querySelector('.startLetter').classList.add('active')
      const splitContentLetterSrart_actived = this.contentLetterSrart_actived.split('')
      setTimeout(() => {
        splitContentLetterSrart_actived.forEach((val, index) => {
          setTimeout(() => {
            document.querySelector('.contentLetter').innerHTML += val
            if (index == this.contentLetterSrart_actived.length - 1) {
              setTimeout(() => {
                document
                  .querySelector('.recieve')
                  .setAttribute('style', 'opacity: 1; transition: .5s')
              }, 1000)
            }
          }, 50 * index)
        })
      }, 1000)
    },
    onClick2() {
      document.querySelector('.startLetter').classList.add('close')
      setTimeout(() => {
        document.querySelector('.startForm').classList.add('close')
        setTimeout(() => {
          document.querySelector('.startForm').setAttribute('style', 'bottom: 100%')

          let getTypeDevice = document.documentElement.clientWidth
          if (getTypeDevice <= 768) {
            this.createLight(20)
          } else {
            this.createLight(40)
          }
        }, 500)
      }, 500)
    },
    createLight(a) {
      var container = document.querySelector('.backgroundParty')
      const blurLv = [2, 4]
      const count = a
      const allDefaultColor = ['red', 'lime', 'yellow', 'orange', 'blue']

      for (var i = 0; i < count; i++) {
        var randomLeft = 0
        randomLeft = Math.floor(Math.random() * this.width)
        var randomTop = 0
        randomTop = Math.floor((Math.random() * this.height) / 2)
        var color = 'white'
        var blur = Math.floor(Math.random() * 2)
        var widthEle = Math.floor(Math.random() * 5) + 15
        var moveTime = Math.floor(Math.random() * 4) + 4

        var div = document.createElement('div')
        div.classList.add = 'snow'
        div.style.position = 'absolute'
        div.style.backgroundColor = allDefaultColor[Math.floor(Math.random() * 5)]
        div.style.borderRadius = Math.floor(Math.random() * 10 + 10).toString() + 'px'

        div.style.height = '0px'
        div.style.width = '0px'

        div.style.height = widthEle * Math.floor(Math.random() * 4 + 1) + 'px'
        div.style.width = widthEle + 'px'
        div.style.marginLeft = randomLeft + 'px'
        div.style.marginTop = randomTop + 'px'
        div.style.filter = 'blur(' + blurLv[blur] + 'px' + ')'
        div.style.animation = 'moveLight ' + moveTime + 's ease-in-out infinite'

        container.appendChild(div)
      }
    }
  }
}
</script>

<style></style>
