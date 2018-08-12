<template>
  <section>
    <el-row style="padding: 10px 0;margin:  10px 0">
      <el-col :span="5">
        <!--<p>样品名称</p>-->
        <el-select v-model="specimen_value" size="mini" placeholder="请选择样品名称" @change="specimen_change">
          <el-option
            v-for="item in specimen"
            :key="item.v"
            :label="item.l"
            :value="item.v">
          </el-option>
        </el-select>
      </el-col>
      <el-col :span="7">
        <el-row>
          <!--<p>型号规格</p>-->
          <el-col :span="18">
            <el-input size="mini" v-model="size_type" placeholder="输入规格,数值，例如100，110，150"></el-input>
          </el-col>
          <el-col :span="6">
            <el-button size="mini" @click="jhl_C" style="width: 100%">
              计算净含量
            </el-button>
          </el-col>
        </el-row>

      </el-col>
      <el-col :span="6">
        <!--<p>选择日期</p>-->
        <el-date-picker
          size="mini"
          value-format="yyyy / MM / dd"
          v-model="date_val"
          align="right"
          type="date"
          placeholder="选择日期">
        </el-date-picker>
      </el-col>
      <el-col :span="6">
        <el-button type="primary" size="mini" @click="sjsf">水分随机生成</el-button>
        <el-button type="primary" size="mini" @click="sjhf">灰分随机生成</el-button>
      </el-col>
      <el-col :span="24">
        <el-button type="primary" size="mini" @click="sjbds">斑点个数随机生成</el-button>
        <el-button type="primary" size="mini" @click="sjxd">细度随机生成</el-button>
        <el-button type="primary" size="mini" @click="sjbd">白度随机生成</el-button>
      </el-col>
    </el-row>
    <div class="row" id="pdfDom"
         style="background-color:#fff;
         width: 800px;
         margin: 0 auto;
         color: #000;
         height: 1120px;
         padding: 10px;
         box-sizing: border-box">
      <el-row>
        <el-col>
          <p style="padding: 10px;font-size: 20px;font-weight: bold">平湖市林埭镇广欣食品厂检验原始记录</p>
          <p style="text-align: right;padding-right: 10px;padding-bottom: 5px">检（ ）第（ ）号</p>
        </el-col>
        <el-col>
          <table class="MsoNormalTable" cellspacing="0"
                 style="border-right: 1px solid #000;border-bottom: 1px solid #000">
            <tbody>

            <tr height="50">
              <td width="68" valign="center">
                <p class="MsoNormal" align="center">
                  <span>样品名称</span>
                </p>
              </td>
              <td width="108" valign="center" colspan="3">
                <p class="MsoHeader" align="justify" style="display: flex;align-items: center;justify-content: center">
                  <span v-html="specimen_value" class="font_class"></span>
                </p>
              </td>
              <td width="103" valign="center" colspan="5">
                <p class="MsoNormal" align="center"><span>型号规格</span></p>
              </td>
              <td width="75" valign="center" colspan="5">
                <p class="MsoNormal" align="center">
                  <span v-html="size_type+'克/包'" v-if="size_type" class="font_class"></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="6">
                <p class="MsoNormal" align="center"><span>等级</span>
                </p>
              </td>
              <td width="40" valign="center">
                <p class="MsoNormal" align="center"><span v-html="level_name" class="font_class"></span>
                </p>
              </td>
              <td width="101" valign="center" colspan="2">
                <p class="MsoNormal" align="center"><span>检验依据</span></p>
              </td>
              <td width="85" valign="center" colspan="2">
                <p class="MsoNormal">
                  <span v-html="jyyj" class="font_class"></span>
                </p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center">
                <p class="MsoNormal" align="center"><span>生产日期</span><span></span>
                </p>
              </td>
              <td width="108" valign="center" colspan="3">
                <p class="MsoHeader">
                  <span v-html="date_val" class="font_class"></span>
                </p>
              </td>
              <td width="103" valign="center" colspan="5">
                <p class="MsoHeader"><span>抽样数量</span><span></span>
                </p>
              </td>
              <td width="217" valign="center" colspan="11">
                <p class="MsoNormal font_class" align="center"><span>3包</span><span></span>
                </p>
              </td>
              <td width="82" valign="center" colspan="2">
                <p class="MsoNormal" align="center"><span>检验日期</span><span></span>
                </p>
              </td>
              <td width="143" valign="center" colspan="3">
                <p class="MsoNormal" align="center">
                  <span v-html="date_val" class="font_class"></span>
                </p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center">
                <p class="MsoNormal" align="center"><span>检验项目</span><span></span>
                </p>
              </td>
              <td width="51" valign="center">
                <p class="MsoNormal" align="center"><span>技术指标</span><span></span>
                </p>
              </td>
              <td width="378" valign="center" colspan="18">
                <p class="MsoNormal" align="center"><span>检 验 数 据 记 录 </span><span></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span>计算公式</span><span>及结果</span><span></span></p>
              </td>
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>检验结果</span><span></span></p>
              </td>
              <td width="37" valign="center">
                <p class="MsoNormal" align="center"><span>判定</span><span></span>
                </p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center">
                <p class="MsoNormal" align="center"><span>感官，<font face="Times New Roman">g</font></span><span></span>
                </p>
              </td>
              <td width="51" valign="center">
                <p class="MsoNormal" align="center"><span>符合标准要求</span><span></span></p>
              </td>
              <td width="378" valign="center" colspan="18">
                <p class="MsoNormal" align="center"><span>微带浅黄色阴影，具有光泽，具有玉米淀粉固有的特殊气味，无异味</span><span></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span>/</span><span></span>
                </p>
              </td>
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>符合</span><span></span></p>
              </td>
              <td width="37" valign="center">
                <p class="MsoNormal" align="center"><span>合格</span><span></span></p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center" rowspan="2">
                <p class="MsoNormal" align="center"><span>净含量，<font face="Times New Roman">g</font></span><span></span>
                </p>
              </td>
              <td width="51" valign="center" rowspan="2">
                <p class="MsoNormal"><span v-if="size_type" v-html="'≥'+size_type" class="font_class"></span></p>
              </td>
              <td width="160" valign="center" colspan="7">
                <p class="MsoNormal" align="center"><span>总重量，</span><span>m</span><sub><span>1</span></sub><span>，<font
                  face="微软雅黑">g</font></span><span></span>
                </p>
              </td>
              <td width="104" valign="center" colspan="7">
                <p class="MsoNormal" align="center"><span>包装重，</span><span>m</span><sub><span>0</span></sub><span>，<font
                  face="微软雅黑">g</font></span><span></span>
                </p>
              </td>
              <td width="113" valign="center" colspan="4">
                <p class="MsoNormal" align="center"><span>3g</span><span></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3" rowspan="2">
                <p class="MsoNormal" align="center">
                  <span>m=m</span><sub><span>1</span></sub><span>-m</span><sub><span>0</span></sub><span></span>
                </p>
              </td>
              <td width="47" valign="center" rowspan="2">
                <p class="MsoNormal font_class" align="center"><span v-html="jhl_average"></span>
                </p>
              </td>
              <td width="37" valign="center" rowspan="2">
                <p class="MsoNormal" align="center"><span>合格</span><span></span></p>
              </td>
            </tr>
            <!--水分-->
            <tr height="50">
              <td width="75" valign="center" colspan="4">
                <p class="MsoNormal" align="center">
                  <span v-if="jhl[0]" v-html="jhl[0]+'克/包'" class="font_class"></span>
                </p>
              </td>
              <td width="40" valign="center" colspan="4">
                <p class="MsoNormal" align="center">
                  <span v-if="jhl[1]" v-html="jhl[1]+'克/包'" class="font_class"></span>
                </p>
              </td>
              <td width="75" valign="center" colspan="4">
                <p class="MsoNormal" align="center">
                  <span v-if="jhl[2]" v-html="jhl[2]+'克/包'" class="font_class"></span>
                </p>
              </td>
              <td width="90" valign="center" colspan="4">
                <p class="MsoNormal" align="center">
                  <span v-if="jhl[3]" v-html="jhl[3]+'克/包'" class="font_class"></span>
                </p>
              </td>
              <td width="75" valign="center" colspan="2">
                <p class="MsoNormal" align="center">
                  <span v-if="jhl[4]" v-html="jhl[4]+'克/包'" class="font_class"></span>
                </p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>水分，<font face="Times New Roman">%</font></span><span></span>
                </p>
              </td>
              <td width="51" valign="center" rowspan="3">
                <p class="MsoNormal font_class" v-if="specimen_value=='玉米'||specimen_value=='小麦'">
                  <span>≤</span><span>14.0</span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='马铃薯'"><span>≤</span><span>20.0</span></p>
              </td>
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>编号</span><span></span></p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal" align="center">
                  <span>皿重W</span><sub>1</sub><span>,</span><span>g</span>
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal" align="center">
                  <span>皿和试样重W<sub>2</sub>,g</span>
                </p>
              </td>
              <td width="80" valign="center" colspan="5">
                <p class="MsoNormal" align="center">
                  <span>烘后一次称重W<sub>3</sub>,g</span>
                </p>
              </td>
              <td width="80" valign="center" colspan="3">
                <p class="MsoNormal" align="center">
                  <span>烘后二次称重W<sub>4</sub>,g</span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center">
                  <img src="./formula1.png" style="width: 100%"/>
                </p>
              </td>
              <td width="47" valign="center" rowspan="3">
                <p class="MsoNormal font_class" align="center"><span>{{sfarr1}}</span><span></span>
                </p>
              </td>
              <td width="37" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>合格</span><span></span>
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>1</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[0].w1}}
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[0].w2}}
                </p>
              </td>
              <td width="80" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[0].w3}}
                </p>
              </td>
              <td width="80" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[0].w4}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[0].h}}
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>2</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[1].w1}}
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[1].w2}}
                </p>
              </td>
              <td width="80" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[1].w3}}
                </p>
              </td>
              <td width="80" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[1].w4}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{sfarr[1].h}}
                </p>
              </td>
            </tr>
            <tr>
              <td width="68" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>灰分</span><span>（干基），</span><span>%</span><span></span>
                </p>
              </td>
              <td width="51" valign="center" rowspan="3">
                <p class="MsoNormal font_class" v-if="specimen_value=='玉米'"><span>≤</span><span>0.15</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-else><span>≤</span><span>0.40</span><span></span></p>
              </td>
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>编号</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal" align="center"><span>空坩埚质量<font
                  face="Times New Roman">m</font></span><sub><span>0</span></sub><span>，</span><span>g</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal" align="center"><span>试样和坩埚质量<font face="Times New Roman">m</font></span><sub><span>1</span></sub><span>，</span><span>g</span><span></span>
                </p>
              </td>
              <td width="160" valign="center" colspan="8">
                <p class="MsoNormal" align="center"><span>灼烧后坩埚和试样灰分质量<font
                  face="Times New Roman">m</font></span><sub><span>2</span></sub><span>，</span><span>g</span><span></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span><img width="106" height="38"
                                                               src="../../imgfile/1007.png"></span>

                </p>
              </td>
              <td width="47" valign="center" rowspan="3">
                <p class="MsoNormal font_class" align="center"><span>{{hfarr1}}</span><span></span>
                </p>
              </td>
              <td width="37" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>合格</span><span></span>
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>1</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[0].m0}}
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[0].m1}}
                </p>
              </td>
              <td width="160" valign="center" colspan="8">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[0].m2}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[0].x}}
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>2</span><span></span>
                </p>
              </td>
              <td width="85" valign="center" colspan="4">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[1].m0}}
                </p>
              </td>
              <td width="85" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[1].m1}}
                </p>
              </td>
              <td width="160" valign="center" colspan="8">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[1].m2}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{hfarr[1].x}}
                </p>
              </td>
            </tr>

            <tr height="50">
              <td width="68" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>斑点，个<font
                  face="Times New Roman">/cm</font></span><sup><span>2</span></sup><span></span></p>
                <p class="MsoNormal" align="center"><span>&nbsp;</span>
                </p>
              </td>
              <td width="51" valign="center" rowspan="3">
                <p class="MsoNormal font_class" v-if="specimen_value=='玉米'"><span>≤</span><span>0.7</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='小麦'"><span>≤</span><span>3.0</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='马铃薯'"><span>≤</span><span>6.0</span><span></span>
                </p>
              </td>
              <td width="47" valign="center">
                <p class="MsoHeader"><span>编号</span><span></span></p>
              </td>
              <td width="330" valign="center" colspan="17">
                <p class="MsoNormal" align="center"><span>10<font face="宋体">个空格内样品斑点的总数</font><font
                  face="Times New Roman">C</font><font face="宋体">（个）</font></span><span></span></p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span>X=C/10</span><span></span></p>
              </td>
              <td width="47" valign="center" rowspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{bdarr1}}
                </p>
              </td>
              <td width="37" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>合格</span><span></span>
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>1</span><span></span>
                </p>
              </td>
              <td width="330" valign="center" colspan="17">
                <p class="MsoNormal font_class" align="center">
                  {{bdarr[0].c}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{bdarr[0].x}}
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>2</span><span></span>
                </p>
              </td>
              <td width="330" valign="center" colspan="17">
                <p class="MsoNormal font_class" align="center">
                  {{bdarr[1].c}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{bdarr[1].x}}
                </p>
              </td>
            </tr>

            <tr>
              <td width="68" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>细度，<font face="Times New Roman">%</font></span><span></span>
                </p>
                <p class="MsoNormal" align="center"><span>&nbsp;</span>
                </p>
              </td>
              <td width="51" valign="center" rowspan="3">
                <p class="MsoNormal font_class" v-if="specimen_value=='玉米'"><span>≥</span><span>99.0</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='小麦'"><span>≥</span><span>98.0</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='马铃薯'">
                  <span>≥</span><span>99.5</span><span></span></p>
              </td>
              <td width="47" valign="center">
                <p class="MsoHeader"><span>编号</span><span></span></p>
              </td>
              <td width="157" valign="center" colspan="8">
                <p class="MsoNormal" align="center">
                  <span>试样质量</span><span>m</span><sub><span>0</span></sub><span></span><span>，</span><span>g</span><span></span>
                </p>
              </td>
              <td width="173" valign="center" colspan="9">
                <p class="MsoAcetate" align="center"><span>试样过</span><span>筛的筛下物质量<font face="Times New Roman">m</font></span><sub><span>1</span></sub><span>，</span><span>g</span><span></span>
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoAcetate" align="center"><span>
                  <img width="84" height="39" src="../../imgfile/1343.png"></span>

                </p>
              </td>
              <td width="47" valign="center" rowspan="3">
                <p class="MsoNormal font_class" align="center">
                  {{xdarr1}}
                </p>
              </td>
              <td width="37" valign="center" rowspan="3">
                <p class="MsoNormal" align="center"><span>合格</span><span></span>
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>1</span><span></span></p>
              </td>
              <td width="157" valign="center" colspan="8">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[0].m0}}
                </p>
              </td>
              <td width="173" valign="center" colspan="9">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[0].m1}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[0].x}}
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="47" valign="center">
                <p class="MsoNormal" align="center"><span>2</span><span></span></p>
              </td>
              <td width="157" valign="center" colspan="8">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[1].m0}}
                </p>
              </td>
              <td width="173" valign="center" colspan="9">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[1].m1}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoAcetate font_class" align="center">
                  {{xdarr[0].x}}
                </p>
              </td>
            </tr>
            <tr height="50">
              <td width="68" valign="center">
                <p class="MsoNormal" align="center"><span>白度，<font face="Times New Roman">%</font></span><span></span>
                </p>
              </td>
              <td width="51" valign="center">
                <p class="MsoNormal font_class" v-if="specimen_value=='玉米'"><span>≥</span><span>87.0</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='小麦'"><span>≥</span><span>91.0</span><span></span>
                </p>
                <p class="MsoNormal font_class" v-if="specimen_value=='马铃薯'"><span>≥</span><span>90.0</span><span></span></p>
              </td>
              <td width="126" valign="center" colspan="5">
                <p class="MsoNormal" align="center"><span>白度仪读数</span><span></span>
                </p>
              </td>
              <td width="63" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span>编号<font face="Times New Roman">1</font></span><span></span>
                </p>
              </td>
              <td width="63" valign="center" colspan="5">
                <p class="MsoNormal font_class" align="center">
                  {{bdsarr[0].x}}
                </p>
              </td>
              <td width="63" valign="center" colspan="4">
                <p class="MsoNormal" align="center"><span>编号<font face="Times New Roman">2</font></span><span></span>
                </p>
              </td>
              <td width="63" valign="center">
                <p class="MsoNormal font_class" align="center">
                  {{bdsarr[1].x}}
                </p>
              </td>
              <td width="141" valign="center" colspan="3">
                <p class="MsoNormal" align="center"><span>/</span><span></span></p>
              </td>
              <td width="47" valign="center">
                <p class="MsoNormal font_class" align="center">
                  {{bdsarr1}}
                </p>
              </td>
              <td width="37" valign="center">
                <p class="MsoNormal" align="center"><span>合格</span><span></span>
                </p>
              </td>
            </tr>
            </tbody>
          </table>
        </el-col>
      </el-row>
    </div>
    <button type="button" class="btn btn-primary" @click="getPdf()">导出PDF</button>
    <!--<div id="test"></div>-->
  </section>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        specimen: [
          {
            l: '玉米',
            v: '玉米'
          }, {
            l: '小麦',
            v: '小麦'
          }, {
            l: '马铃薯',
            v: '马铃薯'
          }
        ],
        sfarr: [
          {
            w1: '',
            w2: '',
            w3: '',
            w4: '',
            h: ''
          }, {
            w1: '',
            w2: '',
            w3: '',
            w4: '',
            h: ''
          }],
        hfarr: [
          {
            m0: '',
            m1: '',
            m2: '',
            x: ''
          }, {
            m0: '',
            m1: '',
            m2: '',
            x: ''
          }],
        bdarr: [{
          c: '',
          x: '',
        }, {
          c: '',
          x: '',
        }],
        xdarr: [
          {
            m0: '',
            m1: '',
            x: ''
          }, {
            m0: '',
            m1: '',
            x: ''
          }
        ],
        bdsarr:[
          {
          x:''
        },{
          x:''
        }],
        bdsarr1:'',
        xdarr1: '',
        bdarr1: '',
        sfarr1: '',
        hfarr1: '',
        specimen_value: '',// 选择的类型
        size_type: '',//型号规格
        level_name: '',// 等级名称
        jyyj: '',//检验依据
        date_val: '',// 选择的日期
        jhl: [],//净含量数组
        jhl_average: '',//净含量平均数
        htmlTitle: '页面导出PDF文件名'
      }
    },
    methods: {
      // 类型切换
      specimen_change() {
        if (this.specimen_value == '小麦') {
          this.level_name = '二级'
        } else {
          this.level_name = '一级'
        }
        if (this.specimen_value == '玉米') {
          this.jyyj = 'GB/T 8885'
        } else {
          this.jyyj = 'GB 31637'
        }
      },
      math_rander(min, max, time_nub, length) {
        // console.log('aaa', min, max, time_nub, length)
        if (min > max) {
          let a = min
          min = max
          max = a
        }
        let arr = []
        if (!time_nub) {
          let NUB = Math.random()
          if (length) {
            NUB = Number(NUB.toString().substring(0, (NUB.toString().indexOf('.') + length)))
          }
          return NUB
        } else {
          if (time_nub > 0) {
            for (let i = 0; i < time_nub; i++) {

              var Range = max - min;
              var Rand = Math.random();
              let NUB = Rand * Range
              var num = min + Number(NUB.toString().substring(0, (NUB.toString().indexOf('.') + length)))
              arr.push(num)
            }
          }
          return arr
        }
      },
      jhl_C() {
        this.other_data()
        if (!this.size_type) {
          this.$message({
            type: 'info',
            message: '请先填写规格型号'
          })
          return
        }
        let ST = Number(this.size_type)
        let sum = 0
        let randem_arr = this.math_rander(3, 6, 5, 2)
        if (randem_arr.length > 0) {
          for (let i = 0; i < randem_arr.length; i++) {
            randem_arr[i] = Number(randem_arr[i]) + ST
          }
          for (let j = 0; j < randem_arr.length; j++) {
            if (Number(randem_arr[j]).toString() != 'NaN') {
              sum += Number(randem_arr[j])
            }
          }
          this.jhl_average = (sum / randem_arr.length).toFixed(1)
        }
        this.jhl = randem_arr
      },
      other_data() {
        let w1 = this.math_rander(21, 25, 1, 5)[0]
        let w2 = this.math_rander(4, 6, 1, 5)[0]
        let w3 = (this.math_rander(1, 2, 1, 5) / 1000).toFixed(5)
        let H;
        if (this.specimen_value == '马铃薯') {
          H = this.math_rander(16.5, 19, 1, 2)[0]
        } else {
          H = this.math_rander(12.5, 14, 1, 2)[0]
        }
        let w4 = w2 - ((H / 100) * (w2 - w1))
        // console.log(
        //   'w1=', w1,
        //   'w2=', w2,
        //   'w3=', w3,
        //   'H=', H,
        //   '计算w4=', w4
        // )
      },
      // 随机数
      meth_rander(min, max, l) {
        let cha = max - min
        let rander = Math.random()
        let qujian = (cha * rander).toFixed(l)
        return Number(min) + Number(qujian)
      },
      //随机水分生成
      sjsf() {
        let arr = []
        for (let i = 0; i < 2; i++) {
          let hh, w4, w3, w1, w2
          w1 = Number(this.meth_rander(21, 25, 4))
          w2 = Number(w1) + Number(this.meth_rander(4, 6, 4))
          if (this.specimen_value == '马铃薯') {
            hh = Number(this.meth_rander(16.5, 19, 1))
          } else {
            hh = Number(this.meth_rander(12.5, 14, 1))
          }
          w4 = Number((w2 - (hh / 100 * (w2 - w1))).toFixed(4))
          // w4=w4
          if (this.meth_rander(0, 10, 1) > 5) {
            w3 = Number(Number(w4) + Number(0.002))
          } else {
            w3 = Number(Number(w4) + Number(0.001))
          }
          w1 = w1.toFixed(4)
          w2 = w2.toFixed(4)
          w3 = w3.toFixed(4)
          w4 = w4.toFixed(4)
          hh = hh.toFixed(1)
          arr.push({w1: w1, w2: w2, w3: w3, w4: w4, h: hh})
        }

        this.sfarr = arr
        //平均数
        this.sfarr1 = ((Number(arr[0].h) + Number(arr[1].h)) / 2).toFixed(1)
      },

      //随机灰分生成
      sjhf() {
        let arr = []
        for (let i = 0; i < 2; i++) {
          let x, m3, m2, m1, m0
          m0 = Number(this.meth_rander(45, 47, 4))
          m1 = Number(m0) + Number(this.meth_rander(7, 9, 4))
          console.log(',,,', m0, m1, this.meth_rander(7, 9, 4))
          if (this.specimen_value == '玉米') {
            x = Number(this.meth_rander(11, 14, 2)) / 100
          } else {
            x = Number(this.meth_rander(22, 38, 2)) / 100
          }
          console.log('ssss', x, m1, m0)
          m2 = Number((x / 100 * (m1 - m0) + m0).toFixed(4))

          m0 = m0.toFixed(4)
          m1 = m1.toFixed(4)
          m2 = m2.toFixed(4)
          x = x.toFixed(2)
          arr.push({m0: m0, m1: m1, m2: m2, x: x})
        }

        this.hfarr = arr
        //平均数
        // this.hfarr1 = ((
        //   Number(arr[0].m0) +
        //   Number(arr[0].m1) +
        //   Number(arr[0].m2) +
        //   Number(arr[1].m0) +
        //   Number(arr[1].m1) +
        //   Number(arr[1].m2)) / 6).toFixed(4)
        this.hfarr1 = ((Number(arr[0].x) + Number(arr[1].x)) / 2).toFixed(2)
      },

      //随机斑点数
      sjbds() {
        let arr = []
        for (let i = 0; i < 2; i++) {
          let c, x
          if (this.specimen_value == '玉米')
            c = Number(this.meth_rander(5, 7, 0))
          if (this.specimen_value == '小麦')
            c = Number(this.meth_rander(22, 28, 0))
          if (this.specimen_value == '马铃薯')
            c = Number(this.meth_rander(48, 58, 0))
          x = c / 10
          arr.push({c: c, x: x})
        }

        this.bdarr = arr
        this.bdarr1 = ((Number(arr[0].x) + Number(arr[1].x)) / 2).toFixed(2)
      },

      //随机细度生成
      sjxd() {
        let arr = []
        for (let i = 0; i < 2; i++) {
          let x, m0, m1
          m0 = Number(this.meth_rander(48, 53, 1))
          if (this.specimen_value == '玉米')
            x = Number(this.meth_rander(99.0, 99.8, 1))
          if (this.specimen_value == '小麦')
            x = Number(this.meth_rander(98.0, 99.1, 1))
          if (this.specimen_value == '马铃薯')
            x = Number(this.meth_rander(99.5, 99.9, 1))
          m1 = Number(x.toFixed(1)) / 100 * m0
          x = x.toFixed(1)
          m1 = m1.toFixed(1)
          arr.push({m0: m0, m1: m1, x: x})
        }

        this.xdarr = arr
        this.xdarr1 = ((Number(arr[0].x) + Number(arr[1].x)) / 2).toFixed(1)
      },

      //随机白度生成
      sjbd() {
        let arr = []
        for (let i = 0; i < 2; i++) {
          let x
          if (this.specimen_value == '玉米')
            x = Number(this.meth_rander(87, 89, 1))
          if (this.specimen_value == '小麦')
            x = Number(this.meth_rander(91, 92.5, 1))
          if (this.specimen_value == '马铃薯')
            x = Number(this.meth_rander(90, 91.5, 1))
          x = x.toFixed(1)
          arr.push({ x: x})
        }

        this.bdsarr = arr
        this.bdsarr1 = ((Number(arr[0].x) + Number(arr[1].x)) / 2).toFixed(2)
      },
    },
    mounted() {
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>


  .font_class {
    font-family: 'hand_font';
    font-size: 20px;
  }

  p, span, tr, td {
    padding: 0;
    margin: 0;
  }

  td {
    border-top: 1px solid #000;
    border-left: 1px solid #000;
  }

  #pdfDom {
    font-size: 12px;
  }
</style>
