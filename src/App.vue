<template>
  <div>
    <!-- ヘッダー -->
    <header class="bg-danger p-4 mb-4 shadow">
      <h1 class="text-white">楽天イーグルス考察アプリ</h1>
    </header>

    <!-- フォーム -->
    <form @submit.prevent="addPlayerToBench" class="mb-4">
      <div class="input-group">
        <input type="text" v-model="newPlayer" class="form-control" placeholder="選手名を入力してください" required>
        <button type="submit" class="btn btn-primary">追加</button>
      </div>
    </form>


    <!-- テーブル -->
    <div class="d-flex justify-content-center">
      <!-- スタメン -->
      <ul class="list-group mr-3">
        <li class="list-group-item bg-secondary text-white">スタメン</li>
        <draggable v-model="startingLineup" item-key="id" tag="li" group="players" @start="onDragStart">
          <template #item="{ element, index }">
            <li class="list-group-item d-flex justify-content-between align-items-center" style="border: 1px solid transparent; border-radius: .5rem; box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); background-color: #dc3545;">
              <div class="banner-red text-center" style="width: 2.5rem; color: white;">{{ index + 1 }}</div>
              <div class="text-white">{{ element }}</div>
            </li>
          </template>
        </draggable>
      </ul>

      <!-- ベンチ -->
      <ul class="list-group">
        <li class="list-group-item bg-secondary text-white">ベンチ</li>
        <draggable v-model="bench" item-key="id" tag="li" group="players">
          <template #item="{ element }">
            <li class="list-group-item d-flex justify-content-end align-items-center" style="border: 1px solid transparent; border-radius: .5rem; box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); background-color: #dc3545;">
              <div class="text-white">{{ element }}</div>
            </li>
          </template>
        </draggable>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import draggable from 'vuedraggable';

export default {
  components: {
    draggable,
  },
  setup() {
    const startingLineup = ref(['小郷', '村林', '浅村', '島内', '阿部', '鈴木大', '辰己', '太田', '小深田']);
    const bench = ref(['石原', '田中貴', '山田', '茂木', '伊藤裕', '岡島', '田中和']);
    const newPlayer = ref('');

    const addPlayerToBench = () => {
      if (newPlayer.value.trim() !== '') {
        const player = newPlayer.value.trim();
        bench.value.push(player);
        newPlayer.value = '';
      }
    };

    const onDragStart = (event) => {
      const index = event.oldIndex;
    };

    return {
      startingLineup,
      bench,
      newPlayer,
      addPlayerToBench,
      onDragStart,
    };
  },
};
</script>


<style>
.banner-black {
  background-color: #000000;
  color: white;
}
</style>
