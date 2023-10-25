<template>
  <q-page class="flex">
    <div class="q-pa-md">
      <q-tabs
        v-model="tab"
        inline-label
        class="bg-red text-white shadow-2"
      >
        <q-tab name="variant1" icon="" label="Вариант 1" />
        <q-tab name="variant2" icon="" label="Вариант 2" />
        <q-tab name="variant3" icon="" label="Вариант 3" />
      </q-tabs>

      <q-tab-panels v-model="tab" animated>
        <q-tab-panel name="variant1">
          <Variant1/>
        </q-tab-panel>

        <q-tab-panel name="variant2">
          <Variant2/>
        </q-tab-panel>

        <q-tab-panel name="variant3">
          <Variant3/>
        </q-tab-panel>
      </q-tab-panels>
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
    };
  },
};
</script>

<style scoped>
.q-tab-panels {
  height: 100%;
}
</style>
