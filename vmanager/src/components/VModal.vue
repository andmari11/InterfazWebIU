<script setup>
import { onMounted, ref } from "vue";
import { Modal } from "bootstrap";
defineProps({
  id: {
    type: String
  },
  title: {
    type: String,
    default: "<<Title goes here>>",
  },
});
let modalElement = ref(null);
let thisModalObj = null;

onMounted(() => {
  thisModalObj = new Modal(modalElement.value);
});
function _show() {
  thisModalObj.show();
}
function _hide() {
  thisModalObj.hide();
}
defineExpose({ show: _show, hide: _hide });
</script>

<template>
  <div class="modal fade" :id="id" tabindex="-1" aria-labelledby=""
    aria-hidden="true" ref="modalElement">
    <div class="modal-dialog modal-xl">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" :id="`${id}Label`">{{ title }}</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <slot name="body"></slot>
        </div>
        <div class="modal-footer">
          <slot name="footer"></slot>
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
