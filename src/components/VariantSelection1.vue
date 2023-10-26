<template>
  <div class="q-gutter-md row">
    <q-select
      filled
      v-model="formatModel"
      use-input
      input-debounce="0"
      label="Формат"
      :options="formatOptions"
      style="width: 250px"
      behavior="menu"
    >
      <template v-slot:no-option>
        <q-item>
          <q-item-section class="text-grey">
            No results
          </q-item-section>
        </q-item>
      </template>
    </q-select>

    <q-select
      filled
      v-model="filialModel"
      use-input
      input-debounce="0"
      label="Филиал"
      :options="filialOptions"
      :disable="!formatModel"
      @filter="filterFilial"
      style="width: 250px"
      behavior="menu"
    >
      <template v-slot:no-option>
        <q-item>
          <q-item-section class="text-grey">
            No results
          </q-item-section>
        </q-item>
      </template>
    </q-select>
    <div class="to-selector">
      <q-select
        filled
        label="ТО"
        v-model="model2"
        use-input
        use-chips
        multiple
        @new-value="createValue"
        :disable="!filialModel"
        :options="TOoptions"
        @filter="filterTO"
        @update:model-value="addTO(model2)"
        style="width: 300px; height: 50px;"
        behavior="dialog"
      />
    </div>
  </div>
</template>

<script>
import { reactive, ref } from 'vue';
import { format, to, filial } from 'src/mock';

export default {
  name: 'VariantSelection1',
  setup() {
    const formatOptions = ref(format);
    const TOoptions = ref(to);
    const filialOptions = ref(filial);
    const formatModel = ref(null);
    const filialModel = ref(null);
    const model2 = ref(null);
    const visibleSelectTO = ref(true);
    const selectedTO = reactive([]);

    return {
      formatModel,
      filialModel,
      model2,
      to,
      formatOptions,
      filialOptions,
      TOoptions,
      multiple: ref(null),
      visibleSelectTO,
      selectedTO,

      createValue(val, done) {
        if (val.length > 0) {
          const modelValue = (model2.value || []).slice();

          val.split(/[,;|]+/).map((v) => v.trim()).filter((v) => v.length > 0).forEach((v) => {
            if (to.includes(v) === false) {
              to.push(v);
            }
            if (modelValue.includes(v) === false) {
              modelValue.push(v);
            }
          });

          done(null);
          model2.value = modelValue;
        }
      },
      filterFilial(val, update) {
        if (val === '') {
          update(() => {
            filialOptions.value = filial;
          });
          return;
        }

        if (val.length >= 3) {
          update(() => {
            const needle = val.toLowerCase();
            filialOptions.value = filial.filter((v) => v.toLowerCase().indexOf(needle) > -1);
          });
        }
      },
      filterTO(val, update) {
        if (val === '') {
          update(() => {
            TOoptions.value = to;
          });
          return;
        }
        if (val.length >= 2) {
          update(() => {
            const needle = val.toLowerCase();
            TOoptions.value = to.filter((v) => v.toLowerCase().indexOf(needle) > -1);
          });
        }
      },

      addTO(val) {
        selectedTO.push({
          index: selectedTO.length + 1,
          name: val.split('-')[0],
          code: val.split('-')[1],
          filial: filialModel,
          status: 'Функционирует',
        });
        model2.value = '';
      },
    };
  },
};
</script>
<style scoped>
.to-selector {
  height: 55px !important;
}

.to-selector label {
  overflow: auto;
}

.q-field__control-container.col.relative-position.row.no-wrap.q-anchor--skip,
.to-selector .q-field__native.row.items-center {
  height: 55px !important;
}

</style>
