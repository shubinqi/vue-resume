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
      class="infomation card"
      v-if="card.info === 2"
    >
      <h2 class="card-title">
        <span contenteditable>个人信息</span>
        <button
          class="add"
          @click="handleAdd({
            name: 'infoList'
          })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: 'info',
            num: 0
          })"
        >+</button>
      </h2>
      <div class="infoList">
        <div
          class="infor-item"
          @dragenter="dragenter($event, index)"
          @dragover="dragover($event, index)"
          @dragstart="dragstart(index)"
          draggable
          v-for="(item, index) in infoList"
          :key="item.index"
        >
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
    </div>
    <!-- 个人信息 -->
    <div
      class="infomation card"
      v-if="card.ssss === 2"
    >
      <h2 class="card-title"><span contenteditable>专业技能</span><button
          class="delete"
          @click="handleDelete({
            card: 'ssss',
            num: 0
          })"
        >+</button></h2>
      <ul class="skillList tasks">
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
    </div>
    <!-- 自我评价 -->
    <div
      class="summary card"
      v-if="card.summary === 2"
    >
      <h2 class="card-title"><span contenteditable>自我评价</span><button
          class="delete"
          @click="handleDelete({
            card: 'summary',
            num: 0
          })"
        >+</button></h2>
      <p
        contenteditable
        v-text="summary"
      ></p>
    </div>
    <!-- 工作经历 -->
    <div
      class="company-card card"
      v-if="card.company === 2"
    >
      <h2 class="card-title">
        <span contenteditable>工作经历</span>
        <button
          class="add"
          @click="handleAdd({
            name: 'companyList'
          })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: 'company',
            num: 0
          })"
        >+</button>
      </h2>
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
      class="experience card"
      v-if="card.experience === 2"
    >
      <h2 class="card-title">
        <span contenteditable>项目经历</span>
        <button
          class="add"
          @click="handleAdd({
            name: 'experienceList'
          })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: 'experience',
            num: 0
          })"
        >+</button>
      </h2>
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
        <p contenteditable><span contenteditable>项目简介：</span>负责XXX\XXX\XXX的开发</p>
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
      class="education card"
      v-if="card.education === 2"
    >
      <h2 class="card-title">
        <span contenteditable>教育经历</span>
        <button
          class="add"
          @click="handleAdd({
            name: 'educationList'
          })"
        >+</button>
        <button
          class="delete"
          @click="handleDelete({
            card: 'education',
            num: 0
          })"
        >+</button>
      </h2>
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
    <template slot="a">123</template>
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
      summary: '掌握Web前端开发基本技能，熟悉W3C标准、页面布局架构、前端语义化、浏览器兼容性等，懂些审美，擅长设计，重视用户体验与代码可维护性，有近2年的前端开发经验。',
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
        name: 'educationList'
      })
    },
    // 拖拽个人信息顺序
    dragstart (index) {
      this.dragIndex = index;
    },
    // 拖拽个人信息顺序
    dragenter (e, index) {
      e.preventDefault();
      // 避免源对象触发自身的dragenter事件
      if (this.dragIndex !== index) {
        const source = this.infoList[this.dragIndex];
        this.infoList.splice(this.dragIndex, 1);
        this.infoList.splice(index, 0, source);
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
            "Built and maintained web applications using Vue.js",
            "Collaborated with back-end developers to integrate APIs",
            "Collaborated with back-end developers to integrate APIs"
          ],
        },
        experienceList: {
          title: "后台管理系统项目",
          company: "前端开发工程师",
          date: "2022.09-2022.12",
          tasks: [
            "Built and maintained web applications using Vue.js",
            "Collaborated with back-end developers to integrate APIs",
            "Collaborated with back-end developers to integrate APIs"
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

<style scoped>
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

.card-title span {
  color: #333;
  padding: 5px 12px;
  border-left: 4px solid #333;
}

.card-title .add {
  opacity: 0;
  font-size: 20px;
  font-weight: 700;
  border-radius: 50%;
  cursor: pointer;
  margin-right: 5px;
}

.card-title .delete {
  opacity: 0;
  font-size: 20px;
  font-weight: 700;
  border-radius: 50%;
  transform: rotate(45deg);
  cursor: pointer;
  margin-right: 5px;
}

.card-title:hover .add,
.card-title:hover .delete {
  opacity: 1;
}

.company-title,
.project-title,
.degree-title {
  display: flex;
  justify-content: space-between;
}

.name {
  margin-right: 20px;
}

.name h1 {
  font-size: 36px;
  margin-bottom: 15px;
}

.name h3 {
  font-size: 22px;
  margin-bottom: 5px;
}

.name p {
  font-size: 18px;
}

.contact {
  flex: 1;
}

ul {
  list-style: auto;
  margin: 0;
  padding: 0;
}

.image {
  position: absolute;
  top: 10px;
  right: 20px;
  width: 100px;
  height: 140px;
}

.image input {
  opacity: 0;
  width: 120px;
}

.image:hover input {
  opacity: 1;
}

.image img {
  position: absolute;
  top: 0;
  left: 0;
  width: 120px;
  height: 180px;
}

.infoList {
  display: flex;
  flex-wrap: wrap;
}

.infoList .infor-item {
  cursor: move;
  width: 33.333%;
}

.infoList .infor-item:hover {
  color: skyblue;
  background: #f5f7f9;
}

.infoList .infor-item span {
  cursor: auto;
}

.infor-item span {
  line-height: 2.5;
}

.summary p {
  font-size: 16px;
  margin: 0;
}

.summary h2,
.experience h2,
.education h2 {
  font-size: 24px;
  margin-bottom: 20px;
}

.projects h3,
.company h3 {
  font-size: 20px;
  margin-bottom: 20px;
}

.projects p {
  font-size: 16px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.projects p span {
  font-weight: 700;
}

.skillList,
.company ul,
.projects ul {
  margin-left: 20px;
  margin-bottom: 0;
}

.skillList li {
  line-height: 1.8;
}

.contact li,
.company li,
.projects li {
  margin-bottom: 5px;
  font-size: 16px;
}

.infor-item,
.company-title,
.project-title,
.degree-title,
.tasks {
  position: relative;
}

.infor-item .delete,
.company-title .delete,
.project-title .delete,
.degree-title .delete,
.tasks .delete,
.tasks .add {
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

.tasks .add {
  position: absolute;
  left: -50px;
  top: 2px;
}

.tasks li {
  position: relative;
}

.tasks .delete {
  transform: rotate(45deg);
  right: 0;
  top: 0;
}

.infor-item .delete {
  transform: rotate(45deg);
  right: 6px;
  top: 9px;
}

.degree-title .delete,
.company-title .delete,
.project-title .delete {
  transform: rotate(45deg);
  left: -35px;
  top: 2px;
}

.infor-item:hover .delete,
.degree-title:hover .delete,
.company-title:hover .delete,
.project-title:hover .delete,
.tasks:hover .add,
.tasks:hover .delete {
  opacity: 1;
}

.degree {
  margin-bottom: 20px;
}

.degree h3 {
  font-size: 18px;
  margin-bottom: 5px;
}
</style>