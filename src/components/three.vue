<template>
  <div class="container" style="width: 100%;height: 70%;background: oldlace;margin-top: 10px" >
    <div class="topItem" style="border: 3px solid black">
      <div></div>
      <div>购入入入入入 <span style="padding: 0 1rem">原材料</span> </div>
      <div>天津丰田合成</div>
    </div>
    <div class="bottomItem" style="border: 3px solid black;border-top: 0">
      <div class="bottomLeft">
<!--        左边俩个，一个上一个下-->
<!--        这个是上-->
        <div class="bottomLeftTop">
          <div class="bottomLeftTop_left" style="border-right: 2px solid black">
            <div class="bottomLeftTop_left_top">
              <span>
                仕入先
              </span>
              <span>
                6410-0
              </span>
            </div>
            <div class="bottomLeftTop_left_bottom">
              <div class="bottomLeftTop_left_bottom_left">
                <span>箱子</span>
                <span>箱</span>
              </div>
              <div class="bottomLeftTop_left_bottom_right">
                <span>收容数</span>
                <span>25</span></div>
            </div>
          </div>
          <div class="bottomLeftTop_right">
            <div class="bottomLeftTop_right_top">
              <div class="fontName">
                品番 <span class="fontCode">TTG30-00905</span>
              </div>
              <div class="fontName">
                品名 <span class="fontCode">韩国乐天材WR-9120J</span>
              </div>
            </div>
            <div class="bottomLeftTop_right_bottom">
              <div class="null_content"></div>
              <div class="two_content">
                <div class="content_flex">
                  <div class="content">纳期</div>
                  <div class="date">2021/4/13</div>
                </div>
              </div>
              <div class="three_content"></div>
            </div>
          </div>
        </div>
<!--        这个是左边的下-->
        <div class="bottomLeftBottom" style="border-top: 1px solid black">
          <div class="bottomLeftBottom_left"></div>
          <div class="bottomLeftBottom_right">
            <div class="bottomLeftBottom_right_top">背番号</div>
            <div class="bottomLeftBottom_right_bottom">Y871</div>
            <div class="null_item"></div>
          </div>
        </div>
      </div>
      <div class="bottomRight" style="border-left:2px solid black ">
        <div>受入
          <div>2</div>
        </div>
        <div>第二工厂</div>
        <div class="last">
          <span>所番地</span>
          <span>7179</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "three"
}
</script>

<style scoped lang="less">
div {
  box-sizing: border-box;
}
  .container {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .topItem {
      width: 70%;
      flex: 1;
      display: flex;
      font-size:  1.8rem;
      font-weight: bold;
      div:nth-of-type(1) {
        flex: 2;

      }
      div:nth-of-type(2) {
        flex: 5;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      div:nth-of-type(3) {
        flex: 2;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
    .bottomItem{

      flex: 6;
      width: 70%;
      display: flex;
      .bottomLeft {
        flex: 7;
        display: flex;
        flex-direction: column;
        .bottomLeftTop {

          display: flex;
          flex: 3;
          .bottomLeftTop_left {
            flex: 2;
            display: flex;
            flex-direction: column;
            .bottomLeftTop_left_top {
              flex: 3;
              padding-left: 1rem;
              display: flex;
              display: flex;
              flex-direction: column;
              font-size: 1.5rem;
              span:nth-of-type(2) {
                font-size: 2.5rem;
                padding-top: 1rem;
                font-weight: bold;
              }
            }
            .bottomLeftTop_left_bottom {

              flex: 2;
              display: flex;
              display: flex;
              .bottomLeftTop_left_bottom_left {
                flex: 1;
                padding-left: 1rem;
                flex-direction: column;
                font-size: 1.5rem;
                span:nth-of-type(2) {
                  font-size: 2.5rem;
                  padding-top: 1rem;
                  font-weight: bold;
                  display: flex;
                  justify-content: center;
                }
              }
              .bottomLeftTop_left_bottom_right {

                padding-left: 1rem;
                flex: 1;
                display: flex;
                flex-direction: column;
                font-size: 1.5rem;
                span:nth-of-type(2) {
                  font-size: 2.5rem;
                  padding-top: 1rem;
                  font-weight: bold;
                  display: flex;
                  justify-content: center;
                }
              }
            }
          }
          .bottomLeftTop_right {
            flex: 5;
            display: flex;
            flex-direction: column;

            .bottomLeftTop_right_top {

              flex: 1;
              .fontName {
                font-size: 1.5rem;
                padding-left: 1rem;
              }
              .fontCode {
                font-size: 2.5rem;
                padding-left: 1rem;
                font-weight: bold
              }
            }
            .bottomLeftTop_right_bottom {
              flex: 2;
              display: flex;
              .null_content{
                flex: 1;
              }
              .two_content {
                flex: 2;
                display: flex;
                justify-content: flex-end;
                align-items: flex-end;
                .content_flex {
                  .content {
                    transform: translateX(-1rem);
                    margin-bottom:1rem;
                    font-size: 1.7rem;
                  }
                  .date {
                    font-size: 3rem;
                    font-weight: bold;
                  }
                }
              }
              .three_content {
                flex: 1;
              }
            }

          }
        }
        .bottomLeftBottom {
          display: flex;
          flex: 2;


          .bottomLeftBottom_left {
            flex: 3;
          }
          .bottomLeftBottom_right {

            flex: 2;
            display: flex;
            flex-direction: column;
            .bottomLeftBottom_right_top {
              flex: 1;
              padding-left: 1rem;
              display: flex;
              align-items: flex-end;
              font-size: 1.7rem;
            }
            .bottomLeftBottom_right_bottom {
              flex: 4;
              font-weight: bold;
              font-size: 8rem;
              padding-left: 6rem;
              line-height: 1;
            }
          }
        }
      }
      .bottomRight {

        flex: 2;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
       div {
         padding-left: 1rem;
         flex: 1;
         font-size: 1.7rem;
       }
        div:nth-of-type(1) {
          margin-top: 3rem;
          div {
            font-size: 2.5rem;
          }
        }
        .last {
          padding: 0;
          display: flex;
          flex-direction: column;
          justify-content: space-between;

          span:nth-of-type(1) {
            padding-left: 1rem;
          }
          span:nth-of-type(2) {
            align-self: flex-end;
          }
        }
      }
    }
  }

</style>