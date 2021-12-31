<template>
  <div>
    <v-row
      class="text-center"
      justify="center"
      align="center"
      style="height: 70vh"
    >
      <v-col cols="6">
        <v-dialog v-model="dialog" width="500">
          <v-card>
            <v-toolbar color="primary" elevation="1" dark>
              <v-toolbar-title>恭喜🎉</v-toolbar-title>
            </v-toolbar>
            <v-scale-transition>
              <div
                class="text-center text-h1 text-primary py-5"
                v-show="dialog"
                v-if="current"
              >
                {{ current }}
              </div>
            </v-scale-transition>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="toggleDialog"> 关闭 </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-card class="pa-5" shaped>
          <div class="text-h4 mb-4">今天的幸运儿是谁呢？</div>
          <v-btn color="primary" outlined @click="draw"> 抽！ </v-btn>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    current: undefined,
  }),
  methods: {
    toggleDialog() {
      this.dialog = !this.dialog;
    },
    draw() {
      this.toggleDialog();
      this.current =
        this.classmates[
          Math.round(Math.random() * (this.classmates.length - 1))
        ];
      console.log(this.current);
    },
  },
  props: {
    classmates: {
      required: true,
    },
  },
};
</script>

<style scoped>
</style>