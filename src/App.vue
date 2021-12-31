<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-app-bar-nav-icon @click="toggleDrawer"></v-app-bar-nav-icon>
      <v-app-bar-title>来一签？</v-app-bar-title>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" app>
      <v-toolbar flat>
        <v-toolbar-title>可能被抽到的人</v-toolbar-title>
      </v-toolbar>
      <v-divider></v-divider>
      <Names :classmates="classmates" />
      <p class="text-center text-body-2">看什么看，爬去学习</p>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <Draw :classmates="classmates" />
        <!-- <v-text-field
          name="name"
          label="名字"
          v-model="inputName"
          @keyup.enter="addName()"
          outlined
        ></v-text-field> -->
        <!-- <p>{{classmates}}</p> -->
      </v-container>
      <v-footer color="primary" fixed>
        <v-row justify="center" no-gutters>
          <v-col class="primary py-4 text-center white--text" cols="12">
            <v-skeleton-loader
              v-if="!this.hitokoto"
              type="text"
            ></v-skeleton-loader>
            <p v-else>
              {{
                `${this.hitokoto.hitokoto} ——${this.hitokoto.from_who}《${this.hitokoto.from}》`
              }}
              <br>
              <v-btn class="mt-2" rounded text small color="white" @click="getHitokoto">
                <v-icon>mdi-replay</v-icon>再来一条
              </v-btn>
            </p>
            ©️Copyright {{ new Date().getFullYear() }} — <strong>RYC</strong>
          </v-col>
        </v-row>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
import Draw from "./components/Draw.vue";
import Names from "./components/Names.vue";

export default {
  name: "App",

  data: () => ({
    classmates: [
      "张博涵",
      "刘阳",
      "王慰先",
      "刘书雨",
      "丰荣珍",
      "范文博",
      "张杰",
      "周欣冉",
      "张圆",
      "白雪",
      "袁扬",
      "申琪",
      "刘睿曦",
      "李涛",
      "王浩源",
      "赵杰",
      "刘秉维",
      "王浩男",
      "乔磊",
      "刘溢华",
      "曹文蕊",
      "贾义轩",
      "李卓(大)",
      "李卓(小)",
      "杨志",
      "葛琪星",
      "景鹏宇",
      "张哲",
      "姚硕",
      "谷晓冉",
      "高乐",
      "赵冬洁",
      "吕存鑫",
      "王昊",
      "孙紫涵",
      "王硕",
      "任绪晶",
      "梁锦煜",
      "史艳涵",
      "申浩田",
      "李雨潮",
      "牟奕歌",
      "李硕",
      "李富荣",
      "刘鹏",
      "刘文慧",
      "刘洋",
      "陈雨蒙",
      "秦震南",
      "胥圣鑫",
      "饶丰",
      "高尹杰",
      "李雨宣",
      "薛巍",
      "王佳鑫",
      // "任彦成",
      "宋旭",
      "张海文",
      "贾晓成",
      "王学彬",
      "新来的女生",
    ],
    alreadyDraw: [],
    inputName: undefined,
    drawer: false,
    hitokoto: undefined,
  }),
  async created() {
    await this.getHitokoto();
  },
  methods: {
    addName() {
      this.classmates.push(this.inputName);
      this.inputName = "";
    },
    toggleDrawer() {
      this.drawer = !this.drawer;
    },
    async getHitokoto() {
      this.hitokoto = undefined;
      this.hitokoto = await this.$http.get(
        "https://international.v1.hitokoto.cn/?c=i"
      );
      this.hitokoto = this.hitokoto.data;
    },
  },
  components: {
    Draw,
    Names,
  },
};
</script>
