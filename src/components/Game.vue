<template>
  <div class="game">
    <div :class="'panel _' + questions.current" :style="{
      width: `${size.panelW}px`,
      height: `${size.panelH}px`,
      backgroundSize: `${size.panelW}px ${size.panelH}px`
    }">
      <div class="tiles"  :style="{
        width: `${size.panelW}px`,
        height: `${size.panelH}px`
      }">
        <div 
          v-for="(tile, idx) in tiles.total" 
          :key="idx" 
          :class="'tile' + (tiles.selected.includes(tile) ? ' selected' : '')" 
          :style="{
            width: `${size.tileW}px`,
            height: `${size.tileH}px`,
            lineHeight: `${size.tileH}px`
          }"
          @click="tiles.selected.push(tile)"
          >
          {{tile + 1}}
        </div>
      </div>
    </div>
    <div class="slides">
      <button @click="clearTiles()">정답 보기</button>
      <span v-for="(question, idx) in questions.total" :key="idx" @click="pickQuestion(question)"
        :class="questions.solved.includes(question) ? 'solved' : ''">
        {{question + 1}}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Game',
  props: {
    msg: String
  },
  data () {
    return {
      size: {
        winW: 0,
        winH: 0,
        panelW: 0,
        panelH: 0,
        tileW: 0,
        tileH: 0
      },
      tiles: {
        total: [],
        selected: []
      },
      questions: {
        current: 0,
        total: [],
        solved: []
      }
    }
  },
  methods: {
    clearTiles: function () {
      const _this = this
      _this.tiles.total.map(function (tile) {
        _this.tiles.selected.push(tile)
      })
    },
    setTiles: function () {
      const _this = this
      _this.tiles.selected.splice(0, _this.tiles.selected.length)
    },
    pickQuestion: function (question) {
      const _this = this
      _this.setTiles()
      _this.questions.current = question + 1
      _this.questions.solved.push(question)
    }
  },
  mounted () {
    const _this = this
    const s = _this.size
    s.winW = window.innerWidth
    s.winH = window.innerHeight
    s.panelH = s.winH - 64
    s.panelW = s.panelH * 4 / 3
    s.tileW = s.panelW / 16 - 2
    s.tileH = s.panelH / 12 - 2

    for (let i = 0; i < 192; i++) {
      _this.tiles.total.push(i)
    }

    for (let i = 0; i < 10; i++) {
      _this.questions.total.push(i)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.game {
  background-color: #ddd;
}
.panel {
  position: relative;
  margin: 0 auto;
  background-color: white;
}

.panel._1 { background-image: url(../assets/img/question/1.png) }
.panel._2 { background-image: url(../assets/img/question/2.png) }
.panel._3 { background-image: url(../assets/img/question/3.png) }
.panel._4 { background-image: url(../assets/img/question/4.png) }
.panel._5 { background-image: url(../assets/img/question/5.png) }
.panel._6 { background-image: url(../assets/img/question/6.png) }
.panel._7 { background-image: url(../assets/img/question/7.png) }
.panel._8 { background-image: url(../assets/img/question/8.png) }
.panel._9 { background-image: url(../assets/img/question/9.png) }
.panel._10 { background-image: url(../assets/img/question/10.png) }

.tiles {
  position: absolute;
  left: 0;
  top: 0;
}
.tiles .tile {
  display: inline-block;
  color: white;
  background-color: #222;
  font-size: 1.2em;
  font-weight: bold;
  cursor: pointer;
  border: 1px solid black;
}
.tiles .tile:hover {
  background-color: black;
}
.tiles .tile.selected {
  opacity: 0;
}
.slides {
  height: 64px;
  line-height: 64px;
  background-color: black;
  font-size: 1.1em;
}
.slides button {
  font-size: 1.1em;
  margin-right: 24px;
  cursor: pointer;
}
.slides button:hover {
  color: #0085ff;
}
.slides span {
  display: inline-block;
  vertical-align: middle;
  width: 32px;
  height: 32px;
  line-height: 32px;
  border-radius: 18px;
  text-align: center;
  background-color: white;
  margin: 0 6px;
  cursor: pointer;
}
.slides span:hover {
  color: #0085ff;
  font-weight: bold;
}
.slides span.solved {
  opacity: 0.25;
}
</style>
