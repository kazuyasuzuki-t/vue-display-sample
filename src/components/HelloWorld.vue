<template>
  <!-- 部署別ステータス表示タイトル -->
  <h1>部署別ステータス表示サンプル</h1>

  <!-- ステータス項目表示 -->
  <div class="status">
    <div
      class="status-children"
      v-for="(status, index) in statusItems"
      :key="index"
    >
      <div class="status-children-box" :class="status.colorClass"></div>
      <div>{{ status.text }}</div>
    </div>
  </div>

  <!-- グリッドレイアウトで表示される項目 -->
  <div class="grid-container">
    <div
      class="grid-item"
      v-for="item in items"
      :key="item.id"
      :style="{ backgroundColor: item.backgroundColor, color: textColor(item) }"
    >
      {{ item.content }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({
    items: [],
    statusItems: [
      { colorClass: 'red-box', text: 'pending' },
      { colorClass: 'blue-box', text: '発送可能' },
    ],
  }),

  created() {
    this.generateItems();
  },

  computed: {
    // ランダムな背景色を生成する関数
    randomColor() {
      return (index) => {
        const colors = ['#f1f1f1', 'red', 'blue'];
        const randomIndex = Math.floor(Math.random() * colors.length);
        return colors[randomIndex];
      };
    },
  },

  methods: {
    // 項目データを生成する関数
    generateItems() {
      const teamData = Array.from({ length: 24 }, (_, i) =>
        String.fromCharCode(65 + i).concat('部署')
      );

      for (let i = 0; i < 24; i++) {
        const item = {
          id: i,
          content: teamData[i],
          backgroundColor: this.randomColor(i),
        };
        this.items.push(item);
      }
    },
    // テキストの色を決定する関数
    textColor(item) {
      return item.backgroundColor === '#f1f1f1' ? 'black' : 'white';
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  font-weight: 400;
  margin: 32px 0;
}
.grid-container {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 10px;
  margin: 12px;
}

.grid-item {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  font-size: 14px;
  height: 120px;
  text-align: center;
}

.status {
  display: flex;
  justify-content: flex-end;
  margin-right: 12px;
}

.status-children {
  display: flex;
  align-items: center;
  padding: 0 4px;
}

.status-children-box {
  height: 20px;
  width: 20px;
  margin-right: 4px;
}

.red-box:before {
  content: '';
  background-color: red;
  display: block;
  width: 100%;
  height: 100%;
}

.blue-box:before {
  content: '';
  background-color: blue;
  display: block;
  width: 100%;
  height: 100%;
}
</style>
