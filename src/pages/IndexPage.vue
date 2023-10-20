<template>
  <q-page class="flex">
    <div class="q-pa-md">
        <div class="q-gutter-md row">

          <q-select
            filled
            v-model="formatModel"
            use-input
            input-debounce="0"
            label="Формат"
            :options="formatOptions"
            @filter="filterFn"
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
            @filter="filterFn"
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
            label="ТО"
            v-model="model2"
            use-input
            use-chips
            multiple
            input-debounce="0"
            @new-value="createValue"
            :disable="!filialModel"
            :options="TOoptions"
            @filter="filterFn"
            style="width: 500px"
          />
        </div>
      </div>
  </q-page>
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
  name: 'IndexPage',
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

      // selectedObject(val) {
      //   console.log('val', val);
      // },
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
      filterFn(val, update) {
        if (val === '') {
          update(() => {
            TOoptions.value = to;
          });
          return;
        }

        update(() => {
          const needle = val.toLowerCase();
          TOoptions.value = to.filter((v) => v.toLowerCase().indexOf(needle) > -1);
        });
      },
    };
  },
};
</script>
