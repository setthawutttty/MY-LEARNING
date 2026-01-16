# install vue vite quasar
```
npm create vite@latest
```
quasar
```
npm install quasar @quasar/extras
npm install -D @quasar/vite-plugin
npm install -D sass-embedded
```

file vite.config
```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { quasar, transformAssetUrls } from '@quasar/vite-plugin'

export default defineConfig({
  plugins: [
    vue({
      template: { transformAssetUrls }
    }),
    quasar()
  ]
})

```
main.ts
```
import { createApp } from 'vue'
import { Quasar } from 'quasar'
import App from './App.vue'

import 'quasar/src/css/index.sass'
import '@quasar/extras/material-icons/material-icons.css'

createApp(App)
  .use(Quasar)
  .mount('#app')

```




# Basic Import
```
import { ref, reactive, watch, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";
import { useQuasar } from "quasar";

import http from "@/plugins/http";
import config from "@/app.config";

import DialogHeader from "@/components/DialogHeader.vue";

const $q = useQuasar();
const mixin = useCounterMixin()
const { dialogConfirm,success,showLoader,hideLoader} = mixin

const route = useRoute();
const router = useRouter();

const id = ref<string>(
  route.params.id ? route.params.id.toString() : ""
);
```
# MASK
```
mask="###,###,###,###"
reverse-fill-mask
```
# Validate Form
```

@validation-success
@submit
type="submit"

@validation-error
@reset=""
type="reset"


<q-form greedy @submit.prevent @validation-success="onSubmit">

</q-form>
```
# RULSE
- :rules="[(val:string) => !!val || `${'กรุณากรอก'}`,]"

# CSS
```
:deep(.check_box .q-checkbox) {
  align-items: start;
}
:deep(.check_box .q-checkbox .q-checkbox__inner) {
  margin-top: 2px;
}
```

# DIALOG
```
<template>
  <q-dialog v-model="modal" persistent>
    <q-card class="col-12" style="width: 80%">
      <q-form greedy @submit.prevent @validation-success="onSubmit">
        <Header
          :tittle="isEdit ? 'แก้ไขหลักเกณฑ์' : 'เพิ่มหลักเกณฑ์'"
          :close="closeDialog"
        />
        <q-separator />

        <q-card-section> </q-card-section>
        <q-separator />

        <q-card-actions align="right">
          <q-btn label="บันทึก" color="secondary" type="submit"
            ><q-tooltip>บันทึกข้อมูล</q-tooltip></q-btn
          >
        </q-card-actions>
      </q-form>
    </q-card>
  </q-dialog>
</template>
```

# PAGINATION
```
const total = ref<number>(0);
const totalList = ref<number>(1);
const pagination = ref({
  sortBy: "createdAt",
  descending: true,
  page: 1,
  rowsPerPage: 10,
});


  /${id.value}?page=${pagination.value.page}&pageSize=${pagination.value.rowsPerPage}&searchKeyword=${filterKeyword.value}

  totalList.value = Math.ceil( res.data.result.total /
  pagination.value.rowsPerPage ); total.value = res.data.result.total;

function updatePagination(newPagination: any) {
  pagination.value.page = 1;
  pagination.value.rowsPerPage = newPagination.rowsPerPage;

}

function getSearch() {
  pagination.value.page = 1;
  getList();
}

watch(
  () => pagination.value.rowsPerPage,
  async () => {
    getSearch();
  }
);

  <template v-slot:append>
    <q-icon v-if="filterKeyword == ''" name="search" />
    <q-icon
      v-if="filterKeyword !== ''"
      name="clear"
      class="cursor-pointer"
      @click="(filterKeyword = ''), getSerach()"
    />
  </template>

  <d-table
    :rows-per-page-options="[1, 25, 50, 100]"
    @update:pagination="updatePagination"
  >
    <template v-slot:pagination="scope">
      ทั้งหมด {{ total }} รายการ
      <q-pagination
        v-model="pagination.page"
        active-color="primary"
        color="dark"
        :max="Number(totalList)"
        size="sm"
        boundary-links
        direction-links
        :max-pages="5"
        @update:model-value="getList"
      ></q-pagination>
    </template>

    <div v-if="col.name == 'no'">
      {{ (pagination.page - 1) * pagination.rowsPerPage + props.rowIndex + 1 }}
    </div>
  </d-table>


```

# RENAME FILE BY LINK
```
  function downloadFile(link: string, fileName: string) { fetch(link)
  .then(response => response.blob()) .then(blob => { const url =
  window.URL.createObjectURL(blob); const a = document.createElement("a");
  a.href = url; a.download = fileName; // ชื่อไฟล์ document.body.appendChild(a);
  a.click(); window.URL.revokeObjectURL(url); document.body.removeChild(a); })
  .catch(error => console.error('ดาวน์โหลดไฟล์ได้:', error)); }
```

# DOWNLOAD FILE
```
import genReport from "@/plugins/genreport";
import genReportXLSX from '@/plugins/genreportxlsx'

const data = res.data.result;
genReport(
 data,
 `รายละเอียดบันทึกเวียนแจ้งการถึงแก่กรรม-${fullName.value}`,
 type
);
```
# xlsx
```
npm install xlsx

import * as XLSX from "xlsx";

function exportToExcel() {
  //จำลองข้อมู,
  const data = [
    { name: "John", age: 25, country: "USA" },
    { name: "Alice", age: 30, country: "UK" },
  ];
  const headers = ["ชื่อ", "อายุ", "ประเทศ"]; // หัวคอลัมน์ภาษาไทย
  const worksheet = XLSX.utils.json_to_sheet(data, {
    header: ["name", "age", "country"],
  });

  //แทรกหัวคอลัมน์ภาษาไทย (ใช้ A1, B1, C1 แทน)
  XLSX.utils.sheet_add_aoa(worksheet, [headers], { origin: "A1" });

  const workbook = XLSX.utils.book_new();
  XLSX.utils.book_append_sheet(workbook, worksheet, "ข้อมูล"); //ชื่อไฟล เเละ ชื่อ sheet
  XLSX.writeFile(workbook, "ข้อมูล.xlsx");
```
# อัพเดตค่าเเบบ reactive
```
----------
# ตัวลูก
----------
<script setup lang="ts">
import { defineProps, defineEmits, reactive, watch } from "vue";
import type { QuerySting } from "@/types"; // Import Type

const props = defineProps<{ modelValue: QuerySting }>(); // รับค่าจากพาเรนต์
const emit = defineEmits(["update:modelValue"]); // ใช้ emit เพื่ออัปเดตค่า

// ใช้ reactive เพื่อเก็บค่าของ querySting
const querySting = reactive({ ...props.modelValue });

// ใช้ watch เพื่ออัปเดตค่ากลับไปที่พาเรนต์เมื่อมีการเปลี่ยนแปลง
watch(querySting, (newValue) => {
  emit("update:modelValue", newValue);
}, { deep: true });
</script>

<template>
  <q-select
    v-model="querySting.status"
    :options="optionStatus"
    option-value="id"
    option-label="name"
    label="สถานะ"
  />
</template>
----------
# ตัวแม่
----------
<script setup lang="ts">
import { reactive } from "vue";
import ChildComponent from "./ChildComponent.vue";
import type { QuerySting } from "@/types";

const querySting = reactive<QuerySting>({
  year: "2025",
  type: "SICK",
  status: "PENDING",
  page: 1,
  pageSize: 10,
  sortBy: "dateSendLeave",
  descending: true,
  keyword: "",
  profileType: "ALL",
});
</script>

<template>
  <ChildComponent v-model="querySting" />
</template>


```

