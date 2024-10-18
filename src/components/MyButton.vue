<template>
  <td>
    <button type="button" class="btn" :class="btnColorClass">
      {{ symbol }}
      <slot></slot>
    </button>
  </td>
</template>
<script>
export default {
  name: "MyButton",
  props: {
    btnColor: {
      type: String,
      required: true,
      default: "default",
    },
    symbol: {
      type: String,
      required: true,
      default: null,
    },
  },
  computed: {
    btnColorClass() {
      return `btn-${this.btnColor}`;
    },
  },
};
</script>
<style scoped>
.btn-primary {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.btn-primary:hover,
.btn-primary:focus {
  color: #fff;
  background-color: #0056b3;
  border-color: #004b9b;
}

.btn-secondary {
  color: #333;
  background-color: #ccc;
  border-color: #ccc;
}

.btn-secondary:hover,
.btn-secondary:focus {
  color: #333;
  background-color: #b3b3b3;
  border-color: #999999;
}

.btn-danger {
  color: #fff;
  background-color: #dc3545;
  border-color: #dc3545;
}

.btn-danger:hover,
.btn-danger:focus {
  color: #fff;
  background-color: #c82333;
  border-color: #bd2130;
}

.btn-warning {
  color: #212529;
  background-color: #ffc107;
  border-color: #ffc107;
}

.btn-warning:hover,
.btn-warning:focus {
  color: #212529;
  background-color: #e0a800;
  border-color: #d39e00;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}

.btn-default:hover,
.btn-default:focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
</style>
