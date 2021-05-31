<template>
  <div>

    <ConditionQuery style="margin-left: 30px">
      <div class="topFormInput display_flex_wrap marginTop" style="font-size:14px;margin-bottom:30px;">
        <span class="" style="line-height:40px;margin-right:5px">供应商 : </span>
        <el-autocomplete
            class="inline-input"
            clearable
            v-model="input_supplierName"
            :fetch-suggestions="searchResults"
            :disabled = "dis_abled"
            placeholder="请选择"
            @input="inputSupplierNameAndCode()"
            style="width:230px"
        ></el-autocomplete>
        <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
        >物料编码:
        </span>
        <el-select
            v-model="input_skuCode"
            placeholder="请选择"
            style="width: 180px"
            clearable
            filterable
        >
          <el-option
              v-for="(item, index) in productCode"
              :key="index"
              :value="item.code"
          ></el-option>
        </el-select>
        <span class="" style="line-height: 40px; margin-right: 5px;margin-left: 20px"
        >月份:
          </span>
        <el-date-picker
            :clearable="false"
            ref="input_month"
            style="margin-left: 15px; width: 150px"
            v-model="input_month"
            format="yyyy-MM"
            value-format="yyyy-MM-dd HH:mm:ss"
            type="month"
            placeholder="选择月"
        >
        </el-date-picker>

        <!-- <el-select v-model="input_supplierCode" clearable filterable>
          <el-option v-for="(item,index) in originSupplierNames" :key="index" :label="item.name" :value="item.code"></el-option>
        </el-select> -->


        <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff" @click="inputParam_a()">查 询</el-button>
        <el-button style="margin-left: 10px;height:40px" @click="changeBlankToNull()">重 置</el-button>
        <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff" @click="exportAll()">Excel导出</el-button>
        <!-- <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff" @click="inputParam()">刷 新</el-button> -->
      </div>
    </ConditionQuery>
    <SearchTitle style="margin-left: 30px">

    </SearchTitle>
    <!-- 入库明细dialog -->
    <el-dialog
        title="入库明细"
        center :visible.sync="inStockOr"
        width="70vw"
        top="5vh"
        @close="clearSafeQuantity()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
    <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
    >日期:
        </span>

      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="value1"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>

      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff;width: 6rem" @click="inStockDetailQuery()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcel()">Excel导出</el-button>
      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="inStockData"
          stripe
          fit
          style="width: 100%;padding-top:  2rem"
      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>


        <el-table-column
            align="center"
            prop="inOrderNo"
            label="入库单号"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="inOrderQuantity"
            label="入库数量"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="inTime"
            label="入库时间"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="入库人"
            prop="inUserName"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>
    <!-- 出库明细dialog -->
    <el-dialog
        title="出库明细"
        center :visible.sync="outStockOr"
        width="70vw"
        top="5vh"
        @close="clearSafeQuantity()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
       <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
       >客户:
        </span>
      <el-select
          v-model="customer"
          placeholder="请选择"
          style="width: 180px"
          clearable
          filterable
      >
        <el-option
            v-for="(item, index) in customerDrop"
            :key="index"
            :value="item.code"
            :label="item.name"
        ></el-option>
      </el-select>
      <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
      >日期:
        </span>

      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="value2"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="inputParamOut()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcel1()">Excel导出</el-button>
      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="outStockData"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"

      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>


        <el-table-column
            align="center"
            prop="outOrderNo"
            label="出库单号"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="outOrderQuantity"
            label="出库数量"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="outTime"
            label="出库时间"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="出库人"
            prop="outUserName"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="客户"
            prop="customerName"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>
<!--    数据调整dia-->
    <el-dialog
        title="数据调整"
        center :visible.sync="dataFillOr"
        width="70vw"
        top="5vh"
        @close="clearDataFill()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
       <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
       >调整类型:
        </span>
      <el-select
          v-model="modifyType"
          placeholder="请选择"
          style="width: 180px"
          clearable
          filterable
      >
        <el-option
          label="盘点"
          value="inventory"
        ></el-option>
        <el-option
          label="排查"
          value="investigation"
        ></el-option>
      </el-select>
      <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
      >日期:
        </span>

      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="value3"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="dataFillQuery()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcel2()">Excel导出</el-button>
      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="dataFillList"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"

      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="modifyTime"
            label="调整时间"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="modifyTypeName"
            label="调整类型名称"
            show-overflow-tooltip
        >
        </el-table-column>


        <el-table-column
            align="center"
            prop="originalSupplierCode"
            label="原供应商编码"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="originalSkuCode"
            label="原供物料编码"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="originalQuantity"
            label="原数量"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="新供应商编码"
            prop="newSupplierCode"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="新供物料编码"
            prop="newSkuCode"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="新数量"
            prop="newQuantity"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="调整人姓名"
            prop="modifyUserName"
            show-overflow-tooltip
        >
        </el-table-column>

        <el-table-column
            align="center"
            label="业务单号"
            prop="orderNo"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>
<!--    本期结存合格品-->
    <el-dialog
        title="结存合格品明细"
        center :visible.sync="thegood"
        width="70vw"
        top="5vh"
        @close="clearTheGood()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
      <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
      >日期:
        </span>
      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="dateTheGoodL"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="inputParamOutTheGood()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcelGood()">Excel导出</el-button>
      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="theGoodList"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"
      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="statisticsDateStr"
            label="日期"
            width="280"
            show-overflow-tooltip
        >  </el-table-column>

       <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>

        <el-table-column
            align="center"
            prop="goodQuantity"
            label="结存合格品数量"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>

<!--    本期结存不良品-->
    <el-dialog
        title="结存不良品明细"
        center :visible.sync="thebad"
        width="70vw"
        top="5vh"
        @close="clearTheBad()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
      <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
      >日期:
        </span>
      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="dateTheGoodL"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="inputParamOutTheBad()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcelBad()">Excel导出</el-button>
      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="theBadList"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"
      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="statisticsDateStr"
            label="日期"
            width="280"
            show-overflow-tooltip
        >  </el-table-column>

        <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>

        <el-table-column
            align="center"
            prop="failedQuantity"
            label="结存不良品数量"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>
    <!-- 不良品入库明细dialog -->

    <el-dialog
        title="不良品入库明细"
        center :visible.sync="badInStockOr"
        width="70vw"
        top="5vh"
        @close="clearSafeQuantity()"
        :close-on-click-modal="false"
        :destroy-on-close="true">

       <span class="marginLeft" style="line-height: 40px; margin-right: 5px"
       >日期:
        </span>
      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="badInstockDate"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="getBadDetail()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcelBad()">Excel导出</el-button>

      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="badInStockData"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"
      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>


        <el-table-column
            align="center"
            prop="inOrderNo"
            label="入库单号"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="defectiveNo"
            label="明细单号"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="inOrderQuantity"
            label="入库数量"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="入库时间"
            prop="inTime"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="入库人"
            prop="inUserName"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="客户"
            prop="customerName"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>

    <!-- 不良品返厂明细dialog -->
    <el-dialog
        title="不良品返厂明细"
        center :visible.sync="badReturnOr"
        width="70vw"
        top="5vh"
        @close="clearReturn()"
        :close-on-click-modal="false"
        :destroy-on-close="true">
      <el-date-picker
          style="width: 16rem"
          :clearable="false"
          v-model="badReturnDate"
          value-format="yyyy-MM-dd HH:mm:ss"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期">
      </el-date-picker>
      <el-button style="margin-left: 10px;height:40px;backgroundColor:#f56c6c;color:#fff; width: 6rem" @click="getBadRetun()">查 询</el-button>
      <el-button class="marginLeft" style="background:#f56c6c;color:#fff; width: 6rem" @click="checkExportExcelBad()">Excel导出</el-button>

      <el-table
          show-summary
          :summary-method="getSummaries"
          :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
          :data="badReturnData"
          stripe
          fit
          style="width: 100%;padding-top: 2rem"
      >
        <el-table-column
            align="center"
            label="行号"
            type="index"
            width="60px"
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuCode"
            label="物料编码"
            width="280"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="skuName"
            label="物料名称"
            show-overflow-tooltip
        >
        </el-table-column>


        <el-table-column
            align="center"
            prop="defectiveNo"
            label="明细单号"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="returnQuantity"
            label="返厂数量"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            prop="returnTime"
            label="返厂时间"
            show-overflow-tooltip
        >
        </el-table-column>
        <el-table-column
            align="center"
            label="返厂操作人"
            prop="returnUserName"
            show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
      </div>
    </el-dialog>
    <div class="searchTable" style="margin-left: 30px">
      <template>
                <el-table
                    :row-style="changeHeight"
                    show-summary
                    :summary-method="getSummaries"
                    :header-cell-style="{ backgroundColor: '#d9d9d9', color: '#333' }"
                    :data="mainData"
                    stripe
                    fit
                    style="width: 100%"
                >
                  <el-table-column
                      align="center"
                      label="行号"
                      width="60px"
                      height="44px"
                  >
                    <template slot-scope="scope">
                      <span>{{ scope.$index + (pageNum - 1) * pageSize + 1 }}</span>
                    </template>
                  </el-table-column>
                  <el-table-column
                      align="center"
                      prop="skuCode"
                      label="物料编码"
                      width="280"
                      show-overflow-tooltip
                  >
                  </el-table-column>
                  <el-table-column
                      align="center"
                      prop="skuName"
                      label="物料名称"
                      show-overflow-tooltip
                  >
                  </el-table-column>
                  <el-table-column
                      align="center"
                      prop="lastGoodQuantity"
                      label="上期结转合格品"
                      show-overflow-tooltip
                  >
                  </el-table-column>
                  <el-table-column
                      align="center"
                      prop="lastFailedQuantity"
                      label="上期结转不良品"
                      show-overflow-tooltip
                  >
                  </el-table-column>
                  <el-table-column
                      align="center"
                      label="本期入库"
                      show-overflow-tooltip
                      prop="inStoreQuantity">
                    <template slot-scope="scope">
                      <el-button
                          @click="openInstock(scope.row)"
                          size="mini"
                           type="text"
                           style="fontSize:14px"> {{scope.row.inStoreQuantity}}</el-button>
                    </template>
                  </el-table-column>
                    <el-table-column
                        align="center"
                        prop="outStoreQuantity"
                        label="本期出库"
                        show-overflow-tooltip
                    >
                      <template slot-scope="scope">
                        <el-button
                            @click="openOutstock(scope.row)"
                            size="mini"
                            type="text"
                            style="fontSize:14px"> {{scope.row.outStoreQuantity}}</el-button>
                      </template>
                  </el-table-column>
                  <el-table-column
                        align="center"
                        prop="modifyQuantity"
                        label="数据调整"
                        show-overflow-tooltip
                    >
                      <template slot-scope="scope">
                        <el-button
                            @click="dataFill(scope.row)"
                            size="mini"
                            type="text"
                            style="fontSize:14px"> {{scope.row.modifyQuantity}}</el-button>
                      </template>
                  </el-table-column>
                  <el-table-column
                      align="center"
                      prop="thisGoodQuantity"
                      label="本期结存合格品"
                      show-overflow-tooltip
                  >
                    <template slot-scope="scope">
                      <el-button
                          @click="openTheGood(scope.row)"
                          size="mini"
                          type="text"
                          style="fontSize:14px">{{scope.row.thisGoodQuantity}}</el-button>
                    </template>
                  </el-table-column>
                    <el-table-column
                        align="center"
                        prop="thisFailedQuantity"
                        label="本期结存不良品"
                        show-overflow-tooltip
                    >
                      <template slot-scope="scope">
                        <el-button
                            @click="openTheBad(scope.row)"
                            size="mini"
                            type="text"
                            style="fontSize:14px"> {{scope.row.thisFailedQuantity}}</el-button>
                      </template>
                  </el-table-column>
                    <el-table-column
                        align="center"
                        label="不良品入库"
                        show-overflow-tooltip
                        prop="failedInQuantity"
                    >
                      <template slot-scope="scope">
                        <el-button
                            @click="badInstock(scope.row)"
                            size="mini"
                            type="text"
                            style="fontSize:14px"> {{scope.row.failedInQuantity}}</el-button>
                      </template>
                  </el-table-column>
                    <el-table-column
                        align="center"
                        label="不良品返厂"
                        show-overflow-tooltip
                        prop="failedReturnQuantity"
                    >
                      <template slot-scope="scope">
                        <el-button
                            @click="badReturn(scope.row)"
                            size="mini"
                            type="text"
                            style="fontSize:14px"> {{scope.row.failedReturnQuantity}}</el-button>
                      </template>
                  </el-table-column>
                </el-table>

      </template>

    </div>
    <div class="page marginTop">
      <el-pagination
          align="center"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="pageNum"
          :page-sizes="pageSizes"
          :page-size="pageSize"
          background
          layout="total, sizes, prev, pager, next"
          :total="totalTable"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: "statisticsAndDetails",
  data(){
    return {
      modifyType:"",
      C:{},
      dataFillType:"",
      dataFillList:[],
      badInstockInfo:{},
      badReturnInfo:{},
      badInstockDate:[],
      badReturnDate:[],
      theGoodskuandsup:{},
      theBadskuandsup:{},
      theGoodList:[],
      theBadList:[],
      dateTheGoodL:[],
      supplierCodep:"",
      a:{},
      value1:[],
      value2:[],
      value3:[],
      c:'',
      dis_abled: false,
      pageSizes: [5,10,20,50],
      pageSize: 10,
      pageNum:1,
      currentPage: 1,
      totalTable: 0,
      A:{},
      customer:"",
      lo:'',
      input_month:'',
      customerDrop:[],
      inStockOr:false,
      outStockOr:false,
      dataFillOr:false,
      badInStockOr:false,
      badReturnOr:false,
      thegood:false,
      thebad:false,
      originSupplierNames:[],
      supplierNames: [],
      input_skuCode:null,
      input_supplierCode:null,
      input_supplierName: null,
      productCode:[],
      search_skuCode:'',
      search_supplierCode :'',
      search_supplierName:'',
      search_day_start: null,
      search_day_end: null,
      mainData:[],
      inStockData:[],
      outStockData:[],
      badInStockData:[],
      badReturnData:[],
      mainPager:{},
      pickerOptions: {
        shortcuts: [
          {
            text: "今天",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一周",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit("pick", [start, end]);
            },
          },
        ],
      },

    }
  },
  computed:{
  },
  watch: {
    mainData: {
      handler:function (a,b) {
        let arr = []
        Object.keys(a[0]).forEach((item, index) => {
          arr[index] = 0
        })
        arr[0] = '合计'
        arr[1] = ''
        arr[2] = ''
        a.forEach(item => {
          arr[3] += Number(item.lastGoodQuantity)
          arr[4] += Number(item.lastFailedQuantity)
          arr[5] += Number(item.inStoreQuantity)
          arr[6] += Number(item.outStoreQuantity)
          arr[7] += Number(item.thisGoodQuantity)
          arr[8] += Number(item.thisFailedQuantity)
          arr[9] += Number(item.failedInQuantity)
          arr[10] += Number(item.failedReturnQuantity)
        })
      },
      // handler: function(newName, oldName) {
      //   console.log(9993);
      //   if (this.mainData.length>0) {
      //     this.$nextTick(() => {
      //       // 改变合计行样式
      //       const s_table = document.getElementsByClassName('el-table__footer-wrapper')[0]
      //       console.log(s_table)
      //       // console.log(s_table)
      //
      //       const child_tr = s_table.getElementsByTagName('tr')[0]
      //       console.log(child_tr)
      //       child_tr.childNodes.forEach(item => {
      //         item.setAttribute('style', 'color:black')
      //       })
      //
      //     })
      //   }
      // },
      immediate: true,
      deep: true
    }
  },
  methods:{
    getBadRetun() {
      this.postURL('core/biz/statistics/finance/queryDefectiveReturnDetail',{
        queryDateMin:this.badReturnDate[0],
        queryDateMax:this.badReturnDate[1],
        supplierCode:this.badReturnInfo.supplierCode,
        skuCode:this.badReturnInfo.skuCode
      },{}).then(res=> {
        this.badReturnData = res.data
        console.log(this.badReturnData);
      })
    },
    clearTheGood() {
      this.theGoodskuandsup={},
      this.theGoodList=[]
    },
    clearDataFill(){
      this.dataFillList=[]
      this.C={}
      this.modifyType=""
    },
    clearTheBad(){
      this.theBadskuandsup={},
      this.theBadList=[]
    },
    openTheGood(res) {
      this.dateTheGoodL=[this.current(),this.current()]
      this.theGoodskuandsup={supplierCode:res.supplierCode,skuCode:res.skuCode}
      this.thegood=true;
      this.postURL('core/biz/statistics/finance/querySkuDailyStore',
      {
          "skuCode":res.skuCode,
          "supplierCode":res.supplierCode,
          "queryDateMin":this.dateTheGoodL[0],
          "queryDateMax":this.dateTheGoodL[1]
      }).then(res=> {
        if(res.status==200) {

          this.theGoodList=res.data
        }else {
          this.$message.error("查询失败,稍后重试")
        }
      })
    },
    openTheBad(res) {
      this.theBadskuandsup={supplierCode:res.supplierCode,skuCode:res.skuCode}
      this.dateTheGoodL=[this.current(),this.current()]
      console.log(res);
      this.thebad=true;
      this.postURL('core/biz/statistics/finance/querySkuDailyStore',
      {
          "skuCode":res.skuCode,
          "supplierCode":res.supplierCode,
          "queryDateMin":this.dateTheGoodL[0],
          "queryDateMax":this.dateTheGoodL[1]
      }).then(res=> {
        console.log(this.theBadList);
        if(res.status==200) {
          this.theBadList=res.data
        }else {
          this.$message.error("查询失败,稍后重试")
        }
      })
    },
    checkExportExcel(){
      this.postURLblob('core/biz/statistics/finance/inDetailExcelExport',{
        "skuCode":this.a.skuCode,
        "supplierCode":this.a.supplierCode,
        "queryDateMin":this.value1[0],
        "queryDateMax":this.value1[1],
      },{}).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },
    checkExportExcel1(){
      this.postURLblob('core/biz/statistics/finance/outDetailExcelExport',{
        "skuCode":this.A.skuCode,
        "queryDateMin":this.value2[0],
        "queryDateMax":this.value2[1],
        "customerCode":this.customer,
        "supplierCode":this.A.supplierCode,
      },{}).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },


    checkExportExcelGood(){
      this.postURLblob('core/biz/statistics/finance/querySkuDailyStoreExport',{
        "skuCode":this.theGoodskuandsup.skuCode,
        "queryDateMin":this.dateTheGoodL[0],
        "queryDateMax":this.dateTheGoodL[1],
        "supplierCode":this.theGoodskuandsup.supplierCode
      },{}).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },
    checkExportExcelBad(){
      this.postURLblob('core/biz/statistics/finance/querySkuDailyStoreExport',{
        "skuCode":this.theBadskuandsup.skuCode,
        "queryDateMin":this.dateTheGoodL[0],
        "queryDateMax":this.dateTheGoodL[1],
        "supplierCode":this.theBadskuandsup.supplierCode
      },{}).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },
    changeHeight({ row, rowIndex}){
      if (rowIndex === 1) {
        console.log(rowIndex)
        return
        {height:'44px'}

      }
    },
    handleSizeChange(a) {
      console.log(a);
      this.pageSize=a
      this.getTable()
    },
    handleCurrentChange(a) {
      console.log(a);
      this.pageNum=a
      this.getTable()
    },
    //出库明细
    inputParamOut(){
      console.log(this.value2==null);
      if(this.value2==null||this.value2.length!==2) {
        this.$message.error('请输入日期')
      }
      else {
        this.postURL('core/biz/statistics/finance/queryOutStoreDetail',{
          queryDateMin:this.value2[0],
          queryDateMax:this.value2[1],
          supplierCode:this.A.supplierCode,
          skuCode:this.A.skuCode,
          customerCode:this.customer,

        },{}).then(res=> {
          this.outStockData = res.data
          console.log(this.outStockData);
        })
      }

    },
    inputParamOutTheGood(){
      if(this.dateTheGoodL==null||this.dateTheGoodL.length!==2)  {
        this.$message.error('请输入日期')
      }
      else {
        this.postURL('core/biz/statistics/finance/querySkuDailyStore',{
          queryDateMin:this.dateTheGoodL[0],
          queryDateMax:this.dateTheGoodL[1],
          supplierCode:this.theGoodskuandsup.supplierCode,
          skuCode:this.theGoodskuandsup.skuCode,
        },{}).then(res=> {
          this.theGoodList= res.data
          this.theBadList=res.data;
          console.log(this.theGoodList);
        })
      }

    },
    outStockDetailQuery(){},
    badInstock(a){
      this.badInstockDate=[this.input_month,this.c]
      this.badInstockInfo= {
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      }
      console.log(a);
      this.badInStockOr= true
      this.ve()
      this.postURL('core/biz/statistics/finance/queryDefectiveInDetail',{
        queryDateMin:this.input_month,
        queryDateMax:this.c,
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      },{}).then(res=> {
        this.badInStockData = res.data
        console.log(this.badInStockData);
      })
    },
    //不良品入库明细查询
    getBadDetail() {
      if(this.badInstockDate==null||this.badInstockDate.length!==2)  {
        this.$message.error('请输入日期')
      }else {
        this.postURL('core/biz/statistics/finance/queryDefectiveInDetail',{
          queryDateMin:this.badInstockDate[0],
          queryDateMax:this.badInstockDate[1],
          supplierCode:this.badInstockInfo.supplierCode,
          skuCode:this.badInstockInfo.skuCode,
        },{}).then(res=> {
          this.badInStockData=res.data;
          console.log(this.theBadList);
        })
      }
    },
    inputParamOutTheBad(){
      if(this.dateTheGoodL==null||this.dateTheGoodL.length!==2)  {
        this.$message.error('请输入日期')
      }
      else {
        this.postURL('core/biz/statistics/finance/querySkuDailyStore',{
          queryDateMin:this.dateTheGoodL[0],
          queryDateMax:this.dateTheGoodL[1],
          supplierCode:this.theBadskuandsup.supplierCode,
          skuCode:this.theBadskuandsup.skuCode,
        },{}).then(res=> {
          this.theBadList=res.data;
          console.log(this.theBadList);
        })
      }
    },
    clearSafeQuantity() {
      this.inStockData=[]
      this.outStockData=[]
      this.badInStockData=[]
      this.badReturnData=[]
      this.customer=""
      this.theBadskuandsup={}
    },
    clearReturn() {
      this.badReturnDate=[]
    },
    getCoustom() {
      this.getURL('core/sys/customer/listCustomerInfoSource').then(res=>{
        this.customerDrop=res.data
        console.log(this.customerDrop);
      })
    },

    openInstock(a){
      this.a=a
      console.log(a);
      this.inStockOr = true
      this.value1=[this.input_month,this.c];
      this.postURL('core/biz/statistics/finance/queryInStoreDetail',{
        queryDateMin:this.value1[0],
        queryDateMax:this.value1[1],
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      },{}).then(res=> {
        this.inStockData = res.data
      })

    },
    inStockDetailQuery() {
      this.postURL('core/biz/statistics/finance/queryInStoreDetail',{
        queryDateMin:this.value1[0],
        queryDateMax:this.value1[1],
        supplierCode:this.a.supplierCode,
        skuCode:this.a.skuCode
      },{}).then(res=> {
        this.inStockData = res.data
      })

    },
    dataFill(a) {
      this.C=a
      this.dataFillOr=true
      this.value3=[this.input_month,this.c];
      this.postURL('core/biz/statistics/finance/queryQuantityModifyDetail',{
        queryDateMin:this.value3[0],
        queryDateMax:this.value3[1],
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      }).then(res=>{
        this.dataFillList=res.data
      })
    },
    dataFillQuery(){
      if(this.value3==null||this.value3.length!==2) {
        this.$message.error('请输入日期')
      }
      else {
        this.postURL('core/biz/statistics/finance/queryQuantityModifyDetail',{
          queryDateMin:this.value3[0],
          queryDateMax:this.value3[1],
          supplierCode:this.C.supplierCode,
          skuCode:this.C.skuCode,
          modifyType:this.modifyType
        },{}).then(res=> {
          this.dataFillList = res.data
          console.log(this.dataFillList);
        })
      }
    },
    checkExportExcel2(){
      this.postURLblob('core/biz/statistics/finance/quantityModifyDetailExport',{
        queryDateMin:this.value3[0],
        queryDateMax:this.value3[1],
        supplierCode:this.C.supplierCode,
        skuCode:this.C.skuCode,
        modifyType:this.modifyType
      },{}).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },
    openOutstock(a){
      this.supplierCodep=a.supplierCode
      this.value2=[this.input_month,this.c];
      this.A=a
      console.log(a);
      this.outStockOr = true
      this.postURL('core/biz/statistics/finance/queryOutStoreDetail',{
        queryDateMin:this.value2[0],
        queryDateMax:this.value2[1],
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      },{}).then(res=> {
        this.outStockData = res.data
        console.log(this.outStockData);
      })
    },

    badReturn(a){
      this.ve()
      this.badReturnInfo={
        supplierCode:a.supplierCode,
        skuCode:a.skuCode,
      }
      this.badReturnDate=[this.input_month,this.c]
      console.log(a);
      this.badReturnOr= true
      this.postURL('core/biz/statistics/finance/queryDefectiveReturnDetail',{
        queryDateMin:this.input_month,
        queryDateMax:this.c,
        supplierCode:a.supplierCode,
        skuCode:a.skuCode
      },{}).then(res=> {
        this.badReturnData = res.data
        console.log(this.badReturnData);
      })
    },
    getSummaries(param) {
      const { columns, data } = param;
      const sums = [];
      columns.forEach((column, index) => {
        if (index === 0) {
          sums[index] = '合计';
          return;
        }
        const values = data.map(item => Number(item[column.property]));
        if (!values.every(value => isNaN(value))) {
          sums[index] = values.reduce((prev, curr) => {
            const value = Number(curr);
            if (!isNaN(value)) {
              return prev + curr;
            } else {
              return prev;
            }
          }, 0);
          sums[index] += '';
        } else {
          sums[index] = '';
        }
      });
      let sum=sums.map(item=> item=="0"?"0":item)
      console.log(sum);
      return sum

    },
    clearEmpty() {
      if (this.input_date != [] && !this.input_date) {
        this.input_date = [];
      }
    },
    ve(){
      if(this.input_month.length<7) {
        this.input_month+="-01 00:00:00"
      }
      let a = this.input_month.split("-");
      console.log(a);
      let A=a[2].split(" ")
      console.log(A);
      let b= new Date(a[0],a[1],0).getDate();
      console.log(b);
      this.c = a[0]+'-'+a[1]+'-'+b+' '+A[1];
    },
    getTable() {
      this.ve()
      console.log(666);
      this.postURL( "core/biz/statistics/finance/queryInAndOutDataInfo",{
        supplierCode:sessionStorage.getItem('supplierCode')||this.input_supplierCode,
        skuCode:this.input_skuCode,
        queryDateMin:this.input_month,
        queryDateMax:this.c,
      },{
        pageSize:this.pageSize,
        pageNum:this.pageNum,
      }).then((res) => {
        if(res.status==400) {
          this.$message.error(res.data)
        }
        this.totalTable = res.pager.total;
        this.mainData = res.data
        this.mainPager = res.pager
      }).catch(error=>{});
      let that =this

      setTimeout(()=>{
        console.log(document.querySelector('.el-table__footer').querySelectorAll("td")[5].innerText);

        if(document.querySelector('.el-table__footer').querySelectorAll("td")[5].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[5].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[5].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[5].onclick=function () {
            that.a={}
            console.log(that)
            that.ve()
            that.value1=[that.input_month,that.c]
            that.a.supplierCode=that.input_supplierCode
            that.postURL('core/biz/statistics/finance/queryInStoreDetail',{
              queryDateMin:that.input_month,
              queryDateMax:that.c,
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {
              if(res.status==200) {
                that.inStockOr=true
                that.inStockData = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[6].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[6].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[6].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[6].onclick=function () {
            that.A={}
            console.log(that)
            that.ve()
            that.value2=[that.input_month,that.c]
            console.log(that.input_supplierCode);
            that.A.supplierCode=that.input_supplierCode
            that.postURL('core/biz/statistics/finance/queryOutStoreDetail',{
              queryDateMin:that.input_month,
              queryDateMax:that.c,
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {

              if(res.status==200) {
                that.outStockOr = true
                that.outStockData = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[7].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[7].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[7].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[7].onclick=function () {
            that.ve()
            console.log(999);
            console.log(that.c);
            that.value3=[that.input_month,that.c]
            that.C.supplierCode=that.input_supplierCode
            that.postURL('core/biz/statistics/finance/queryQuantityModifyDetail',{
              queryDateMin:that.input_month,
              queryDateMax:that.c,
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {
              if(res.status==200) {
                that.dataFillOr = true
                that.dataFillList = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[8].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[8].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[8].style.cursor ='pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[8].onclick=function () {
            that.dateTheGoodL=[that.current(),that.current()]
            that.theGoodskuandsup={supplierCode:that.input_supplierCode,skuCode:""}
            that.A={}
            console.log(that)
            // that.ve()
            // that.dateTheGoodL=that.value2
            console.log(that.input_supplierCode);
            that.A.supplierCode=that.input_supplierCode
            that.postURL('core/biz/statistics/finance/querySkuDailyStore',{
              queryDateMin:that.dateTheGoodL[0],
              queryDateMax:that.dateTheGoodL[1],
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {

              if(res.status==200) {
                that.thegood= true
                that.theGoodList = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[9].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[9].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[9].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[9].onclick=function () {
            that.dateTheGoodL=[that.current(),that.current()]
            that.theBadskuandsup={supplierCode:that.input_supplierCode,skuCode:""}
            console.log(that)
            // that.ve()
            // that.dateTheGoodL=that.value2
            console.log(that.input_supplierCode);
            that.postURL('core/biz/statistics/finance/querySkuDailyStore',{
              queryDateMin:that.dateTheGoodL[0],
              queryDateMax:that.dateTheGoodL[1],
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {

              if(res.status==200) {
                that.thebad= true
                console.log(5555555)
                that.theBadList = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[10].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[10].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[10].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[10].onclick=function () {
            that.ve()
            that.badInstockDate=[that.input_month,that.c]
            that.badInstockInfo={supplierCode:that.input_supplierCode,skuCode:""}
            console.log(that)

            // that.dateTheGoodL=that.value2
            console.log(that.input_supplierCode);
            that.postURL('core/biz/statistics/finance/queryDefectiveInDetail',{
              queryDateMin:that.badInstockDate[0],
              queryDateMax:that.badInstockDate[1],
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {
              if(res.status==200) {
                that.badInStockOr= true
                that.badInStockData = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
        if(document.querySelector('.el-table__footer').querySelectorAll("td")[11].innerText!==""){
          document.querySelector('.el-table__footer').querySelectorAll("td")[11].style.color="#409EFF"
          document.querySelector('.el-table__footer').querySelectorAll("td")[11].style.cursor = 'pointer'
          document.querySelector('.el-table__footer').querySelectorAll("td")[11].onclick=function () {
            that.ve()
            that.badReturnDate=[that.input_month,that.c]
            that.badReturnInfo={supplierCode:that.input_supplierCode,skuCode:""}
            console.log(that)

            // that.dateTheGoodL=that.value2
            console.log(that.input_supplierCode);
            that.postURL('core/biz/statistics/finance/queryDefectiveReturnDetail',{
              queryDateMin:that.badReturnDate[0],
              queryDateMax:that.badReturnDate[1],
              supplierCode:that.input_supplierCode,
            },{}).then(res=> {
              if(res.status==200) {
                that.badReturnOr= true
                that.badReturnData = res.data
              }
              else  {
                this.$message.error('响应出错了,请稍后重试')
              }
            })
          }
        }
      },1500)
     // document.querySelector('.el-table__footer').querySelectorAll("td")[6]
    },
    getSupplierName() {
      this.postURL("core/sys/supplier/querySupplierDropList").then((res) => {
        console.log(res)
        if (sessionStorage.getItem('roleName') == "供应商") {
          this.dis_abled = true
          res.data.forEach((item)=>{
            if (item.code == sessionStorage.getItem('supplierCode')) {
              this.input_supplierName = item.code + "" + item.name;
              this.input_supplierCode = item.code
            }
          })
        } else {
          this.dis_abled = false
          this.originSupplierNames = res.data;
          res.data.forEach((item) => {
            let obj = new Object();
            obj.value = item.code + "" + item.name;
            obj.id = item.code;
            this.supplierNames.push(obj);
          });
        }
        
      });
    },
    searchResults(queryString, cb) {
      let results = queryString
          ? this.supplierNames.filter(this.supplierFilter(queryString))
          : this.supplierNames;
      cb(results);
    },
    //过滤函数
    supplierFilter(queryString) {
      return (res) => {
        return res.value.toLowerCase().includes(queryString.toLowerCase());
      };
    },
    inputParam_a() {
      this.pageSize=10, this.pageNum=1,
      this.inStockData=[];
      this.getTable();
    },
    exportAll() {
      this.getTable()
      this.postURLblob('core/biz/statistics/finance/inAndOutDataInfoExport',{
        supplierCode:this.input_supplierCode,
        skuCode:this.input_skuCode,
        queryDateMin:this.input_month,
        queryDateMax:this.c,
      }).then((res) => {
        // var blob = new Blob([res], { type: 'blob' })
        var link = document.createElement('a');
        link.href = window.URL.createObjectURL(res);
        link.download = 'stockAgeInquire.xlsx';
        link.click()
      }).catch((data) => {
        console.log(data);
      })
    },
    inputParam() {

      this.getTable();
    },
    changeMonth() {
      let date = new Date()
      this.input_month = (date.getFullYear())+'-'+ (date.getMonth()+1)+"-1"+" 00:00:00"
      console.log(this.input_month);

    },
    changeBlankToNull() {
      this.input_date = [];
      this.input_skuCode = null;
      this.input_supplierCode = null;
      this.input_supplierName = null;
      this.productCode = [];
      this.changeMonth()
      // this.getTable();
    },
    inputSupplierNameAndCode() {
      this.input_skuCode = null;
      this.input_supplierCode = null;
      // this.$forceUpdate();
      this.supplierNames.forEach((item) => {
        console.log(item)
        if (item.value == this.input_supplierName) {
          this.input_supplierCode = item.id;
          this.input_supplierName = this.input_supplierName.replace(
              /^[A-Za-z0-9]*/g,
              ""
          );
        }
      });
      this.byOwner()
    },
    byOwner(){
      const params = {};
      const promes = {
        ownerCode: this.input_supplierCode,

      };
      this.postURL(
          "core/sys/product/getProductCodeSourceByOwnerCode",
          params,
          promes
      ).then((res) => {
        // console.log(res)
        this.productCode = res.data;
      });
    },
    current() {
      let d = new Date(),
          str = '';
      str += d.getFullYear() + '-'; //获取当前年份
      str += d.getMonth() + 1 + '-'; //获取当前月份（0——11）
      str += (d.getDate()-1)+" 00:00:00";
      return str;
    },
  },
  mounted() {
    console.log(222);
    console.log(sessionStorage.getItem('supplierCode'));
    // let c = new Date(a[0], a[1],b);
    this.getSupplierName()
    this.getCoustom()
    this.changeMonth()
    this.byOwner()
    this.ve()
    this.dateTheGoodL=[this.current(),this.current()]
    this.badInstockDate=[this.input_month,this.c]
    this.badReturnDate=[this.input_month,this.c]
    console.log(this.badInstockDate);
    this.inputParam_a()
    console.log(this.dateTheGoodL);
  }

}
</script>

<style scoped>
 /deep/ table .el-button {
   padding: 0!important;
 }
</style>