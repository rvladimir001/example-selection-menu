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

          <q-select
            filled
            label="ТО"
            v-model="model2"
            use-input
            multiple
            @new-value="createValue"
            :disable="!filialModel"
            :options="TOoptions"
            @filter="filterTO"
            @update:model-value="addTO(model2)"
            style="width: 300px; height: 50px;"
          />

              <q-list
                bordered
                class="rounded-borders"
                style="width: 300px; max-height: 150px; overflow: auto">
                <q-item-label header>Выбранные ТО</q-item-label>
                <q-item v-for="to in selectedTO" :key="to">
                  <q-item-section top>
                    <q-item-label lines="1">
                      <span>{{to.name}}</span>
                    </q-item-label>
                  </q-item-section>
                  <q-item-section top side>
                    <div class="text-grey-8 q-gutter-xs">
                      <q-btn
                        class="gt-xs"
                        size="12px"
                        flat
                        dense
                        round
                        icon="delete"
                        @click="removeTO(to)"/>
                    </div>
                  </q-item-section>
                </q-item>
                </q-list>
            </div>
</template>

<script>
import { ref, reactive } from 'vue';
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
      selectedTO,
      addTO(val) {
        selectedTO.push({
          index: selectedTO.length + 1,
          name: val[0].split('-')[0],
          code: val[0].split('-')[1],
          filial: filialModel,
          status: 'Функционирует',
        });
        delete TOoptions.value[TOoptions.value.indexOf(val[0])];
        model2.value = [];
      },
      removeTO(val) {
        // delete selectedTO[selectedTO.indexOf(val)];
        // selectedTO.find((tempTO) => tempTO.index === val.index);
        console.log('result', selectedTO.indexOf(val));
        delete selectedTO[selectedTO.indexOf(val)];
        console.log('result', selectedTO);
      },
      pagination: ref({
        rowsPerPage: 0,
      }),

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
