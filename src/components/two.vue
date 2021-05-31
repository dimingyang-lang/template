<template>
  <div class="container">
    <div class="top">
      <div class="top_code">TJ-INTEX</div>
      <div class="top_center">
        <span class="sortNum">C</span>
        <div class="listShop">
          <div  class="shopName">品名:</div>
          <div  class="shopCode">480B BRACKET RR SEAT BACK STOPPER RH</div>
        </div>
      </div>
      <div class="supplier">
        <div class="supplierName">供应商编码:</div>
        <div class="supplierCode">0400-0</div>
      </div>
    </div>
    <div class="top_A">
      <div class="top_code_A">
        <div class="top_code_A_a">受入区分:</div>
        <div class="top_code_A_b">N1</div>
      </div>
      <div class="top_center_A">
        <div class="listShop_A">
          <div  class="shopName_A">品番:</div>
          <div  class="shopCode_A">71266-07030-00</div>
        </div>
        <div class="listShop_A_A">
          <div class="codeArea">
            <div  class="shopName_A_A">条码区:</div>
            <div  class="shopCode_A_A">71266-07030-00</div>
          </div>
          <div class="number">
            <div class="number_a">看板联号</div>
            <div class="number_b">9014</div>
          </div>
        </div>
      </div>
      <div class="supplier_A">
        <div class="supplierName_A">供应商名称:</div>
        <div class="supplierCode_A">山东丰达</div>
      </div>
    </div>
    <div class="bottom">
      <div class="bottom_a">
        <div class="bottom_a_name">收容数：</div>
        <div class="bottom_a_code">14</div>
      </div>
      <div class="bottom_b">
        <div class="bottom_b_a">背番:</div>
        <div class="bottom_b_b">F3R</div>
      </div>
      <div class="bottom_c">
        <div class="bottom_c_a">循环周期</div>
        <div class="bottom_c_b">1-2-2</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "two"
}
</script>

<style scoped lang="less">
  div {
    box-sizing: border-box;
  }
  .container {
    margin: 0 auto;
    background: lightgray;
    width:70%;
    height: 70%;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    .top {
      flex: 3;
      background: lightgray;
      display: flex;
      padding-bottom: 1rem;
      .top_code {
        flex:  7;
        background: white;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 3rem;
        font-style: italic;
        border: 1px solid black;
      }

      .top_center {
        margin-left: 4rem;
        flex:  20;
        background: white;
        display: flex;
        .sortNum {
          flex: 3;
          background: lightgray;
          display: flex;
          align-items: center;
          justify-content: center;
          font-size: 5rem;
          color: white;
        }
        .listShop{
          border: 1px solid black;
          flex: 17;
          display: flex;
          flex-direction: column;
          .shopName {
            display: flex;
            justify-content:flex-start;
            padding-left: 1rem;
            font-size: 2rem;
            flex: 3;
          }
          .shopCode {
            display: flex;
            justify-content: center;
            font-size: 2rem;
            flex: 3
          }

        }

      }
      .supplier {
        flex: 10;
        background: white;
        margin-left: 1rem;
        display: flex;
        flex-direction: column;
        border: 1px solid black;
        .supplierName {
          flex: 1;
          font-size: 1.8rem;
          padding-left: 1rem;
        }
        .supplierCode {
          flex: 2;
          display: flex;
          align-items: center;
          justify-content: center;
          font-size: 3rem;
          font-weight: bold;
        }
      }
    };
    .top_A {
      flex: 8;
      background: lightgray;
      display: flex;
      padding-bottom: 1rem;
      .top_code_A {
        border: 1px solid black;
        flex: 7;
        background: white;
        display: flex;
        flex-direction: column;
        .top_code_A_a {
          flex: 1;
          padding-left: 1rem;
          font-size: 1.5rem;
        }
        .top_code_A_b {
          flex: 5;
          display: flex;
          font-weight: bold;
          font-size: 10rem;
          justify-content: center;
          align-items: center;
        }
      }
      .top_center_A {
        flex:  20;
        background: white;
        margin-left: 4rem;
        display: flex;
        flex-direction: column;
        .listShop_A{
          border: 1px solid black;
          flex: 1;
          display: flex;
          flex-direction: column;
          .shopName_A {
            display: flex;
            justify-content:flex-start;
            padding-left: 1rem;
            font-size: 2rem;
            flex: 1;
          }
          .shopCode_A {
            display: flex;
            justify-content: center;
            font-size: 5rem;
            align-items: center;
            flex: 3;
            font-weight: bold;
          }
        }
        .listShop_A_A{
          margin-top: 1rem;
          border: 1px solid black;
          flex: 17;
          display: flex;
          .codeArea {
            display: flex;
            flex-direction: column;
            flex: 5;
            .shopName_A_A {
              display: flex;
              justify-content:flex-start;
              padding-left: 1rem;
              font-size: 2rem;
              flex: 1;
            }
            .shopCode_A_A {
              flex: 3;
              background: white;
              display: flex;
              align-items: flex-end;
              padding-left: 5rem;
            }
          }
          .number {
            margin-left: 1rem;
            border-left: 1px solid black;
            flex: 2;
            display: flex;
            flex-direction: column;
            .number_a {
              display: flex;
              justify-content:flex-start;
              padding-left: 1rem;
              font-size: 2rem;
              flex: 1;
            }
            .number_b {
              flex: 4;
              display: flex;
              justify-content: center;
              align-items: center;
              font-weight: bold;
              font-size: 5rem;
            }
          }

        }

      }
      .supplier_A {
        flex: 10;
        background: white;
        margin-left: 1rem;
        display: flex;
        flex-direction: column;
        border: 1px solid black;
        .supplierName_A {
          flex: 1;
          font-size: 1.8rem;
          padding-left: 1rem;
        }
        .supplierCode_A {
          flex: 5;
          display: flex;
          align-items: center;
          justify-content: center;
          font-size: 6rem;
          font-weight: bold;
        }
      }
    }

    .bottom {
      flex: 5;
      background: lightgray;
      display: flex;
      .bottom_a {
        flex: 7;
        background: white;
        border:1px solid black;
        display: flex;
        flex-direction: column;
        .bottom_a_name {
          padding-left: 1rem;
          font-size: 1.7rem;
          flex: 1;
        }
        .bottom_a_code {
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 5rem;
          font-weight: bold;
          flex: 5;
        }
      }
      .bottom_b {
        border:1px solid black;
        background: white;
        flex:  20;
        background: white;
        margin-left: 4rem;
        display: flex;
        flex-direction: column;
        .bottom_b_a {
          padding-left: 1rem;
          font-size: 1.8rem;
          flex: 1 ;
        }
        .bottom_b_b {
          padding-left: 1rem;
          font-size: 1.8rem;
          flex: 4 ;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 9rem;
          font-weight: bold;
        }
      }
      .bottom_c {
        flex: 10;
        background: white;
        margin-left: 1rem;
        border:1px solid black;
        .bottom_c_a {
          padding-left: 1rem;
          font-size: 1.8rem;
          flex: 1 ;
        }
        .bottom_c_b {
          padding-left: 1rem;
          font-size: 1.8rem;
          flex: 4 ;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 9rem;
          font-weight: bold;
        }
      }
    }
  }
</style>