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
