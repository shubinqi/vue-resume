<template>
  <div class="resume">
    <!-- 头部信息 -->
    <div class="header card">
      <div class="name">
        <h1
          contenteditable
          v-text="name"
        ></h1>
        <h3
          contenteditable
          v-text="title"
        ></h3>
        <p
          contenteditable
          v-text="subTitle"
        ></p>
      </div>
      <div class="image">
        <input
          type="file"
          ref="fileInput"
          @change="handleFileChange"
        >
        <img
          :src="imageUrl"
          v-if="imageUrl"
        >
      </div>
    </div>
    <!-- 个人信息 -->
    <div
      @dragenter="dragenter($event, s, 'cardList')"
      @dragover="dragover($event, s)"
      @dragstart="dragstart(s)"
      class="infomation card"
      v-for="(item, s) in cardList"
      :key="item.s"
    >
      <h2
        class="card-title"
        draggable
      >
        <span contenteditable>{{ item.name }}</span>
        <button
          class="add"
          @click="handleAdd({
            name: item.list
          })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: item.show,
            num: 0
          })"
        >+</button>
      </h2>
      <!-- 个人信息 -->
      <div
        class="infoList"
        v-if="item.type === '1'"
      >
        <div
          class="infor-item"
          v-for="(item) in infoList"
          :key="item.ss"
        >
          <!-- <div
          class="infor-item"
          @dragenter="dragenter($event, ss, 'infoList')"
          @dragover="dragover($event, ss)"
          @dragstart="dragstart(ss)"
          draggable
        > -->
          <span
            contenteditable
            v-text="item.title"
          ></span>
          <span
            contenteditable
            v-text="item.intro"
          ></span>
          <button
            class="delete"
            contenteditable="false"
            @click="handleDeleteChildren({
              name: 'infoList',
              index: -10,
              i: index
            })"
          >+</button>
        </div>
      </div>
      <!-- 专业技能 -->
      <ul
        class="skillList tasks"
        v-if="item.type === '2'"
      >
        <li
          contenteditable
          v-for="(item, i) in skillList"
          :key="i"
        >{{ item }} <button
            class="delete"
            contenteditable="false"
            @click="handleDeleteChildren({
              name: 'skillList',
              index: -10,
              i: i
            })"
          >+</button></li>
        <button
          class="add"
          @click="handleAdd({
              name: 'skillList',
              content: '随便加点啥。'
            })"
        >+</button>
      </ul>
      <!-- 自我评价 -->
      <p
        contenteditable
        v-text="summary"
        v-if="item.type === '3'"
      ></p>
      <!-- 工作经历 -->
      <div
        class="box"
        v-if="item.type === '4'"
      >
        <div
          class="company"
          v-for="(company, index) in companyList"
          :key="index"
        >
          <h3 class="company-title">
            <span
              contenteditable
              v-text="company.company"
            ></span>
            <span
              contenteditable
              v-text="company.date"
            ></span>
            <span
              contenteditable
              v-text="company.title"
            ></span>
            <button
              class="delete"
              contenteditable="false"
              @click="handleDeleteChildren({
              name: 'companyList',
              index: -10,
              i: i
            })"
            >+</button>
          </h3>
          <ul class="tasks">
            <li
              contenteditable
              v-for="(task, i) in company.tasks"
              :key="i"
            >{{ task }} <button
                class="delete"
                contenteditable="false"
                @click="handleDeleteChildren({
              name: 'companyList',
              index: index,
              i: i
            })"
              >+</button></li>
            <button
              class="add"
              @click="handleAddChildren({
                name: 'companyList',
                index: index
              })"
            >+</button>
          </ul>
        </div>
      </div>
      <!-- 项目经历 -->
      <div
        class="box"
        v-if="item.type === '5'"
      >
        <div
          class="projects"
          v-for="(job, index) in experienceList"
          :key="index"
        >
          <h3 class="project-title">
            <span
              contenteditable
              v-text="job.title"
            ></span>
            <span
              contenteditable
              v-text="job.date"
            ></span>
            <span
              contenteditable
              v-text="job.company"
            ></span>
            <button
              class="delete"
              contenteditable="false"
              @click="handleDeleteChildren({
              name: 'experienceList',
              index: -10,
              i: i
            })"
            >+</button>
          </h3>
          <p contenteditable><span contenteditable>项目简介：</span>该项目是一个移动端电商网站，包含商品列表、商品详情、购物车、订单结算等功能。使用Vue框架和Vant组件库实现页面的开发，使用Vuex管理状态，使用axios库进行数据交互。本人主要负责购物车和订单结算模块的开发，实现了购物车的增删改查和订单的生成和支付功能。</p>
          <p contenteditable><span contenteditable>技术栈：</span>Vue2 + Vue-Cli</p>
          <ul class="tasks">
            <li
              contenteditable
              v-for="(task, i) in job.tasks"
              :key="i"
            >{{ task }} <button
                class="delete"
                contenteditable="false"
                @click="handleDeleteChildren({
              name: 'experienceList',
              index: index,
              i: i
            })"
              >+</button></li>
            <button
              class="add"
              @click="handleAddChildren({
                name: 'experienceList',
                index: index
              })"
            >+</button>
          </ul>
        </div>
      </div>
      <!-- 教育经历 -->
      <div
        class="box"
        v-if="item.type === '6'"
      >
        <div
          class="degree"
          v-for="(degree, index) in educationList"
          :key="index"
        >
          <h3 class="degree-title">
            <span
              contenteditable
              v-text="degree.school"
            ></span>
            <span
              contenteditable
              v-text="degree.degree"
            ></span>
            <span
              contenteditable
              v-text="degree.date"
            ></span>
            <button
              class="delete"
              contenteditable="false"
              @click="handleDeleteChildren({
              name: 'educationList',
              index: -10,
              i: i
            })"
            >+</button>
          </h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import cardList from './card-list.vue'

export default {
  name: "ResumeName",
  // components: {
  //   cardList
  // },
  data () {
    return {
      name: "姓名", // 姓名
      title: "前端开发工程师", // 岗位
      subTitle: '男  |  25岁  |  软件技术  |  3年经验', // 重点信息
      imageUrl: null, // 头像
      summary: '掌握Web前端开发基本技能，熟悉W3C标准、页面布局架构、前端语义化、浏览器兼容性等，懂些审美，擅长设计，重视用户体验与代码可维护性，有近2年的前端开发经验。', // 自我评价
      cardList: [{
        name: '个人信息',
        show: 'info',
        list: 'infoList',
        type: '1'
      }, {
        name: '专业技能',
        show: 'ssss',
        list: 'skillList',
        type: '2'
      }, {
        name: '自我评价',
        show: 'summary',
        list: '',
        type: '3'
      }, {
        name: '工作经历',
        show: 'company',
        list: 'companyList',
        type: '4'
      }, {
        name: '项目经历',
        show: 'experience',
        list: 'experienceList',
        type: '5'
      }, {
        name: '教育经历',
        show: 'education',
        list: 'educationList',
        type: '6'
      }],
      skillList: [
        "精通 HTML+CSS，并能快速处理各浏览器兼容问题；",
        "熟练掌握 JavaScript 或 TypeScript",
        "熟练掌握 Vue 全家桶项目的开发"
      ], // 专业技能
      infoList: [{
        title: '性别：',
        intro: '男'
      }, {
        title: '学历：',
        intro: '本科'
      }, {
        title: '专业：',
        intro: '软件工程'
      }, {
        title: '经验：',
        intro: '3年'
      }, {
        title: '电话：',
        intro: '18888888888'
      }, {
        title: '邮箱：',
        intro: '123456@163.com'
      }], // 个人信息
      companyList: [], // 工作经历
      experienceList: [], // 项目经历
      educationList: [], // 教育经历
      dragIndex: '',
      dragIndexs: '',
      enterIndex: '',
      card: {
        info: 2,
        ssss: 2,
        summary: 2,
        company: 2,
        experience: 2,
        education: 2
      }
    };
  },
  created () {
    this.init()
  },
  methods: {
    // 初始化数据
    init () {
      this.handleAdd({
        name: 'companyList'
      })
      this.handleAdd({
        name: 'experienceList'
      })
      this.handleAdd({
        name: 'experienceList'
      })
      this.handleAdd({
        name: 'educationList'
      })
    },
    // 拖拽个人信息顺序
    dragstart (index) {
      this.dragIndex = index;
    },
    // 拖拽个人信息顺序
    dragenter (e, index, list) {
      e.preventDefault();
      // 避免源对象触发自身的dragenter事件
      if (this.dragIndex !== index) {
        if (list === 'infoList') {
          const source = this.infoList[this.dragIndex];
          this.infoList.splice(this.dragIndex, 1);
          this.infoList.splice(index, 0, source);
        } else {
          const source = this.cardList[this.dragIndex];
          this.cardList.splice(this.dragIndex, 1);
          this.cardList.splice(index, 0, source);
        }
        // 排序变化后目标对象的索引变成源对象的索引
        this.dragIndex = index;
      }
    },
    // 拖拽个人信息顺序
    dragover (e) {
      e.preventDefault();
    },
    // 添加板块数据
    handleAdd (data) {
      const content = {
        infoList: {
          title: '项目：',
          intro: '项目内容'
        },
        companyList: {
          date: "2022.09-2023.03",
          company: "深圳市XXX有限公司",
          title: "前端开发工程师",
          tasks: [
            "参与团队的代码审核和重构，提高代码质量和可维护性。",
            "与后台工程师配合，实现前后端数据的交互和接口的对接，使用axios库进行AJAX请求。",
            "参与公司的技术分享，分享自己的经验和学习成果，学习其他同事的优秀经验和技能。"
          ],
        },
        experienceList: {
          title: "后台管理系统项目",
          company: "前端开发工程师",
          date: "2022.09-2022.12",
          tasks: [
            "根据UI设计师提供的设计图，编写静态页面，完成页面排版。",
            "解决各大浏览器的兼容问题。",
            "与UI、产品经理等同事交流，提出可行性的建议和实施方法。"
          ],
        },
        educationList: {
          school: "浙江大学（本科）",
          degree: "软件技术",
          date: "2016.09-2020.07",
        }
      }
      this[data.name].push(!data.content ? content[data.name] : '随便加点什么吧！')
    },
    // 添加子列表数据
    handleAddChildren (data) {
      this[data.name][data.index].tasks.push('随便加点什么吧！')
    },
    // 删除板块
    handleDelete (data) {
      this.card[data.card] = data.num
    },
    // 删除子列表数据
    handleDeleteChildren (data) {
      console.log(data, this[data.name], '111')
      if (data.index >= 0) {
        if (this[data.name][data.index].tasks.length === 1) {
          alert('最少保留一个！')
          return
        }
        this[data.name][data.index].tasks.splice([data.i], 1)
      } else {
        if (this[data.name].length === 1) {
          alert('最少保留一个！')
          return
        }
        this[data.name].splice([data.i], 1)
      }
    },
    // 添加简历照片
    handleFileChange () {
      const file = this.$refs.fileInput.files[0];
      const reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = () => {
        this.imageUrl = reader.result;
      };
    }
  }
};
</script>

<style lang="less" scoped>
ul {
  list-style: auto;
  margin: 0;
  padding: 0;
}

.resume {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.5;
}

.header {
  position: relative;
}

.card {
  margin-bottom: 30px;
}

.card-title {
  position: relative;
  span {
    color: #333;
    padding: 5px 12px;
  }
  &:after {
    content: '';
    position: absolute;
    left: 0;
    top: 6px;
    width: 4px;
    height: 25px;
    background: #333;
  }
  .add {
    opacity: 0;
    font-size: 20px;
    font-weight: 700;
    border-radius: 50%;
    cursor: pointer;
    margin-right: 5px;
  }
  .delete {
    opacity: 0;
    font-size: 20px;
    font-weight: 700;
    border-radius: 50%;
    transform: rotate(45deg);
    cursor: pointer;
    margin-right: 5px;
  }
}

.card-title {
  &:hover .add,
  &:hover .delete {
    opacity: 1;
  }
}

.company-title,
.project-title,
.degree-title {
  display: flex;
  justify-content: space-between;
}

.name {
  margin-right: 20px;
  h1 {
    font-size: 36px;
    margin-top: 20px;
    margin-bottom: 15px;
  }
  h3 {
    font-size: 22px;
    margin-bottom: 5px;
  }
  p {
    font-size: 18px;
  }
}

.image {
  position: absolute;
  top: 10px;
  right: 20px;
  width: 90px;
  height: 126px;
  input {
    opacity: 0;
    width: 90px;
    z-index: 2;
    position: relative;
    height: 140px;
    cursor: pointer;
  }
  &:hover input {
    opacity: 1;
  }
  img {
    position: absolute;
    top: 0;
    left: 0;
    width: 90px;
    height: 126px;
    object-fit: cover;
  }
}

.infoList {
  display: flex;
  flex-wrap: wrap;
  .infor-item {
    cursor: move;
    width: 33.333%;
    &:hover {
      color: skyblue;
      background: #f5f7f9;
    }
    span {
      cursor: auto;
      line-height: 2.5;
    }
  }
}

.summary {
  p {
    font-size: 16px;
    margin: 0;
  }
}

.summary,
.experience,
.education {
  h2 {
    font-size: 24px;
    margin-bottom: 20px;
  }
}

.projects {
  margin-bottom: 25px;
  p {
    font-size: 16px;
    margin-top: 10px;
    margin-bottom: 10px;
    span {
      font-weight: 700;
    }
  }
}

.projects,
.company {
  h3 {
    font-size: 20px;
    margin-bottom: 20px;
  }
}

.skillList,
.company ul,
.projects ul {
  margin-left: 22px;
  margin-bottom: 0;
}

.skillList li {
  line-height: 1.8;
}

.contact,
.company,
.projects {
  li {
    margin-bottom: 5px;
    font-size: 16px;
  }
}

.infor-item,
.company-title,
.project-title,
.degree-title,
.tasks {
  position: relative;
}

.infor-item,
.company-title,
.project-title,
.degree-title,
.tasks {
  .delete,
  .add {
    cursor: pointer;
    opacity: 0;
    font-size: 14px;
    font-weight: 700;
    line-height: 16px;
    text-align: center;
    width: 20px;
    height: 20px;
    margin-left: 10px;
    border: 0;
    border-radius: 50%;
    background: #ccc;
    display: inline-block;
    box-sizing: border-box;
    position: absolute;
  }
}

.tasks {
  .add {
    position: absolute;
    left: -50px;
    top: 2px;
  }
  li {
    position: relative;
  }
  .delete {
    transform: rotate(45deg);
    right: 0;
    top: 0;
  }
}

.company-title,
.project-title,
.infor-item,
.tasks li {
  position: relative;
}

.degree-title,
.company-title,
.project-title {
  .delete {
    transform: rotate(45deg);
    left: -35px;
    top: 5px;
  }
}

.infor-item,
.degree-title,
.company-title,
.project-title,
.tasks {
  &:hover .add,
  &:hover .delete {
    opacity: 1;
  }
}

.degree {
  margin-bottom: 20px;
  h3 {
    font-size: 18px;
    margin-bottom: 5px;
  }
}
</style>