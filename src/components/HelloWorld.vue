<template>
  <div class="if">
    <h1>火焰纹章if升级模拟器</h1>
    <p class="mark" v-if="person.name === '神威'">自捏神威默认得意速度苦手运</p>
    <p class="mark" v-if="person.name === '物集'">物集的成长率因良成长默认全部加10，职业选项没有村姑</p>
    <el-select v-model="name" placeholder="请选择人物">
      <el-option
        v-for="item in persons"
        :key="item.name"
        :value="item.name">
      </el-option>
    </el-select>
    <el-select v-if="name" v-model="classical" placeholder="请选择职业">
      <el-option
        v-for="item in professionals"
        :key="item.classical"
        :value="item.classical">
      </el-option>
    </el-select>
    <el-row v-if="person&&professional" :gutter="20">
      <el-col :span="11">
        <h3>{{person.name}}成长率</h3>
        <el-table :data="person.personup">
          <el-table-column
            prop="attr"
            label="属性">
          </el-table-column>
          <el-table-column
            prop="val"
            label="成长率">
          </el-table-column>
        </el-table>
      </el-col>
      <el-col :span="11">
        <h3>{{professional.classical}}职业成长率</h3>
        <el-table :data="professional.professionalup">
          <el-table-column
            prop="attr"
            label="属性">
          </el-table-column>
          <el-table-column
            prop="val"
            label="成长率">
          </el-table-column>
        </el-table>
      </el-col>
    </el-row>
    <div class="info" v-if="person&&professional">
      <h3>人物基础属性</h3>
      <img :src="person.avatar" alt="">
      <p>{{person.name}}</p>
      <p>职业：{{professional.classical}}</p>
      <p>等级：{{person.lv}}</p>
      <template v-for="(item, index) in person.ablity">
        <p :key="item.attr">{{item.attr}}: {{item.val}} <span class="uped" v-if="index === list[index]">+1</span></p>
      </template>
      <el-button :disabled="lv40" type="danger" @click="lvup">升级</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [1, 2, 3, 4, 5, 6, 7, 8],
      professionals: [
        {
          classical: '黑暗王子',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 10},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '歌姬',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 20},
            {attr: '速度', val: 20},
            {attr: '运气', val: 20},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '暗夜血族',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 5},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 15}
          ]
        },
        {
          classical: '白夜血族',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 10},
            {attr: '防御', val: 15},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '女仆',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 10},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '管家',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 10},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '侍',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 20},
            {attr: '运气', val: 15},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '剑圣',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 5},
            {attr: '技术', val: 15},
            {attr: '速度', val: 20},
            {attr: '运气', val: 15},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '忍者',
          professionalup: [
            {attr: 'hp', val: 5},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 20},
            {attr: '速度', val: 20},
            {attr: '运气', val: 0},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 15}
          ]
        },
        {
          classical: '上忍',
          professionalup: [
            {attr: 'hp', val: 5},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 20},
            {attr: '速度', val: 20},
            {attr: '运气', val: 0},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '弓使',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '弓圣',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 20},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '枪术士',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '枪圣',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '兵法者',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 10},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '药商人',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 20},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '大商人',
          professionalup: [
            {attr: 'hp', val: 15},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 5},
            {attr: '运气', val: 15},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '傀儡师',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 10},
            {attr: '运气', val: 5},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 15}
          ]
        },
        {
          classical: '天马武者',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 20},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '圣天马武者',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 20},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '金鵄武者',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 15},
            {attr: '运气', val: 15},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 15}
          ]
        },
        {
          classical: '鬼人',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 20},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 0},
            {attr: '速度', val: 10},
            {attr: '运气', val: 0},
            {attr: '防御', val: 20},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '修罗',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 20},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 0},
            {attr: '速度', val: 10},
            {attr: '运气', val: 0},
            {attr: '防御', val: 20},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '锻冶',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 10},
            {attr: '运气', val: 5},
            {attr: '防御', val: 15},
            {attr: '魔防', val: 0}
          ]
        },
        {
          classical: '婆娑罗',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 15},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '咒术师',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '阴阳师',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 0},
            {attr: '魔力', val: 20},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 0},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 15}
          ]
        },
        {
          classical: '修验者',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 15},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '山伏',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 5},
            {attr: '技术', val: 5},
            {attr: '速度', val: 15},
            {attr: '运气', val: 15},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '巫女',
          professionalup: [
            {attr: 'hp', val: 0},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 10},
            {attr: '速度', val: 15},
            {attr: '运气', val: 5},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '战巫女',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 5},
            {attr: '速度', val: 15},
            {attr: '运气', val: 15},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '妖狐',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 20},
            {attr: '运气', val: 10},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '九尾狐',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 15},
            {attr: '速度', val: 20},
            {attr: '运气', val: 10},
            {attr: '防御', val: 0},
            {attr: '魔防', val: 20}
          ]
        },
        {
          classical: '轻骑士',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 15},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ]
        },
        {
          classical: '圣骑士',
          professionalup: [
            {attr: 'hp', val: 10},
            {attr: '力量', val: 15},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 15},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 10}
          ]
        },
        {
          classical: '重骑士',
          professionalup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 20},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 10},
            {attr: '速度', val: 5},
            {attr: '运气', val: 5},
            {attr: '防御', val: 20},
            {attr: '魔防', val: 0}
          ]
        }
      ],
      persons: [
        {
          name: '神威',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Kamui.png',
          ablity: [
            {attr: 'hp', val: 19},
            {attr: '力量', val: 7},
            {attr: '魔力', val: 4},
            {attr: '技术', val: 7},
            {attr: '速度', val: 8},
            {attr: '运气', val: 3},
            {attr: '防御', val: 6},
            {attr: '魔防', val: 2}
          ],
          personup: [
            {attr: 'hp', val: 45},
            {attr: '力量', val: 40},
            {attr: '魔力', val: 25},
            {attr: '技术', val: 45},
            {attr: '速度', val: 60},
            {attr: '运气', val: 30},
            {attr: '防御', val: 35},
            {attr: '魔防', val: 25}
          ]
        },
        {
          name: '阿库娅',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Aqua.png',
          ablity: [
            {attr: 'hp', val: 16},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 2},
            {attr: '技术', val: 8},
            {attr: '速度', val: 8},
            {attr: '运气', val: 6},
            {attr: '防御', val: 4},
            {attr: '魔防', val: 7}
          ],
          personup: [
            {attr: 'hp', val: 25},
            {attr: '力量', val: 50},
            {attr: '魔力', val: 25},
            {attr: '技术', val: 60},
            {attr: '速度', val: 60},
            {attr: '运气', val: 40},
            {attr: '防御', val: 15},
            {attr: '魔防', val: 35}
          ]
        },
        {
          name: '菲利西亚',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Felicia.png',
          ablity: [
            {attr: 'hp', val: 19},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 9},
            {attr: '技术', val: 10},
            {attr: '速度', val: 10},
            {attr: '运气', val: 12},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 9}
          ],
          personup: [
            {attr: 'hp', val: 40},
            {attr: '力量', val: 10},
            {attr: '魔力', val: 35},
            {attr: '技术', val: 30},
            {attr: '速度', val: 40},
            {attr: '运气', val: 55},
            {attr: '防御', val: 15},
            {attr: '魔防', val: 35}
          ]
        },
        {
          name: '乔克',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Joker.png',
          ablity: [
            {attr: 'hp', val: 21},
            {attr: '力量', val: 8},
            {attr: '魔力', val: 6},
            {attr: '技术', val: 12},
            {attr: '速度', val: 9},
            {attr: '运气', val: 10},
            {attr: '防御', val: 7},
            {attr: '魔防', val: 6}
          ],
          personup: [
            {attr: 'hp', val: 50},
            {attr: '力量', val: 30},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 40},
            {attr: '速度', val: 35},
            {attr: '运气', val: 45},
            {attr: '防御', val: 25},
            {attr: '魔防', val: 25}
          ]
        },
        {
          name: '凉风',
          lv: 3,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Suzukaze.png',
          ablity: [
            {attr: 'hp', val: 19},
            {attr: '力量', val: 7},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 9},
            {attr: '速度', val: 12},
            {attr: '运气', val: 4},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 10}
          ],
          personup: [
            {attr: 'hp', val: 55},
            {attr: '力量', val: 40},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 45},
            {attr: '速度', val: 65},
            {attr: '运气', val: 20},
            {attr: '防御', val: 20},
            {attr: '魔防', val: 35}
          ]
        },
        {
          name: '塞拉斯',
          lv: 6,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Silas.png',
          ablity: [
            {attr: 'hp', val: 22},
            {attr: '力量', val: 11},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 9},
            {attr: '速度', val: 8},
            {attr: '运气', val: 7},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 5}
          ],
          personup: [
            {attr: 'hp', val: 40},
            {attr: '力量', val: 45},
            {attr: '魔力', val: 5},
            {attr: '技术', val: 50},
            {attr: '速度', val: 40},
            {attr: '运气', val: 40},
            {attr: '防御', val: 40},
            {attr: '魔防', val: 25}
          ]
        },
        {
          name: '物集',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Mozume.png',
          ablity: [
            {attr: 'hp', val: 17},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 4},
            {attr: '速度', val: 5},
            {attr: '运气', val: 3},
            {attr: '防御', val: 4},
            {attr: '魔防', val: 0}
          ],
          personup: [
            {attr: 'hp', val: 40},
            {attr: '力量', val: 50},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 60},
            {attr: '速度', val: 65},
            {attr: '运气', val: 55},
            {attr: '防御', val: 45},
            {attr: '魔防', val: 40}
          ]
        },
        {
          name: '樱',
          lv: 1,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Sakura.png',
          ablity: [
            {attr: 'hp', val: 16},
            {attr: '力量', val: 3},
            {attr: '魔力', val: 6},
            {attr: '技术', val: 5},
            {attr: '速度', val: 7},
            {attr: '运气', val: 9},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 7}
          ],
          personup: [
            {attr: 'hp', val: 45},
            {attr: '力量', val: 30},
            {attr: '魔力', val: 50},
            {attr: '技术', val: 40},
            {attr: '速度', val: 40},
            {attr: '运气', val: 55},
            {attr: '防御', val: 30},
            {attr: '魔防', val: 20}
          ]
        },
        {
          name: '燐火',
          lv: 4,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Rinka.png',
          ablity: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 8},
            {attr: '魔力', val: 2},
            {attr: '技术', val: 6},
            {attr: '速度', val: 8},
            {attr: '运气', val: 5},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 3}
          ],
          personup: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 25},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 50},
            {attr: '速度', val: 45},
            {attr: '运气', val: 35},
            {attr: '防御', val: 45},
            {attr: '魔防', val: 20}
          ]
        },
        {
          name: '风花',
          lv: 4,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Kazahana.png',
          ablity: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 9},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 11},
            {attr: '速度', val: 11},
            {attr: '运气', val: 5},
            {attr: '防御', val: 6},
            {attr: '魔防', val: 9}
          ],
          personup: [
            {attr: 'hp', val: 25},
            {attr: '力量', val: 55},
            {attr: '魔力', val: 10},
            {attr: '技术', val: 45},
            {attr: '速度', val: 55},
            {attr: '运气', val: 25},
            {attr: '防御', val: 20},
            {attr: '魔防', val: 30}
          ]
        },
        {
          name: '椿',
          lv: 5,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Tsubaki.png',
          ablity: [
            {attr: 'hp', val: 22},
            {attr: '力量', val: 8},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 13},
            {attr: '速度', val: 10},
            {attr: '运气', val: 7},
            {attr: '防御', val: 9},
            {attr: '魔防', val: 10}
          ],
          personup: [
            {attr: 'hp', val: 55},
            {attr: '力量', val: 30},
            {attr: '魔力', val: 20},
            {attr: '技术', val: 50},
            {attr: '速度', val: 20},
            {attr: '运气', val: 25},
            {attr: '防御', val: 45},
            {attr: '魔防', val: 5}
          ]
        },
        {
          name: '才藏',
          lv: 7,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Saizou.png',
          ablity: [
            {attr: 'hp', val: 23},
            {attr: '力量', val: 11},
            {attr: '魔力', val: 3},
            {attr: '技术', val: 14},
            {attr: '速度', val: 11},
            {attr: '运气', val: 9},
            {attr: '防御', val: 9},
            {attr: '魔防', val: 7}
          ],
          personup: [
            {attr: 'hp', val: 40},
            {attr: '力量', val: 50},
            {attr: '魔力', val: 45},
            {attr: '技术', val: 60},
            {attr: '速度', val: 30},
            {attr: '运气', val: 55},
            {attr: '防御', val: 45},
            {attr: '魔防', val: 10}
          ]
        },
        {
          name: '大蛇',
          lv: 5,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Orochi.png',
          ablity: [
            {attr: 'hp', val: 20},
            {attr: '力量', val: 0},
            {attr: '魔力', val: 9},
            {attr: '技术', val: 11},
            {attr: '速度', val: 7},
            {attr: '运气', val: 6},
            {attr: '防御', val: 5},
            {attr: '魔防', val: 10}
          ],
          personup: [
            {attr: 'hp', val: 35},
            {attr: '力量', val: 5},
            {attr: '魔力', val: 65},
            {attr: '技术', val: 50},
            {attr: '速度', val: 15},
            {attr: '运气', val: 35},
            {attr: '防御', val: 25},
            {attr: '魔防', val: 45}
          ]
        },
        {
          name: '日乃香',
          lv: 8,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Hinoka.png',
          ablity: [
            {attr: 'hp', val: 23},
            {attr: '力量', val: 9},
            {attr: '魔力', val: 4},
            {attr: '技术', val: 13},
            {attr: '速度', val: 16},
            {attr: '运气', val: 12},
            {attr: '防御', val: 9},
            {attr: '魔防', val: 15}
          ],
          personup: [
            {attr: 'hp', val: 45},
            {attr: '力量', val: 45},
            {attr: '魔力', val: 15},
            {attr: '技术', val: 40},
            {attr: '速度', val: 45},
            {attr: '运气', val: 45},
            {attr: '防御', val: 35},
            {attr: '魔防', val: 40}
          ]
        },
        {
          name: '拓海',
          lv: 11,
          avatar: 'http://fcfantasy.cn/fe2015/image/portrait100/Takumi.png',
          ablity: [
            {attr: 'hp', val: 26},
            {attr: '力量', val: 13},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 17},
            {attr: '速度', val: 11},
            {attr: '运气', val: 13},
            {attr: '防御', val: 10},
            {attr: '魔防', val: 4}
          ],
          personup: [
            {attr: 'hp', val: 50},
            {attr: '力量', val: 35},
            {attr: '魔力', val: 0},
            {attr: '技术', val: 60},
            {attr: '速度', val: 40},
            {attr: '运气', val: 45},
            {attr: '防御', val: 35},
            {attr: '魔防', val: 20}
          ]
        }
      ],
      name: '',
      person: '',
      professional: '',
      classical: ''
    }
  },
  computed: {
    lv40 () {
      if (this.person.lv >= 40) {
        return true
      } else {
        return false
      }
    }
  },
  watch: {
    name () {
      if (this.name !== '') {
        this.person = this.persons.find(p => {
          return p.name === this.name
        })
      }
    },
    classical () {
      if (this.classical !== '') {
        this.professional = this.professionals.find(z => {
          return z.classical === this.classical
        })
      }
    }
  },
  methods: {
    lvup () {
      this.person.lv = this.person.lv + 1
      for (let i = 0; i < this.person.ablity.length; i++) {
        setTimeout(() => {
          if (this.person.personup[i].val + this.professional.professionalup[i].val > Math.floor(Math.random() * 100)) {
            // 让对应的能力处显示+1
            this.list[i] = this.list[i] - 1
            // 能力+1
            this.person.ablity[i].val = this.person.ablity[i].val + 1
          }
        }, 400)
      }
      this.list = [1, 2, 3, 4, 5, 6, 7, 8]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.if {
  margin: 0 auto;
  max-width: 460px;
}
.uped {
  color: green;
  margin: 0 0 0 10px;
}
.mark {
  font-size: 14px;
  color: rgb(121, 37, 37);
}
.el-button {
  width: 20%;
}
</style>
