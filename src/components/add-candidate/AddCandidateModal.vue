<template></template>

<script setup>
import { defineProps, defineEmits, reactive } from 'vue'
import UploadCV from './UploadCV.vue'
import CandidateForm from './CandidateForm.vue'

//  Định nghĩa một props cha truyền xuống
const props = defineProps({
  isOpen: Boolean,
})

// Định nghĩa emit
const emit = defineEmits(['close', 'save'])

const formData = reactive({
  name: '',
  birthday: '',
  gender: '',
  phone: '',
  email: '',
  address: '',
  education: [],
  experience: [],
  file: null,
})

const handleFile = (file) => {
  formData.file = file
}

const close = () => emit('close')

const save = () => {
  emit('save', { ...formData })
}
</script>

<style scoped></style>
