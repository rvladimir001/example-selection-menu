<template>
  <q-page class="flex">
    <div class="q-pa-md">
      <div class="q-gutter-md row">
        <q-btn color="red" @click="variant1=true">Вариант 1</q-btn>
        <q-btn color="red" @click="variant2=true">Вариант 2</q-btn>
        <q-btn color="red" @click="variant3=true">Вариант 3</q-btn>
        <q-btn color="red" @click="variant4=true">Вариант 4</q-btn>
        <q-btn color="red" @click="variant5=true">Вариант 5</q-btn>
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
          <q-card-section>
            <Variant3/>
          </q-card-section>
          <q-card-actions align="center">
            <q-btn flat label="Отмена" color="primary" v-close-popup />
            <q-btn flat label="Принять" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-dialog v-model="variant4">
        <q-card style="width: 800px; max-width: 80vw;">
          <q-card-section>
            <Variant4/>
          </q-card-section>
          <q-card-actions align="center">
            <q-btn flat label="Отмена" color="primary" v-close-popup />
            <q-btn flat label="Принять" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-dialog v-model="variant5">
        <q-card style="width: 800px; max-width: 80vw;">
          <q-card-section>
            <Variant5/>
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
import Variant4 from 'components/VariantSelection4.vue';
import Variant5 from 'components/VariantSelection5.vue';

export default {
  name: 'IndexPage',
  components: {
    Variant1,
    Variant2,
    Variant3,
    Variant4,
    Variant5,
  },
  setup() {
    return {
      variant1: ref(false),
      variant2: ref(false),
      variant3: ref(false),
      variant4: ref(false),
      variant5: ref(false),
    };
  },
};
</script>

<style scoped>
.q-tab-panels {
  height: 100%;
}
</style>
