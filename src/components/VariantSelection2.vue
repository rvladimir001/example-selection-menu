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
              input-debounce="0"
              @new-value="createValue"
              :disable="!filialModel"
              :options="TOoptions"
              options-cover
              stack-label
              @filter="filterTO"
              @click="scaleChange"
              style="width: 500px; max-height: 70px;"
            />
          </div>
        </div>
</template>

<script>
import { ref } from 'vue';

const format = [
  'ММ', 'МК', 'ГМ', 'МА',
];
const filial = [
  'Краснодар', 'Краснодар Запад', 'Краснодар Восток', 'Ростов-на-Дону', 'Ростов-на-Дону Север', 'Волгоград',
];

const to = [
  'Торговвый объект 1 - 01380',
  'Торговвый объект 2 - 02380',
  'Торговвый объект 3 - 03380',
  'Торговвый объект 4 - 04380',
  'Торговвый объект 5 - 05380',
  'Торговвый объект 6 - 06380',
  'Торговвый объект 7 - 07380',
  'Торговвый объект 8 - 08380',
  'Торговвый объект 9 - 09380',
  'Торговвый объект 10 - 10380',
  'Торговвый объект 11 - 11380',
  'Торговвый объект 12 - 12380',
  'Торговвый объект 13 - 13380',
  'Торговвый объект 14 - 14380',
  'Торговвый объект 15 - 15380',
  'Торговвый объект 16 - 16380',
  'Торговвый объект 17 - 17380',
  'Торговвый объект 18 - 18380',
  'Торговвый объект 19 - 19380',
  'Торговвый объект 20 - 20380',
];

export default {
  name: 'VariantSelection2',
  setup() {
    const formatOptions = ref(format);
    const TOoptions = ref(to);
    const filialOptions = ref(filial);
    const formatModel = ref(null);
    const filialModel = ref(null);
    const model2 = ref(null);

    return {
      formatModel,
      filialModel,
      model2,
      to,
      formatOptions,
      filialOptions,
      TOoptions,
      multiple: ref(null),

      scaleChange() {
        document.querySelector('.to-selector .q-field__native.row.items-center').style.height = '50px';
      },

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
    };
  },
};
</script>

<style scoped>
.to-selector {
  height: 50px !important;
}
.to-selector label {
  overflow: auto;
}
.q-field__control-container.col.relative-position.row.no-wrap.q-anchor--skip,
.to-selector .q-field__native.row.items-center {
  height: 50px !important;
}

</style>
