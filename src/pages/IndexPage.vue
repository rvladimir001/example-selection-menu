<template>
  <q-page class="flex">
    <div class="q-pa-md">
      <div class="q-gutter-md row">
        <q-btn color="red" @click="variant1=true">Вариант 1</q-btn>
        <q-btn color="red" @click="variant2=true">Вариант 2</q-btn>
        <q-btn color="red" @click="variant3=true">Вариант 3</q-btn>
      </div>

      <q-dialog v-model="variant1">
        <q-card style="width: 1000px; max-width: 80vw;">
          <q-card-section class="column no-wrap flex-center">
            <Variant1/>
          </q-card-section>
          <q-card-actions align="center">
            <q-btn flat label="Отмена" color="primary" v-close-popup />
            <q-btn flat label="Принять" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-dialog v-model="variant2">
        <q-card style="width: 1000px; max-width: 80vw;">
          <q-card-section class="column no-wrap flex-center">
            <Variant2/>
          </q-card-section>
          <q-card-actions align="center">
            <q-btn flat label="Отмена" color="primary" v-close-popup />
            <q-btn flat label="Принять" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-dialog v-model="variant3">
        <q-card style="width: 1200px; max-width: 80vw;">
          <q-card-section style="height: 200px">
            <Variant3/>
          </q-card-section>
          <q-card-actions align="center">
            <q-btn flat label="Отмена" color="primary" v-close-popup />
            <q-btn flat label="Принять" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>
      </div>
  </q-page>
</template>

<script>
import { ref } from 'vue';
import Variant1 from 'components/VariantSelection1.vue';
import Variant2 from 'components/VariantSelection2.vue';
import Variant3 from 'components/VariantSelection3.vue';

export default {
  name: 'IndexPage',
  components: { Variant1, Variant2, Variant3 },
  setup() {
    return {
      tab: ref('variant1'),
      variant1: ref(false),
      variant2: ref(false),
      variant3: ref(false),
    };
  },
};
</script>

<style scoped>
.q-tab-panels {
  height: 100%;
}
</style>
