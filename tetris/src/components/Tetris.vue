<template>
  <div class="snake">
    <table ref="table" v-html="demo"></table>
    <div class="wicket">
      <table class="table2">
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
      </table>
      <h2>分数：{{number}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tetris",
  data() {
    return {
      row: 0,
      col: 4,
      demo: "",
      td: "",
      type: "",
      allDir: "",
      dir: "",
      nextType: "",
      nextAllDir: "",
      nextDir: "",
      allColor: "",
      timer: "",
      number:0,
      mapCode: [
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0],
        [1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0],
        [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
        [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
      ],
      fangkuai: {
        S: [
          [
            [0, 1, 1, 0],
            [1, 1, 0, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 1, 0, 0],
            [0, 1, 1, 0],
            [0, 0, 1, 0],
            [0, 0, 0, 0],
          ],
        ],
        Z: [
          [
            [2, 2, 0, 0],
            [0, 2, 2, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 2, 0, 0],
            [2, 2, 0, 0],
            [2, 0, 0, 0],
            [0, 0, 0, 0],
          ],
        ],
        L: [
          [
            [0, 3, 0, 0],
            [0, 3, 0, 0],
            [0, 3, 3, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 0, 0, 0],
            [3, 3, 3, 0],
            [3, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [3, 3, 0, 0],
            [0, 3, 0, 0],
            [0, 3, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 0, 3, 0],
            [3, 3, 3, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
        ],
        O: [
          [
            [0, 4, 4, 0],
            [0, 4, 4, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
        ],
        T: [
          [
            [0, 0, 0, 0],
            [5, 5, 5, 0],
            [0, 5, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 5, 0, 0],
            [0, 5, 5, 0],
            [0, 5, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 5, 0, 0],
            [5, 5, 5, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 5, 0, 0],
            [5, 5, 0, 0],
            [0, 5, 0, 0],
            [0, 0, 0, 0],
          ],
        ],
        J: [
          [
            [0, 6, 0, 0],
            [0, 6, 0, 0],
            [6, 6, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [6, 0, 0, 0],
            [6, 6, 6, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [6, 6, 0, 0],
            [6, 0, 0, 0],
            [6, 0, 0, 0],
            [0, 0, 0, 0],
          ],
          [
            [0, 0, 0, 0],
            [6, 6, 6, 0],
            [0, 0, 6, 0],
            [0, 0, 0, 0],
          ],
        ],
        I: [
          [
            [0, 7, 0, 0],
            [0, 7, 0, 0],
            [0, 7, 0, 0],
            [0, 7, 0, 0],
          ],
          [
            [0, 0, 0, 0],
            [7, 7, 7, 7],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
          ],
        ],
      },
    };
  },
  methods: {
    // 获取颜色
    setColor(row, col, num) {
      setTimeout(() => {
        document.getElementsByTagName("tr")[row].getElementsByTagName("td")[
          col
        ].className = "c" + num;
      }, 0);
    },
    // 清除颜色
    clearColor(row, col) {
      setTimeout(() => {
        document
          .getElementsByTagName("tr")
          [row].getElementsByTagName("td")
          [col].className='';
      }, 0);
    },
    // 预览窗口
    // wicket(){
    //   this.
    // },
    // 预处理，看后一位是否有方块
    check(row, col) {
      for (let i = 0; i < 4; i++) {
        for (let j = 0; j < 4; j++) {
          // 看地图后一行是否有方块，并且看方块数列此行是否为0
          if (this.mapCode[row + i][col + j] !== 0 && this.dir[i][j] !== 0) {
            // 如果有则返回false停止下落
            return false;
          }
        }
      }
      return true;
    },
    // 渲染方块
    block(row, col) {
      for (let i = 0; i < 4; i++) {
        for (let j = 0; j < 4; j++) {
          if (this.dir[i][j] !== 0) {
            this.setColor(i + row, j + col, this.dir[i][j]);
          }
        }
      }
    },
    nextBlock(row, col) {
      for (var i = 0; i < 4; i++) {
        for (var j = 0; j < 4; j++) {
          document.getElementsByClassName('table2')[0].getElementsByTagName('tr')[i].getElementsByTagName('td')[j].className=''
          if (this.nextDir[i][j] !== 0) {
              console.log(document.getElementsByClassName('table2')[0].getElementsByTagName('tr')[i].getElementsByTagName('td')[j]);
              document.getElementsByClassName('table2')[0].getElementsByTagName('tr')[i].getElementsByTagName('td')[j].className='c'+this.nextDir[i][j]
          }
        }
      }
    },
    // 下一个初始化类型，此类型种类，图中位置
    nextInit() {
      let arrType = ["S", "T", "O", "L", "J", "I", "Z"];
      this.nextType = arrType[Math.floor(Math.random() * arrType.length)];
      this.nextAllDir = Math.floor(Math.random() * this.fangkuai[this.nextType].length);
      this.nextDir = this.fangkuai[this.nextType][this.nextAllDir];
      // console.log(this.type);
      this.nextBlock(0, 4);
    },
    init() {
      this.block(0,4)
    },
    // 初始化地图
    render() {
      for (let i = 0; i < 20; i++) {
        for (let j = 0; j < 12; j++) {
          this.clearColor(i,j)
          if (this.mapCode[i][j] !== 0) {
            this.setColor(i, j, this.mapCode[i][j]);
          }
        }
      }
    },
    // 停止后在地图上更改数字
    renderMap(row, col) {
      for (let i = 0; i < 4; i++) {
        for (let j = 0; j < 4; j++) {
          if (this.dir[i][j] !== 0) {
            this.mapCode[i + row].splice(j + col, 1, this.dir[i][j]);
            // console.log(this.mapCode);
          }
        }
      }
    },
    clear() {
      for (let i = 0; i < this.row+4; i++) {
        for (let j = 0; j < this.col+4; j++) {
          // 如果地图上此行此列是0，清除之前渲染的颜色
          if (this.mapCode[i][j] === 0) {
            this.clearColor(i,j);
          }
        }
      }
    },
    handleKeyDown(event) {
      console.log(event.keyCode);
      if (event.keyCode === 65 || event.keyCode === 37) {
        console.log(1);
        this.checkLeft();
      } else if (event.keyCode === 68 || event.keyCode === 39) {
        console.log(2);
        this.checkRight();
      } else if (event.keyCode === 32 || event.keyCode === 40) {
        console.log(3);
        this.checkEnd();
      } else if (event.keyCode === 87 || event.keyCode === 38) {
        console.log(4);
        this.checkRot();
      }
    },
    checkLeft() {
      if (this.check(this.row, this.col - 1)) {
        this.clear();
        this.col--;
        this.block(this.row, this.col);
      }
    },
    checkRight() {
      if (this.check(this.row, this.col + 1)) {
        this.clear();
        this.col++;
        this.block(this.row, this.col);
      }
    },
    checkEnd() {
      this.clear();
      while (this.check(this.row + 1, this.col)) {
        this.row++;
      }
      this.block(this.row, this.col);
    },
    checkRot() {
      let oldDir = this.allDir;
      console.log(oldDir);
      this.clear();
      this.allDir++;
      if (this.allDir > this.fangkuai[this.type].length - 1) {
        this.allDir = 0;
        console.log(this.allDir);
      }
      this.dir = this.fangkuai[this.type][this.allDir];
      if (!this.check(this.row, this.col)) {
        this.allDir = oldDir;
        console.log(this.allDir);
        this.dir = this.fangkuai[this.type][this.allDir];
      }
      this.block(this.row, this.col);
    },
    checkRemove() {
      for (let i = 0; i < 20; i++) {
        if (this.mapCode[i].indexOf(0) === -1) {
          this.mapCode.splice(i, 1);
          this.mapCode.unshift([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]);
          this.render()
          this.number+=10
          }
        }
    },
    checkOver(){
      for(let i=0;i<12;i++){
        if(this.mapCode[0][i]!==0){
          clearInterval(this.timer)
          alert('游戏结束')
        }
      }
    },
    checkDown() {
      this.timer = setInterval(() => {
        if (this.check(this.row + 1, this.col)) {
          this.clear();
          this.row++;
          this.block(this.row, this.col);
        } else {
          clearInterval(this.timer);
          console.log(this.col, this.row);
          this.renderMap(this.row, this.col);
          this.checkRemove();
          this.checkOver()
          this.type=this.nextType
          this.allDir=this.nextAllDir
          this.dir=this.nextDir
          this.row = 0;
          this.col = 4;
          this.nextInit()
          this.init();
          this.checkDown();
          
        }
      }, 500);
    },
  },
  mounted() {
    for (let i = 0; i < 20; i++) {
      for (let j = 0; j < 12; j++) {
        this.td += "<td></td>";
      }
      this.demo += `<tr>${this.td}</tr>`;
      this.td = "";
    }
    let arrType = ["S", "T", "O", "L", "J", "I", "Z"];
    this.type = arrType[Math.floor(Math.random() * arrType.length)];
    this.allDir = Math.floor(Math.random() * this.fangkuai[this.type].length);
    this.dir = this.fangkuai[this.type][this.allDir];
    this.render();
    this.init();
    this.nextInit()
    this.checkDown();
    window.addEventListener("keydown", this.handleKeyDown);
  },
};
</script>

<style lang="less" >
.snake{
  display: flex;
  justify-content: center;
  table {
    border-collapse: collapse;
    td {
      border: 1px solid black;
      width: 25px;
      height: 25px;
    }
  }
  .wicket{
    position: relative;
    left: 40px;
    .table2{
    // td{
    //   border: 1px solid #D4D4D4;
    //   background-color: black;
    // }
  }
  }
  
}

.c7 {
  background-color: tomato;
}
.c1 {
  background-color: red;
}
.c2 {
  background-color: blue;
}
.c3 {
  background-color: yellow;
}
.c4 {
  background-color: orange;
}
.c5 {
  background-color: purple;
}
.c6 {
  background-color: skyblue;
}
</style>