<template>
  <li>
    <span class="label">
      {{ description }}
    </span>
    <div class="actions">
      <button class="btn-picto" type="button" @click="onCheck">
        <img src="@/assets/icons/checkbox-icon.svg" alt="" />
      </button>
      <button class="btn-picto" type="button">
        <img src="@/assets/icons/task-edit-icon.svg" alt="" />
      </button>
      <button class="btn-picto" type="button">
        <img src="@/assets/icons/delete-icon.svg" alt="" />
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "AppTask",
  props: {
    description: {
      type: String,
      requrired: true,
    },
  },
  methods: {
    onCheck() {
      this.$emit("check-task");
    },
    onEdit() {},
    onDelete() {},
  },
};
</script>

<style>
#todolist li {
  display: flex;
  margin: 0 -3rem 4px;
  padding: 1.1rem 3rem;
  justify-content: space-between;
  align-items: center;
  background: rgba(255, 255, 255, 0.1);
}

#todolist .actions {
  flex-shrink: 0;
  padding-left: 0.7em;
  display: flex;
  align-items: center;
  gap: 5px;
}
#todolist .label {
  position: relative;
  transition: opacity 0.2s linear;
}
#todolist .done .label {
  opacity: 0.6;
}
#todolist .done .label:before {
  content: "";
  position: absolute;
  top: 50%;
  left: -0.5rem;
  display: block;
  width: 0%;
  height: 1px;
  background: #fff;
  animation: strikeitem 0.3s ease-out 0s forwards;
}
#todolist .btn-picto {
  border: none;
  background: none;
  -webkit-appearance: none;
  cursor: pointer;
  color: #fff;
  width: 25px;
  height: 25px;
  padding: 0;
  display: flex;
  align-items: center;
}

#todolist .btn-picto img {
  border: none;
  background: none;
  -webkit-appearance: none;
  cursor: pointer;
  color: #fff;
  width: 100%;
}
</style>
