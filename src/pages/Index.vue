<template>
  <q-page class="flex flex-center" >
    <div class="q-pa-md" >
      <div class="q-gutter-md" style="min-width: 500px;max-width: 500px" >
        <q-dialog v-model="alert">
          <q-card>
            <q-card-section>
              <div class="text-h6">提醒</div>
            </q-card-section>

            <q-card-section class="q-pt-none">
              请至少填写一项
            </q-card-section>

            <q-card-actions align="right">
              <q-btn flat label="OK" color="primary" v-close-popup />
            </q-card-actions>
          </q-card>
        </q-dialog>
        <q-btn color="primary" label="末尾" @click="goToPanel('q49')" />
        <q-btn color="primary" label="Go" @click="goToPanel(tttt)" />
        <q-input outlined v-model="tttt" />

        <q-carousel
          ref="carousel"
          v-model="slide"
          transition-prev="scale"
          transition-next="scale"
          swipeable
          animated
          control-color="blue"
          padding
          height="600px"
          class="bg-grey-12 text-black shadow-1 rounded-borders"
        >
          <q-carousel-slide name="q1" class="flex-center">
            <div class="q-mt-md text-center"  >
              <div><label class="sv-title">Q1. 请问您来自哪个国家或地区？</label></div>
              <q-input outlined v-model="q1_answer"  />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q2" class="no-wrap flex-center">
            <div class="q-mt-md" >
              <div style="margin: 0 auto;">
                <label class="sv-title">Q2. 请问您2019年是否到过中国旅游？ </label>
              </div>
              <div style="max-width:200px;" >
                <q-item  tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGo" v-model="q2_answer" val=1 color="teal" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>1. 是</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGoSpecific('q36')" v-model="q2_answer" val=2 color="teal" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>2. 否</q-item-label>
                  </q-item-section>
                </q-item>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q3" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q3. 请问您这次是参加旅行团还是自己旅游？ </label>
              <div style="max-width:300px;" >
                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGo" v-model="q3_answer" val=1 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>1. 参加旅行社的出游团</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGo" v-model="q3_answer" val=2 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>2. 自己组织</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGo" v-model="q3_answer" val=3 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>3. 公务</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio v-model="q3_answer" val=4 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>4. 其他</q-item-label>
                  </q-item-section>
                </q-item>
              </div>
              <div style="margin: 0 auto; max-width: 220px;">
                <q-input outlined v-model="q3_answer_qita" v-if="q3_answer=='4'" />
              </div>
              <div class="sub_but">
                <q-btn color="primary" label="下一题" v-if="q3_answer=='4'" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q4" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <div>
                <label class="sv-title">Q4. 您是第一次到中国来旅游吗？ </label>
              </div>
              <div style="max-width:400px;" >
                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGoSpecific('q6')" v-model="q4_answer" val=1 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>1. 是</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio @input="checkAndGo()" v-model="q4_answer" val=2 />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>2. 否</q-item-label>
                  </q-item-section>
                </q-item>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q5" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <div>
                <label class="sv-title">Q5.是第几次呢？ </label>
              </div>
              <div>
                <q-input outlined v-model="q5_answer" />
              </div>
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q6" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <div>
                <label class="sv-title">Q6.请问您来华旅游的主要目的是？ </label>
              </div>
              <div class="sv-container">
              <q-option-group
                :options="q6_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelExcept(q6_answer, '10')"
                v-model="q6_answer"
              />
              <q-input outlined v-model="q6_answer_qita" v-if="q6_answer=='10'" />
              <div class="sub_but">
                <q-btn color="primary" v-if="q6_answer=='10'" label="下一题" @click="goToNextPanel()" />
              </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q7" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q7.请问您来中国主要接触了哪些景点、活动或风土人情？ 【选择最主要的1-3个】？ </label>
            </div>
            <div>
              <q-option-group dense
                :options="q7_options"
                label="Notifications"
                type="checkbox"
                v-model="q7_answer"
              />
              <q-input :dense="true" outlined v-model="q7_answer_qita" v-if="q7_answer.includes('12')" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q8" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q8.您这次旅游是和谁一起出来玩的？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q8_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelExcept(q8_answer, '7')"
                v-model="q8_answer"
              />
              <q-input outlined v-model="q8_answer_qita" v-if="q8_answer=='7'" />
              <div class="sub_but">
                <q-btn color="primary" v-if="q8_answer=='7'" label="下一题" @click="goToNextPanel()" />
              </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q9" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q9.您这次出游前主要通过哪些渠道了解有关信息？【最多选三项】 </label>
              <q-option-group dense
                :options="q9_options"
                label="Notifications"
                type="checkbox"
                v-model="q9_answer"
              />
              <q-input :dense="true" outlined v-model="q9_answer_qita" v-if="q9_answer.includes('12')" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q10" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q10.您这次出游前主要查找了哪些方面的信息？【最多选三项】 </label>
              <q-option-group dense
                :options="q10_options"
                label="Notifications"
                type="checkbox"
                v-model="q10_answer"
              />
              <q-input :dense="true" outlined v-model="q10_answer_qita" v-if="q10_answer.includes('8')" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q11" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q11.您这次出游前在电视上看到过中国的旅游形象广告或专题片吗？ </label>
              <div>
              <q-option-group
                :options="q11_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelOnCondition(q11_answer==='2', 'q13')"
                v-model="q11_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q12" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q12.是哪个城市（景区）呢？ </label>
              <q-input outlined v-model="q12_answer_qita" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q13" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q13.您选择一地作为目的地出行，下列因素哪些对您影响较大？【最多选三项】 </label>
              <q-option-group dense
                :options="q13_options"
                label="Notifications"
                type="checkbox"
                v-model="q13_answer"
              />
              <q-input :dense="true" outlined v-model="q13_answer_qita" v-if="q13_answer.includes('15')" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q14" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q14.您这次旅游时人均花费是多少钱？ </label>
              <div>
              <q-option-group
                :options="q14_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q14_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q15" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q15.您这次旅游花费最多的项目是？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q15_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelExcept(q15_answer, '7')"
                v-model="q15_answer"
              />
              <q-input outlined v-model="q15_answer_qita" v-if="q15_answer=='7'" />
              <div class="sub_but">
                <q-btn color="primary" v-if="q15_answer=='7'" label="下一题" @click="goToNextPanel()" />
              </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q16" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q16.您这次旅游时参观了几个景点？ </label>
              <div>
              <q-option-group
                :options="q16_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q16_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q17" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q17. 您这次旅游途经了哪些国家（地区）？ </label>
              <q-input outlined v-model="q17_answer_1" label="1st" />
              <q-input filled v-model="q17_answer_2" label="2nd" />
              <q-input outlined v-model="q17_answer_3" label="3rd" />
              <q-input filled v-model="q17_answer_4" label="4th" />
              <q-input outlined v-model="q17_answer_5" label="5th" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="validateNoneNullAndGoToNextPanel(q17_answer_1+q17_answer_2+q17_answer_3+q17_answer_4+q17_answer_5)" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q18" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q18. 您这次在华旅游线路包含了哪些城市（景区）？ </label>
              <q-input dense outlined v-model="q18_answer_1" label="1st" />
              <q-input dense filled v-model="q18_answer_2" label="2nd" />
              <q-input dense outlined v-model="q18_answer_3" label="3rd" />
              <q-input dense filled v-model="q18_answer_4" label="4th" />
              <q-input dense outlined v-model="q18_answer_5" label="5th" />
              <q-input dense filled v-model="q18_answer_6" label="6th" />
              <q-input dense outlined v-model="q18_answer_7" label="7th" />
              <q-input dense filled v-model="q18_answer_8" label="8th" />
              <q-input dense outlined v-model="q18_answer_9" label="9th" />
              <q-input dense filled v-model="q18_answer_10" label="10th" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="validateNoneNullAndGoToNextPanel(q18_answer_1+q18_answer_2+q18_answer_3+q18_answer_4+q18_answer_5+q18_answer_6+q18_answer_7+q18_answer_8+q18_answer_9+q18_answer_10)" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q19" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q19.您这次旅游了多长时间？ </label>
              <div>
              <q-option-group
                :options="q19_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q19_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q20" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q20.您这次旅游时住在什么地方？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q20_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelExcept(q20_answer, '5')"
                v-model="q20_answer"
              />
              <q-input outlined v-model="q20_answer_qita" v-if="q20_answer=='5'" />
              <div class="sub_but">
                <q-btn color="primary" v-if="q20_answer=='5'" label="下一题" @click="goToNextPanel()" />
              </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q21" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q21.您这次旅游时购买了保险吗？ </label>
              <div>
              <q-option-group
                :options="q21_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelOnCondition(q21_answer==='1', 'q23')"
                v-model="q21_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q22" class=" no-wrap flex-center">
            <div class="q-mt-md ">
              <label class="sv-title">Q22.您购买了以下哪几种保险？ </label>
              <div>
                <q-option-group dense
                  :options="q22_options"
                  label="Notifications"
                  type="checkbox"
                  v-model="q22_answer"
                />
                <q-input :dense="true" outlined v-model="q22_answer_qita" v-if="q22_answer.includes('7')" />
                <div class="sub_but">
                  <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
                </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q23" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q23.在此次旅遊之前，您對以下城市的印象如何？（城市旅遊形象）？ </label>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  北京:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_beijing"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  上海:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_shanghai"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  重庆:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_chongqing"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  沈阳:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_shenyang"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  西安:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_xian"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  广州:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_guangzhou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  天津:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_tianjin"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  苏州:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_suzhou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  南京:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_nanjing"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  成都:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_chengdu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  杭州:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_hangzhou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  承德:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_chengde"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  昆明:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_kunming"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  桂林:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_guilin"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  深圳:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_shenzhen"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  珠海:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_zhuhai"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  西宁:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_xining"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div class="q-pa-md">
                <q-badge color="secondary">
                  兰州:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q23_answer_lanzhou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div style="height: 20px; margin-top: 55px;margin-bottom: 25px;"></div>

              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>

            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q24" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q24.来这里旅游前，您对目的地的整体形象评价如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  城市形象:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q24_answer_chengshixingxiang"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  城市服务水平:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q24_answer_chengshifuwushuip"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>

            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q25" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q25.在此次旅游之前，您对此次旅游的期望有多高？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  城市服务质量预期:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q25_answer_chengshifuwuzhiliangyuqi"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  旅游服务质量预期:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q25_answer_lvyoufuwuzhiliangyuqi"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q26" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q26.您对此次出游的定位如何评价？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  旅游价格是否合理:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q26_answer_lvyouzhiliangshifouheli"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  旅游质量是否与旅游价格相符:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q26_answer_jiagexiangfu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q27" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q27.您对当地的总体评价如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  现代化程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q27_answer_xiandaihua"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  美丽程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q27_answer_meili"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  知名度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q27_answer_zhimingdu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  开放度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q27_answer_kaifangdu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  信息化程度（智慧城市):（1~10分）
                </q-badge>
                <q-slider
                  v-model="q27_answer_xinxihua"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q28" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q28.您对城市管理的满意程度如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  我感觉很差~很不错:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q28_answer"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q29" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q29.您对公共行业服务的满意程度如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  我感觉很差~很不错:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q29_answer"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q30" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q30.您对当地窗口服务具体评价如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  交通:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_jiaotong"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  餐饮:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_canyin"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  住宿:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_zhusu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  购物:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_gouwu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  文化娱乐:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_wenhua"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  景区景点:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_jingdian"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  旅行社:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_lvxingshe"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  导游:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_daoyou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  产品和服务质量:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_chanpinfuwuzhiliang"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  发票具备及正规度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_fapiao"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  旅游公共服务:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_gonggongfuwu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  标准化程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_biaozhunhua"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  总体服务质量:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q30_answer_zongti"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>

              <div style="height: 20px; margin-top: 55px;margin-bottom: 25px;"></div>

              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q31" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q31.您对此次出游的总体评价如何？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  总体满意程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q31_answer_zongti"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  与需求相比满意程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q31_answer_xiangbi"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  与理想中相比的满意程度:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q31_answer_lixiang"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q32" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q32.您旅途过程中有抱怨或投诉吗？ </label>
              <div>
              <q-option-group
                :options="q32_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelOnCondition(q32_answer==='1', 'q34')"
                v-model="q32_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q33" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q33.投诉处理满意程度？ </label>
              <div>
              <q-option-group
                :options="q33_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q33_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q34" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q34.您对中国有再游一次的想法吗？ </label>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  未来自己重游:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q34_answer_zijichongyou"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  未来继续选择该旅行社的可能性:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q34_answer_jixu"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="q-pa-md">
                <q-badge color="secondary">
                  未来推荐亲友:（1~10分）
                </q-badge>
                <q-slider
                  v-model="q34_answer_tuijian"
                  :min="1"
                  :max="10"
                  :step="1"
                  markers
                  label
                  color="purple"
                />
              </div>
              <div class="sub_but">
                <q-btn color="primary"  label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q35" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q35. 您对目的地在旅游建设与旅游服务方面主要意见和建议是什么？ </label>
              <q-input outlined v-model="q35_answer_qita" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q36" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q36.您在2020 or 2021年有旅行计划吗？ </label>
              <div>
              <q-option-group
                :options="q36_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q36_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q37" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q37.准备去那些地方旅行呢？ </label>
              <div>
              <q-option-group
                :options="q37_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q37_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q38" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q38.如果您现在或将来准备前往中国，那您会为了什么来到中国呢？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q38_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanelExcept(q38_answer, '10')"
                v-model="q38_answer"
              />
              <q-input outlined v-model="q38_answer_qita" v-if="q38_answer=='10'" />
              <div class="sub_but">
                <q-btn color="primary" v-if="q38_answer=='10'" label="下一题" @click="goToNextPanel()" />
              </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q39" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q39.如果前往中国，您现在已经收集了至少一些中国的旅行情报吗？ </label>
              <div class="sv-container">
                <q-option-group
                  :options="q39_options"
                  label="Notifications"
                  type="radio"
                  @input="goToNextPanelExcept(q39_answer, '5')"
                  v-model="q39_answer"
                />
                <q-input outlined v-model="q39_answer_qita" v-if="q39_answer=='5'" />
                <div class="sub_but">
                  <q-btn color="primary" v-if="q39_answer=='5'" label="下一题" @click="goToNextPanel()" />
                </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q40" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q40. 如果前往中国，您会选择什么季节前往中国呢？ </label>
              <div>
              <q-option-group
                :options="q40_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q40_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q41" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q41. 您最近的一次出行是什么时候呢？任意目的地？ </label>
              <div>
              <q-option-group
                :options="q41_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q41_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q42" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q42. 最近的COVID-19疫情影响了您的出行度假计划吗？ </label>
              <div>
              <q-option-group
                :options="q42_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q42_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q43" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q43. 被访者性别？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q43_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q43_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q44" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label class="sv-title">Q44. 被访者姓名？ </label>
              <q-input outlined v-model="q44_answer_qita" />
              <div class="sub_but">
                <q-btn color="primary" label="下一题" @click="goToNextPanel()" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q45" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q45. 请问您所接受的最高教育程度是？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q45_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q45_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q46" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q46. 请问您的年龄是？ </label>
              <div class="sv-container">
              <q-option-group
                :options="q46_options"
                label="Notifications"
                type="radio"
                @input="goToNextPanel"
                v-model="q46_answer"
              />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q47" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q47. 请问您所在的行业是？ </label>
              <div class="sv-container">
                <q-option-group
                  :options="q47_options"
                  label="Notifications"
                  type="radio"
                  @input="goToNextPanelExcept(q47_answer, '24')"
                  v-model="q47_answer"
                />
                <q-input outlined v-model="q47_answer_qita" v-if="q47_answer=='24'" />
                <div class="sub_but">
                  <q-btn color="primary" v-if="q47_answer=='24'" label="下一题" @click="goToNextPanel()" />
                </div>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q48" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <label class="sv-title">Q48. 您个人愿意花多少钱在一次旅行上？ </label>
              <div>
                <q-option-group
                  :options="q48_options"
                  label="Notifications"
                  @input="goToNextPanel"
                  type="radio"
                  v-model="q48_answer"
                />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="email" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <div>
                <q-input outlined v-model="email" label="您的邮箱"  />
              </div>
              <div class="sub_but">
                <q-btn color="primary" label="下一页" @click="validateNoneNullAndGoToNextPanel(email)" />
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q49" class=" no-wrap flex-center">
            <div class="q-mt-md">
              <q-btn color="primary" label="提交答案" @click="submit()" />
              <q-btn color="secondary" label="回到首页" @click="goToPanel('q1')" />
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
  </q-page>
</template>

<script>
import axios from 'axios'
export default {
  name: 'PageIndex',
  data () {
    return {
      tttt: '',
      q2_answer_dict: {
        1: '1. 是',
        2: '2. 否'
      },
      q3_answer_dict: {
        1: '1. 参加旅行社的出游团',
        2: '2. 自己组织',
        3: '3. 公务'
      },
      q4_answer_dict: {
        1: '1. 是',
        2: '2. 否'
      },
      q11_answer_dict: {
        1: '1. 否',
        2: '2. 是'
      },
      q6_answer_dict: {
        1: '1.了解中国特色文化',
        2: '2.游览/观光',
        3: '3.休闲/度假',
        4: '4.探亲访友',
        5: '5.商务',
        6: '6.会议',
        7: '7.文体/教育/科技交流',
        8: '8.宗教/朝拜',
        9: '9.健康医疗'
      },
      q6_options: [
        { label: '1.了解中国特色文化', value: '1' },
        { label: '2.游览/观光', value: '2' },
        { label: '3.休闲/度假', value: '3' },
        { label: '4.探亲访友', value: '4' },
        { label: '5.商务', value: '5' },
        { label: '6.会议', value: '6' },
        { label: '7.文体/教育/科技交流', value: '7' },
        { label: '8.宗教/朝拜', value: '8' },
        { label: '9.健康医疗', value: '9' },
        { label: '10.其他（请注明）', value: '10' }
      ],
      slide: 'q1',
      q1_answer: '',
      q2_answer: '',
      q3_answer: '',
      q4_answer: '',
      q5_answer: '',
      q6_answer: '',
      q7_answer: [],
      q8_answer: '',
      q9_answer: [],
      q13_answer: [],
      q7_answer_qita: '',
      q9_answer_qita: '',
      q19_answer_qita: '',
      q22_answer_qita: '',
      q8_answer_qita: '',
      q10_answer: [],
      q3_answer_qita: '',
      q13_answer_qita: '',
      q12_answer_qita: '',
      q6_answer_qita: '',
      q39_answer_qita: '',
      q10_answer_qita: '',
      q47_answer_qita: '',
      q44_answer_qita: '',
      q35_answer_qita: '',
      q38_answer_qita: '',
      q15_answer_qita: '',
      q20_answer_qita: '',
      q48_answer: '',
      q7_answer_dict: {
        1: '1.山水风光',
        2: '2.文物古迹',
        3: '3.文化艺术',
        4: '4.美食烹调',
        5: '5.医疗保健',
        6: '6.购物消费',
        7: '7.气候生态',
        8: '8.建筑设施',
        9: '9.节庆会展',
        10: '10.学习培训',
        11: '11.乡村度假'
      },
      q7_options: [
        { label: '1.山水风光', value: '1' },
        { label: '2.文物古迹', value: '2' },
        { label: '3.文化艺术', value: '3' },
        { label: '4.美食烹调', value: '4' },
        { label: '5.医疗保健', value: '5' },
        { label: '6.购物消费', value: '6' },
        { label: '7.气候生态', value: '7' },
        { label: '8.建筑设施', value: '8' },
        { label: '9.节庆会展', value: '9' },
        { label: '10.学习培训', value: '10' },
        { label: '11.乡村度假', value: '11' },
        { label: '12.其他（请注明）', value: '12' }],
      q8_answer_dict: {
        1: '1.和家人一起出游',
        2: '2.公司、班级、社团等集体出游',
        3: '3.和好友结伴出游',
        4: '4.网络结伴旅游',
        5: '5.自助游组织出游',
        6: '6.商务活动/会议培训旅游'
      },
      q8_options: [
        { label: '1.和家人一起出游', value: '1' },
        { label: '2.公司、班级、社团等集体出游', value: '2' },
        { label: '3.和好友结伴出游', value: '3' },
        { label: '4.网络结伴旅游', value: '4' },
        { label: '5.自助游组织出游', value: '5' },
        { label: '6.商务活动/会议培训旅游', value: '6' },
        { label: '7.其他（请注明）', value: '7' }
      ],
      q9_answer_dict: {
        1: '1.社交媒体',
        2: '2.报纸/杂志/书籍',
        3: '3.亲朋好友介绍',
        4: '4.电视/广播',
        5: '5.户外广告',
        6: '6.电梯广告',
        7: '7.机场/地铁广告',
        8: '8.旅游宣传册',
        9: '9.旅游会展',
        10: '10.到旅行社咨询',
        11: '11.旅游地自己的推广活动'
      },
      q9_options: [
        { label: '1.社交媒体', value: '1' },
        { label: '2.报纸/杂志/书籍', value: '2' },
        { label: '3.亲朋好友介绍', value: '3' },
        { label: '4.电视/广播', value: '4' },
        { label: '5.户外广告', value: '5' },
        { label: '6.电梯广告', value: '6' },
        { label: '7.机场/地铁广告', value: '7' },
        { label: '8.旅游宣传册', value: '8' },
        { label: '9.旅游会展', value: '9' },
        { label: '10.到旅行社咨询', value: '10' },
        { label: '11.旅游地自己的推广活动', value: '11' },
        { label: '12.其他（请注明）', value: '12' }
      ],
      q13_answer_dict: {
        1: '1.旅行费用',
        2: '2.距离',
        3: '3.旅游地交通',
        4: '4.住宿条件',
        5: '5.旅行安全',
        6: '6.信息获取',
        7: '7.沟通交流',
        8: '8.景点吸引力/旅游地吸引力',
        9: '9.特色饮食',
        10: '10.休闲的环境',
        11: '11.城市形象',
        12: '12.节事活动',
        13: '13.民风民俗',
        14: '14.居民友善好客'
      },
      q13_options: [
        { label: '1.旅行费用', value: '1' },
        { label: '2.距离', value: '2' },
        { label: '3.旅游地交通', value: '3' },
        { label: '4.住宿条件', value: '4' },
        { label: '5.旅行安全', value: '5' },
        { label: '6.信息获取', value: '6' },
        { label: '7.沟通交流', value: '7' },
        { label: '8.景点吸引力/旅游地吸引力', value: '8' },
        { label: '9.特色饮食', value: '9' },
        { label: '10.休闲的环境', value: '10' },
        { label: '11.城市形象', value: '11' },
        { label: '12.节事活动', value: '12' },
        { label: '13.民风民俗', value: '13' },
        { label: '14.居民友善好客', value: '14' },
        { label: '15.其他（请注明）', value: '15' }
      ],
      q10_answer_dict: {
        1: '1.当地政策和法规',
        2: '2.旅游景区接待情况',
        3: '3.旅游产品和服务介绍',
        4: '4.旅游交通/天气等生活信息',
        5: '5.旅游购物环境情况',
        6: '6.特色文化娱乐活动',
        7: '7.旅游价格'
      },
      q10_options: [
        { label: '1.当地政策和法规', value: '1' },
        { label: '2.旅游景区接待情况', value: '2' },
        { label: '3.旅游产品和服务介绍', value: '3' },
        { label: '4.旅游交通/天气等生活信息', value: '4' },
        { label: '5.旅游购物环境情况', value: '5' },
        { label: '6.特色文化娱乐活动', value: '6' },
        { label: '7.旅游价格', value: '7' },
        { label: '8.其他（请注明）', value: '8' }
      ],

      q45_answer: '',
      q45_answer_dict: {
        1: '1.小学及以下',
        2: '2.初中',
        3: '3.高中/中专/技校',
        4: '4.大学专科',
        5: '5.大学本科',
        6: '6.硕士及以上'
      },
      q45_options: [
        { label: '1.小学及以下', value: '1' },
        { label: '2.初中', value: '2' },
        { label: '3.高中/中专/技校', value: '3' },
        { label: '4.大学专科', value: '4' },
        { label: '5.大学本科', value: '5' },
        { label: '6.硕士及以上', value: '6' }
      ],
      q18_answer_1: '',
      q18_answer_2: '',
      q18_answer_3: '',
      q18_answer_4: '',
      q18_answer_5: '',
      q31_answer_lixiang: 1,
      q31_answer_xiangbi: 1,
      q31_answer_zongti: 1,
      q18_answer_6: '',
      q18_answer_7: '',
      q18_answer_8: '',
      q18_answer_9: '',
      q18_answer_10: '',
      q46_answer: '',
      q46_answer_dict: {
        1: '1.15岁以下',
        2: '2.15-24岁',
        3: '3.25-34',
        4: '4.35-44',
        5: '5.45-59',
        6: '6.60岁及以上'
      },
      q46_options: [
        { label: '1.15岁以下', value: '1' },
        { label: '2.15-24岁', value: '2' },
        { label: '3.25-34', value: '3' },
        { label: '4.35-44', value: '4' },
        { label: '5.45-59', value: '5' },
        { label: '6.60岁及以上', value: '6' }
      ],
      q47_answer: '',
      q47_answer_dict: {
        1: '1.农林牧',
        2: '2.科学研究、技术服务和地质勘查业',
        3: '3.采矿业',
        4: '4.水利、环境和公共设施管理业',
        5: '5.制造业',
        6: '6.居民服务和其他服务业',
        7: '7.教育',
        8: '8.电力、燃气及水的生产和供应',
        9: '9.建筑业',
        10: '10.卫生、社会保障和社会福利业',
        11: '11.文化体育和娱乐业',
        12: '12.交通运输、仓储和邮政业',
        13: '13.国际组织',
        14: '14.信息传输、计算机服务和软件业',
        15: '15.公共管理与社会组织',
        16: '16.批发和零售业',
        17: '17.金融业',
        18: '18.住宿和餐饮业',
        19: '19.租赁和商务服务业',
        20: '20.下岗失业人员',
        21: '21.房地产业',
        22: '22.学生',
        23: '23.退休人员'
      },
      q47_options: [
        { label: '1.农林牧', value: '1' },
        { label: '2.科学研究、技术服务和地质勘查业', value: '2' },
        { label: '3.采矿业', value: '3' },
        { label: '4.水利、环境和公共设施管理业', value: '4' },
        { label: '5.制造业', value: '5' },
        { label: '6.居民服务和其他服务业', value: '6' },
        { label: '7.教育', value: '7' },
        { label: '8.电力、燃气及水的生产和供应', value: '8' },
        { label: '9.建筑业 ', value: '9' },
        { label: '10.卫生、社会保障和社会福利业', value: '10' },
        { label: '11.文化体育和娱乐业', value: '11' },
        { label: '12.交通运输、仓储和邮政业', value: '12' },
        { label: '13.国际组织', value: '13' },
        { label: '14.信息传输、计算机服务和软件业', value: '14' },
        { label: '15.公共管理与社会组织', value: '15' },
        { label: '16.批发和零售业', value: '16' },
        { label: '17.金融业', value: '17' },
        { label: '18.住宿和餐饮业', value: '18' },
        { label: '19.租赁和商务服务业', value: '19' },
        { label: '20.下岗失业人员', value: '20' },
        { label: '21.房地产业', value: '21' },
        { label: '22.学生', value: '22' },
        { label: '23.退休人员', value: '23' },
        { label: '24.其它（请注明）', value: '24' }
      ],
      q48_answer_dict: {
        1: '1.1000美元以下',
        2: '2.1001-3000美元',
        3: '3.3001-5000美元',
        4: '4.5001-8000美元',
        5: '5.8001-10000美元',
        6: '6.10001-20000美元',
        7: '7.20000美元以上'
      },
      q48_options: [
        { label: '1.1000美元以下 ', value: '1' },
        { label: '2.1001-3000美元', value: '2' },
        { label: '3.3001-5000美元', value: '3' },
        { label: '4.5001-8000美元', value: '4' },
        { label: '5.8001-10000美元', value: '5' },
        { label: '6.10001-20000美元', value: '6' },
        { label: '7.20000美元以上', value: '7' }
      ],
      q21_answer: '',
      q21_answer_dict: {
        1: '1.购买了保险',
        2: '2.没有购买保险'
      },
      q21_options: [
        { label: '1.购买了保险', value: '1' },
        { label: '2.没有购买保险', value: '2' }
      ],
      q20_answer: '',
      q20_answer_dict: {
        1: '1.豪华酒店（四星级及以上）',
        2: '2.中等价位酒店（二星、三星酒店）',
        3: '3.经济型酒店',
        4: '4.社会旅馆/青旅'
      },
      q20_options: [
        { label: '1.豪华酒店（四星级及以上）', value: '1' },
        { label: '2.中等价位酒店（二星、三星酒店）', value: '2' },
        { label: '3.经济型酒店', value: '3' },
        { label: '4.社会旅馆/青旅', value: '4' },
        { label: '5.其他（请注明）', value: '5' }
      ],
      q15_answer: '',
      q15_answer_dict: {
        1: '1.景点门票',
        2: '2.交通',
        3: '3.餐饮',
        4: '4.购物',
        5: '5.文化娱乐',
        6: '6.住宿'
      },
      q15_options: [
        { label: '1.景点门票', value: '1' },
        { label: '2.交通', value: '2' },
        { label: '3.餐饮', value: '3' },
        { label: '4.购物', value: '4' },
        { label: '5.文化娱乐', value: '5' },
        { label: '6.住宿', value: '6' },
        { label: '7.其他（请注明）', value: '7' }
      ],
      q16_answer: '',
      q16_answer_dict: {
        1: '1.0个',
        2: '2.1-2个',
        3: '3.3-5个',
        4: '4.6-9个',
        5: '5.10个及以上'
      },
      q16_options: [
        { label: '1.0个', value: '1' },
        { label: '2.1-2个', value: '2' },
        { label: '3.3-5个', value: '3' },
        { label: '4.6-9个', value: '4' },
        { label: '5.10个及以上', value: '5' }
      ],
      q11_answer: '',
      q11_options: [
        { label: '1.否', value: '1' },
        { label: '2.是', value: '2' }
      ],
      q14_answer: '',
      q14_answer_dict: {
        1: '1.旅行费用',
        2: '2.501-1000美元',
        3: '3.1001-2000美元',
        4: '4.2001-3000美元',
        5: '5.3001-5000美元',
        6: '6.5001-10000美元',
        7: '7.10000美元以上'
      },
      q14_options: [
        { label: '1.500美元以下', value: '1' },
        { label: '2.501-1000美元', value: '2' },
        { label: '3.1001-2000美元', value: '3' },
        { label: '4.2001-3000美元', value: '4' },
        { label: '5.3001-5000美元', value: '5' },
        { label: '6.5001-10000美元', value: '6' },
        { label: '7.10000美元以上', value: '7' }
      ],
      q19_answer: '',
      q19_answer_dict: {
        1: '1.当天往返',
        2: '2.2—3日以内',
        3: '3.4-7天',
        4: '4.8-15天',
        5: '5.一个月以内',
        6: '6.一个月以上'
      },
      q19_options: [
        { label: '1.当天往返', value: '1' },
        { label: '2.2—3日以内', value: '2' },
        { label: '3.4-7天', value: '3' },
        { label: '4.8-15天', value: '4' },
        { label: '5.一个月以内', value: '5' },
        { label: '6.一个月以上', value: '6' }
      ],
      q22_answer: [],
      q22_answer_dict: {
        1: '1.航空意外险',
        2: '2.交通意外险',
        3: '3.旅游意外险',
        4: '4.一般意外险',
        5: '5.旅游救助险',
        6: '6.旅行社责任险'
      },
      q22_options: [
        { label: '1.航空意外险', value: '1' },
        { label: '2.交通意外险', value: '2' },
        { label: '3.旅游意外险', value: '3' },
        { label: '4.一般意外险', value: '4' },
        { label: '5.旅游救助险', value: '5' },
        { label: '6.旅行社责任险', value: '6' },
        { label: '7.其他（请注明）', value: '7' }
      ],
      q36_answer: '',
      q36_answer_dict: {
        1: '1.是，已经预定/出行了',
        2: '2.是，正在等待打折才预定',
        3: '3.是，还没有决定',
        4: '4.否，明年及以后才准备出行'
      },
      q36_options: [
        { label: '1.是，已经预定/出行了', value: '1' },
        { label: '2.是，正在等待打折才预定', value: '2' },
        { label: '3.是，还没有决定', value: '3' },
        { label: '4.否，明年及以后才准备出行', value: '4' }
      ],
      q32_answer: '',
      q32_answer_dict: {
        1: '1.有',
        2: '2.没有'
      },
      q32_options: [
        { label: '1.有', value: '1' },
        { label: '2.没有', value: '2' }
      ],
      q33_answer: '',
      email: '',
      q33_answer_dict: {
        1: '1.很好',
        2: '2.还行',
        3: '3.糟糕',
        4: '4.非常糟糕'
      },
      q33_options: [
        { label: '1.很好', value: '1' },
        { label: '2.还行', value: '2' },
        { label: '3.糟糕', value: '3' },
        { label: '4.非常糟糕', value: '4' }
      ],
      q37_answer: '',
      q37_answer_dict: {
        1: '1.自己的国家',
        2: '2.中国',
        3: '3.其他国家',
        4: '4.不知道'
      },
      q37_options: [
        { label: '1.自己的国家', value: '1' },
        { label: '2.中国', value: '2' },
        { label: '3.其他国家', value: '3' },
        { label: '4.不知道', value: '4' }
      ],
      q38_answer: '',
      q38_answer_dict: {
        1: '1.了解中国特色文化',
        2: '2.游览/观光',
        3: '3.休闲/度假',
        4: '4.探亲访友',
        5: '1.商务',
        6: '2.会议',
        7: '3.文体/教育/科技交流',
        8: '4.宗教/朝拜',
        9: '4.健康医疗'
      },
      q38_options: [
        { label: '1.了解中国特色文化', value: '1' },
        { label: '2.游览/观光', value: '2' },
        { label: '3.休闲/度假', value: '3' },
        { label: '4.探亲访友', value: '4' },
        { label: '5.商务', value: '5' },
        { label: '6.会议', value: '6' },
        { label: '7.文体/教育/科技交流', value: '7' },
        { label: '8.宗教/朝拜', value: '8' },
        { label: '9.健康医疗', value: '9' },
        { label: '10.其他', value: '10' }
      ],
      q39_answer: '',
      q39_answer_dict: {
        1: '1.是的',
        2: '2.不是，我会在确定出行后开始收集',
        3: '3.不是，我从不提前看情报',
        4: '4.不是，我现在没有前往中国的计划'
      },
      q39_options: [
        { label: '1.是的', value: '1' },
        { label: '2.不是，我会在确定出行后开始收集', value: '2' },
        { label: '3.不是，我从不提前看情报', value: '3' },
        { label: '4.不是，我现在没有前往中国的计划', value: '4' },
        { label: '5.其他', value: '5' }
      ],
      q28_answer: 1,
      q40_answer: '',
      q40_answer_dict: {
        1: '1.春',
        2: '2.夏',
        3: '3.秋',
        4: '4.冬'
      },
      q40_options: [
        { label: '1.春', value: '1' },
        { label: '2.夏', value: '2' },
        { label: '3.秋', value: '3' },
        { label: '4.冬', value: '4' }
      ],
      q41_answer: '',
      q41_answer_dict: {
        1: '1.秋 2020',
        2: '2.冬 2021',
        3: '3.春 2021',
        4: '4.夏 2021',
        5: '5.秋 2021'
      },
      q41_options: [
        { label: '1.秋 2020', value: '1' },
        { label: '2.冬 2021', value: '2' },
        { label: '3.春 2021', value: '3' },
        { label: '4.夏 2021', value: '4' },
        { label: '5.秋 2021', value: '5' }
      ],
      q42_answer: '',
      q42_answer_dict: {
        1: '1.很大影响',
        2: '2.有影响',
        3: '3.影响很少',
        4: '4.完全没有影响'
      },
      q42_options: [
        { label: '1.很大影响', value: '1' },
        { label: '2.有影响', value: '2' },
        { label: '3.影响很少', value: '3' },
        { label: '4.完全没有影响', value: '4' }
      ],
      q43_answer: '',
      q17_answer_1: '',
      q17_answer_2: '',
      q17_answer_3: '',
      q17_answer_4: '',
      q29_answer: 1,
      q17_answer_5: '',
      q43_answer_dict: {
        1: '1.男',
        2: '2.女'
      },
      q43_options: [
        { label: '1.男', value: '1' },
        { label: '2.女', value: '2' }
      ],
      q24_answer_chengshixingxiang: 1,
      q24_answer_chengshifuwushuip: 1,
      q23_answer_lanzhou: 1,
      q23_answer_xining: 1,
      q23_answer_zhuhai: 1,
      q23_answer_shenzhen: 1,
      q23_answer_guilin: 1,
      q23_answer_kunming: 1,
      q23_answer_chengde: 1,
      q23_answer_hangzhou: 1,
      q23_answer_chengdu: 1,
      q23_answer_nanjing: 1,
      q23_answer_suzhou: 1,
      q23_answer_tianjin: 1,
      q23_answer_guangzhou: 1,
      q23_answer_xian: 1,
      q23_answer_shenyang: 1,
      q23_answer_chongqing: 1,
      q23_answer_shanghai: 1,
      q23_answer_beijing: 1,
      q25_answer_chengshifuwuzhiliangyuqi: 1,
      q25_answer_lvyoufuwuzhiliangyuqi: 1,
      q26_answer_lvyouzhiliangshifouheli: 1,
      q26_answer_jiagexiangfu: 1,
      q27_answer_xiandaihua: 1,
      q27_answer_meili: 1,
      q27_answer_zhimingdu: 1,
      q27_answer_kaifangdu: 1,
      q27_answer_xinxihua: 1,
      q34_answer_tuijian: 1,
      q34_answer_jixu: 1,
      q34_answer_zijichongyou: 1,
      q30_answer_zongti: 1,
      q30_answer_biaozhunhua: 1,
      q30_answer_gonggongfuwu: 1,
      q30_answer_fapiao: 1,
      q30_answer_chanpinfuwuzhiliang: 1,
      q30_answer_daoyou: 1,
      q30_answer_lvxingshe: 1,
      q30_answer_jingdian: 1,
      q30_answer_wenhua: 1,
      q30_answer_gouwu: 1,
      q30_answer_zhusu: 1,
      q30_answer_canyin: 1,
      q30_answer_jiaotong: 1,
      things2submit: {},
      alert: false
    }
  },
  methods: {
    validateNoneNullAndGoToNextPanel (val) {
      if (val.trim() !== null && val.trim() !== '') {
        this.checkAndGo()
      } else {
        this.alert = true
      }
    },
    goToPanel (panel) {
      this.slide = panel
    },
    submit () {
      this.things2submit.q1 = this.q1_answer
      this.things2submit.q2 = this.q2_answer
      this.things2submit.q3 = this.q3_answer_dict[this.q3_answer] == null ? this.q3_answer_qita : this.q3_answer_dict[this.q3_answer]
      this.things2submit.q4 = this.q4_answer
      this.things2submit.q5 = this.q5_answer
      this.things2submit.q6 = this.q6_answer_dict[this.q6_answer] == null ? this.q6_answer_qita : this.q6_answer_dict[this.q6_answer]
      this.things2submit.q7 = this.combineMulti(this.q7_answer_dict, this.q7_answer, this.q7_answer_qita)
      this.things2submit.q8 = this.q8_answer_dict[this.q8_answer] == null ? this.q8_answer_qita : this.q8_answer_dict[this.q8_answer]
      this.things2submit.q9 = this.combineMulti(this.q9_answer_dict, this.q9_answer, this.q9_answer_qita)
      this.things2submit.q10 = this.combineMulti(this.q10_answer_dict, this.q10_answer, this.q10_answer_qita)
      this.things2submit.q11 = this.q11_answer_dict[this.q11_answer]
      this.things2submit.q12 = this.q12_answer_qita
      this.things2submit.q13 = this.combineMulti(this.q13_answer_dict, this.q13_answer, this.q13_answer_qita)
      this.things2submit.q14 = this.q14_answer_dict[this.q14_answer]
      this.things2submit.q15 = this.q15_answer_dict[this.q15_answer] == null ? this.q15_answer_qita : this.q15_answer_dict[this.q15_answer]
      this.things2submit.q16 = this.q16_answer_dict[this.q16_answer] == null ? this.q16_answer_qita : this.q16_answer_dict[this.q16_answer]
      this.things2submit.q17 = this.q17_answer_1 + ',' + this.q17_answer_2 + ',' + this.q17_answer_3 + ',' + this.q17_answer_4 + ',' + this.q17_answer_5
      this.things2submit.q18 = this.q18_answer_1 + ',' + this.q18_answer_2 + ',' + this.q18_answer_3 + ',' + this.q18_answer_4 + ',' + this.q18_answer_5 + ',' + this.q18_answer_6 + ',' + this.q18_answer_7 + ',' + this.q18_answer_8 + ',' + this.q18_answer_9 + ',' + this.q18_answer_10
      this.things2submit.q19 = this.q19_answer_dict[this.q19_answer]
      this.things2submit.q20 = this.q20_answer_dict[this.q20_answer] == null ? this.q20_answer_qita : this.q20_answer_dict[this.q20_answer]
      this.things2submit.q21 = this.q21_answer_dict[this.q21_answer]
      this.things2submit.q22 = this.combineMulti(this.q22_answer_dict, this.q22_answer, this.q22_answer_qita)
      this.things2submit.q23 = '北京: ' + this.q23_answer_beijing +
      ',上海: ' + this.q23_answer_shanghai +
      ',重庆: ' + this.q23_answer_chongqing +
      ',沈阳: ' + this.q23_answer_shenyang +
      ',西安: ' + this.q23_answer_xian +
      ',广州: ' + this.q23_answer_guangzhou +
      ',天津: ' + this.q23_answer_tianjin +
      ',苏州: ' + this.q23_answer_suzhou +
      ',南京: ' + this.q23_answer_nanjing +
      ',成都: ' + this.q23_answer_chengdu +
      ',杭州: ' + this.q23_answer_hangzhou +
      ',承德: ' + this.q23_answer_chengde +
      ',昆明: ' + this.q23_answer_kunming +
      ',桂林: ' + this.q23_answer_guilin +
      ',深圳: ' + this.q23_answer_shenzhen +
      ',珠海: ' + this.q23_answer_zhuhai +
      ',西宁: ' + this.q23_answer_xining +
      ',兰州: ' + this.q23_answer_lanzhou
      this.things2submit.q24 = '城市形象: ' + this.q24_answer_chengshixingxiang + ',城市服务水平: ' + this.q24_answer_chengshifuwushuip
      this.things2submit.q25 = '城市服务质量预期: ' + this.q25_answer_chengshifuwuzhiliangyuqi + ',旅游服务质量预期: ' + this.q25_answer_lvyoufuwuzhiliangyuqi
      this.things2submit.q26 = '旅游价格是否合理: ' + this.q26_answer_lvyouzhiliangshifouheli + ',旅游质量是否与旅游价格相符:' + this.q26_answer_jiagexiangfu
      this.things2submit.q27 = '现代化程度: ' + this.q27_answer_xiandaihua + ',美丽程度: ' + this.q27_answer_meili + ',知名度: ' + this.q27_answer_zhimingdu + ',开放度: ' + this.q27_answer_kaifangdu + ',信息化程度（智慧城市): ' + this.q27_answer_xinxihua
      this.things2submit.q28 = this.q28_answer
      this.things2submit.q29 = this.q29_answer
      this.things2submit.q30 = '交通: ' + this.q30_answer_jiaotong +
      ',餐饮: ' + this.q30_answer_canyin +
      ',住宿: ' + this.q30_answer_zhusu +
      ',购物: ' + this.q30_answer_gouwu +
      ',文化娱乐: ' + this.q30_answer_wenhua +
      ',景区景点: ' + this.q30_answer_jingdian +
      ',旅行社: ' + this.q30_answer_lvxingshe +
      ',导游: ' + this.q30_answer_daoyou +
      ',产品和服务质量: ' + this.q30_answer_chanpinfuwuzhiliang +
      ',发票具备及正规度: ' + this.q30_answer_fapiao +
      ',旅游公共服务: ' + this.q30_answer_gonggongfuwu +
      ',标准化程度: ' + this.q30_answer_biaozhunhua +
      ',总体服务质量: ' + this.q30_answer_zongti

      this.things2submit.q31 = '总体满意程度: ' + this.q31_answer_zongti +
      ',与需求相比满意程度: ' + this.q31_answer_xiangbi +
      ',与理想中相比的满意程度: ' + this.q31_answer_lixiang

      this.things2submit.q32 = this.q32_answer_dict[this.q32_answer]
      this.things2submit.q33 = this.q33_answer_dict[this.q33_answer]

      this.things2submit.q34 = '未来自己重游: ' + this.q34_answer_zijichongyou +
      ',未来继续选择该旅行社的可能性: ' + this.q34_answer_jixu +
      ',未来推荐亲友: ' + this.q34_answer_tuijian

      this.things2submit.q35 = this.q35_answer_qita

      this.things2submit.q36 = this.q36_answer_dict[this.q36_answer]
      this.things2submit.q37 = this.q37_answer_dict[this.q37_answer]
      this.things2submit.q38 = this.q38_answer_dict[this.q38_answer] == null ? this.q38_answer_qita : this.q38_answer_dict[this.q38_answer]
      this.things2submit.q39 = this.q39_answer_dict[this.q39_answer] == null ? this.q39_answer_qita : this.q39_answer_dict[this.q39_answer]
      this.things2submit.q40 = this.q40_answer_dict[this.q40_answer]
      this.things2submit.q41 = this.q41_answer_dict[this.q41_answer]
      this.things2submit.q42 = this.q42_answer_dict[this.q42_answer]
      this.things2submit.q43 = this.q43_answer_dict[this.q43_answer]
      this.things2submit.q44 = this.q44_answer_qita
      this.things2submit.q45 = this.q45_answer_dict[this.q45_answer]
      this.things2submit.q46 = this.q46_answer_dict[this.q46_answer]
      this.things2submit.q47 = this.q47_answer_dict[this.q47_answer] == null ? this.q47_answer_qita : this.q47_answer_dict[this.q47_answer]
      this.things2submit.q48 = this.q48_answer_dict[this.q48_answer]

      axios.get('/api/v1/user', {
        test: 'test'
      }).then(response => {
        console.log('normal')
      }).catch(e => {
        console.log('bad')
      })

      console.log(this.things2submit)
    },
    combineMulti (dic, arr, plaintext) {
      var i
      var ret = ''
      for (i = 0; i < arr.length; i++) {
        if (ret.length > 0) {
          ret += ';'
        }
        ret = ret + (dic[arr[i]] == null ? plaintext : dic[arr[i]])
      }
      return ret
    },
    goToNextPanelOnCondition (normal, destination) {
      if (normal) {
        this.$refs.carousel.next()
      } else {
        this.checkAndGoSpecific(destination)
      }
    },
    goToNextPanel () {
      this.$refs.carousel.next()
    },
    goToNextPanelExcept (val, biaozhun) {
      if (val === biaozhun) {

      } else {
        this.goToNextPanel()
      }
    },
    checkAndGo () {
      console.log('executed check and')
      this.$refs.carousel.next()
    },
    checkAndGoSpecific (val) {
      this.slide = val
    }
  }
}
</script>

<style scoped>
.sv-title{
  font-size: 150%;
}

.sub_but{
  float:right;
  position:absolute;
  bottom:0;
  margin-bottom: 50px;
  margin-left: 175px;
}

.sv-container{
  margin-bottom: 180px;
}
</style>
