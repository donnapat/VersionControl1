<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="name"
        label="ชื่อ นามสกุล*"
        hint="กรุณากรอกชื่อ นามสกุล"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาพิมพ์ข้อมูล']"
      />
      <q-input
        filled
        type="number"
        v-model="age"
        label="อายุ *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'กรุณากรอกอายุ',
          val => val > 0 && val < 100 || 'กรุณากรอกอายุที่ถูกต้อง'
        ]"
      />
      <q-toggle v-model="accept" label="ฉันยอมรับเงื่อนไขและข้อตกลง" />
      <div>
        <q-btn label="ส่งข้อมูล" type="submit" color="primary"/>
        <q-btn label="รีเซ็ต" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)
    return {
      name,
      age,
      accept,
      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'คุณต้องยอมรับเงื่อนไขและข้อตกลงก่อน'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'ส่งข้อมูลเรียบร้อยแล้ว'
          })
        }
      },
      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>
