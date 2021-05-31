<template>
  <div class="container" style="width: 100%;height: 30%;background: oldlace;margin-top: 2rem" >
      <!--    上边一整栏-->
      <div class="topItem">
<!--        上边左侧-->
        <div class="top_left">
<!--          左侧第一行-->
          <div class="left_frist_row">
            <div style="border: 1px solid black">
              <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">SUPPLIER</div>
              <div>
                <div class="supName">天津高木</div>
                <div class="supCode">3710-0</div>
              </div>
            </div>
            <div>
              <div style="border: 1px solid black">
                <div  style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">PART ADDRESS</div>
                <div>
                  <div class="addName"></div>
                  <div class="addCode">B/T1R- 08</div>
                </div>
              </div>
            </div>
            <div>
              <div style="border: 1px solid black">
                <div  style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">CONVEYANCE NO</div>
                <div class="convCode">3710</div>
              </div>
            </div>
          </div>
<!--          左侧第二行-->
<!--          烦人的盒子又不能用组件,累了,我决定直接干行内样式了-->
<!--          哎嘿,深入骨髓-->
          <div class="left_second_row">
            <div  style="border: 1px solid black">
              L7N
            </div>
            <div></div>
<!--            第二行的第三个盒子，二维码右边那个-->
<!--            这个往下移一点，用margin吧-->
            <div>
<!--              上边的pallet code-->
              <div class="pallet" style="border: 1px solid black">
                <div class="palletName"  style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">PALLET CODE</div>
                <div class="palletCode"></div>
              </div>
<!--              下边的俩个小盒子-->
              <div class="bankrupt" >
                <div  style="border: 1px solid black">
                  <div  style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">PCS/ KANBAN</div>
                  <div>250</div>
                </div>
                <div style="border: 1px solid black">
                  <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">SERIAL#</div>
                  <div>1</div>
                </div>
              </div>
            </div>
          </div>

        </div>
<!--        上边右侧-->
        <div class="top_right">
          <div>
            <div>天津一汽 丰田汽车有限公司</div>
            <div>TFTM3</div>
          </div>
          <div  style="border: 1px solid black">
            <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">DOCK CODE</div>
            <div>AF</div>
          </div>
          <div style="border: 1px solid black">
            <div  style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">MORS</div>
            <div>33</div>
          </div>
        </div>
      </div>
      <!--    下边横栏-->
      <div class="bottomItem">
<!--        左边是个条形码-->
        <div  style="border: 1px solid black">
          <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">SUPPLIER DATA</div>
          <div>||||||||||||||||||||||</div>
        </div>
<!--        右边-->
        <div>
<!--          第二行分上下俩行吧-->
<!--          上-->
          <div>
<!--            上左-->
            <div  style="border: 1px solid black">
              <div>82715-0U180-00</div>
              <div>BRAKCET WIRING HARNESS CLAMP</div>
            </div>
<!--            上右-->
            <div>
              <div  style="border: 1px solid black">
                <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">ORDER NO</div>
                <div>2021<span style="padding: 0 .7rem">0508</span>03</div>
              </div>
            </div>
          </div>
<!--          下-->
          <div>
<!--            下左-->
            <div  style="border: 1px solid black">
              <div style="border-bottom: 1px solid black;background: lightgray;align-items: center;display: flex;flex-direction: row;justify-content: center">
                ARRIVAL TIME
              </div>
              <div>
                2021  /05/08  17:51
              </div>
            </div>
<!--            下右-->
            <div>
              |||||||||||
            </div>
          </div>
        </div>
      </div>
    </div>
<!--貌似可以用了，一天1900行代码。心烦烦。-->


</template>

<script>
export default {
  name: "tab",
  mounted() {
    // window.print()
  }
}
</script>
<style scoped lang="less">
div {
  box-sizing: border-box;
}
.container {
  box-sizing: border-box;
  border-top: 1px dashed gray;
  border-bottom: 1px black dashed ;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem 0;
}
.topItem {
  width: 70%;
  flex: 2;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  box-sizing: border-box;
  .top_left {
    width: 100%;
    flex:4;
    display: flex;
    flex-direction: column;
    .left_frist_row {
      display: flex;
      flex: 1;
      width: 100%;
      justify-content: space-between;
      div:nth-of-type(1) {
        flex: 2.5;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        div:nth-of-type(1) {
          flex: 1;
          font-size: .7rem;
          font-weight: bold;
          text-align: center;
        } 
        div:nth-of-type(2) {
          flex: 5;
          margin-left: 0;
          display: flex;
          flex-direction: column;
         .supName {
            flex: 2;
            font-size: .7rem;
            text-align: center;
            font-weight: normal;
            display: flex;
            justify-content: center;
            align-items: center;
         }
          .supCode{
            flex: 3;
            font-size: 1.7rem;
            font-weight: bold;
            display: flex;
            justify-content: center;
            align-items: center;
          }
        }
      }
      div:nth-of-type(2) {
        flex: 2;
        display: flex;
        flex-direction: column;
        margin-left: .3rem;
        div:nth-of-type(1) {
          flex: 1;
          font-size: .7rem;
          font-weight: bold;
          text-align: center;
        }
        div:nth-of-type(2) {
          flex: 5;
          margin-left: 0;
          display: flex;
          flex-direction: column;
          .addName {
            flex: 2;
            font-size: .7rem;
            text-align: center;
            font-weight: normal;
            display: flex;
            justify-content: center;
            align-items: center;
          }
          .addCode{
            flex: 3;
            font-size: 1.7rem;
            font-weight: bold;
            display: flex;
            justify-content: center;
            align-items: center;
          }

        }
      }
      div:nth-of-type(3) {
        flex: 1.5;
        display: flex;
        flex-direction: column;
        margin-left: .3rem;
        div:nth-of-type(1) {
          flex: 1;
          display: flex;
          font-weight: bold;
          justify-content: flex-start;
          font-size: .7rem;
        }
        div:nth-of-type(2) {
          flex: 5;
          font-size: 1.8rem;
          font-weight: bold;
          text-align: center;
          display: flex;
          justify-content: center;
          align-items: center;
        }
      }
    }
    .left_second_row {
      display: flex;
      margin-top: .3rem;
      flex: 1.5;
      width: 100%;
      justify-content: space-between;
      div:nth-of-type(1) {
        flex: 2.5;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 5rem;
      }
      div:nth-of-type(2) {
        flex: 1.75;
        margin-left: .3rem;
      }
      div:nth-of-type(3) {
        flex: 1.75;
        margin-left: .3rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        margin-top: .4rem;
        div:nth-of-type(1) {
          flex: 3;
          font-size: .7rem;
          display: flex;
          justify-content: space-between;
          flex-direction: column;
          div:nth-of-type(1) {
            flex: 1;
            width: 100%;
          }
          div:nth-of-type(2) {
            flex: 5;
            width: 100%;
            margin-top: 0;
          }
        }
        div:nth-of-type(2) {
          flex: 2;
          margin-left: 0;
          margin-top: .1rem;
          display: flex;
          div:nth-of-type(1) {
            flex: 3;
            margin-top: 0;
            display: flex;
            flex-direction: column;
            div:nth-of-type(1) {
              flex: 1;
              justify-content: center;
              align-items: center;
            }
            div:nth-of-type(2) {
              flex: 1;
              margin-left: 0;
              justify-content: center;
              align-items: center;
              font-weight: bold;
            }
          }
          div:nth-of-type(2) {
            flex: 2;
            margin-top: 0;
            margin-left: .2rem;
            display: flex;
            flex-direction: column;
            div:nth-of-type(1) {
              flex: 1;
              justify-content: center;
              align-items: center;
            }
            div:nth-of-type(2) {
              justify-content: center;
              align-items: center;
              flex: 1;
              margin-left: 0;
              font-weight: bold;
            }
          }
        }
      }
    }
  }
  .top_right {
    flex:1;
    display: flex;
    margin-left: .3rem;
    box-sizing: border-box;
    flex-direction: column;
    justify-content: space-between;
    div:nth-of-type(1) {
      flex: 1;
      display: flex;
      flex-direction: column;
      div:nth-of-type(1) {
        flex: 1;
        display: flex;
        justify-content: center;
        font-size: .7rem;
        flex-direction: row
      }
      div:nth-of-type(2) {
        flex: 4;
        font-size: 1.7rem;
        display: flex;
        justify-content: center;
        font-weight: bold;
        flex-direction: row;
      }
    }
    div:nth-of-type(2) {
      flex: 1;
      margin-top: .3rem;
      display: flex;
      flex-direction: column;
      div:nth-of-type(1) {
        flex: 1;
        display: flex;
        justify-content: center;
        font-size: .7rem;
        flex-direction: row;
        font-weight: bold;
      }
      div:nth-of-type(2) {
        flex: 4;
        display: flex;
        justify-content: center;
        font-weight: bold;
        flex-direction: row;
        align-items: center;
        font-size: 2.5rem;
      }
    }
    div:nth-of-type(3) {
      flex: 1;
      margin-top: .3rem; display: flex;
      flex-direction: column;
      div:nth-of-type(1) {
        flex: 1;
        display: flex;
        justify-content: center;
        font-size: .7rem;
        flex-direction: row;
        font-weight: bold;
      }
      div:nth-of-type(2) {
        flex: 4;
        font-size: 1.7rem;
        display: flex;
        justify-content: center;
        font-weight: bold;
        flex-direction: row;
        align-items: center;
        font-size: 2.5rem;
      }

    }
  }
}
.bottomItem {
  flex: 1;
  width: 70%;
  width: 70%;
  margin-top: .2rem;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  div:nth-of-type(1) {
    width: calc((100% - .9rem)/3);
    display: flex;
    flex-direction: column;
    div:nth-of-type(1) {
      flex: 1;
      width: 100%;
      flex-direction: row;
      font-size: .7rem;
      font-weight: bold;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    div:nth-of-type(2) {
      flex: 5;
      display: flex;
      width: 100%;
      flex-direction: row;
      justify-content: center;
      margin-left: 0;
      margin-top: 2rem;
    }
  }
  div:nth-of-type(2) {
    flex: 1;
    margin-left: .3rem;
    display: flex;
    flex-direction: column;
    div:nth-of-type(1) {
      flex: 4;
      width: 100%;
      display: flex;
      flex-direction: row;
      div:nth-of-type(1) {
        flex: 5;
        display: flex;
        flex-direction: column;
        div:nth-of-type(1) {
          flex: 1;
          display: flex;
          font-size: 1.5rem;
          justify-content: center;
        }
        div:nth-of-type(2) {
          flex: 1;
          display: flex;
          font-size: .9rem;
          font-weight: bold;
          justify-content: center;
          margin-left: 0;
        }
      }
      div:nth-of-type(2) {
        flex: 4;
        margin-left: .3rem;
        margin-top: 0;
        display: flex;
        justify-content: center;
        div:nth-of-type(1) {
          flex: 1;
          font-size: .7rem;
        }
        div:nth-of-type(2) {
          flex:4;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 1.2rem;
          span {
            font-size: 1.7rem;
          }
        }
      }
    }
    div:nth-of-type(2) {
      flex: 3;
      margin-top: .3rem;
      margin-left: 0;
      display: flex;
      flex-direction: row;
      div:nth-of-type(1) {
        flex: 4;
        display: flex;
        flex-direction: column;
        div:nth-of-type(1) {
          flex: 1;
        }
        div:nth-of-type(2) {
          flex: 4;
          margin-left: 0 ;
        }

      }
      div:nth-of-type(2) {
        flex: 5;
        margin-left: .3rem;
        margin-top: 0;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
  }
}
.CONVEY {
  font-size: .7rem!important;
  font-weight: normal!important;
}


</style>