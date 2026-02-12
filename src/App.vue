<script setup>
import SideBar from "./components/SideBar.vue";
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import CheckBox from "./components/CheckBox.vue";
import Input from "./components/Input.vue";
import { reactive } from "vue";

const form = reactive({
  email: "",
  password: "",
  phone: "",
  userType: [],
});

const errors = reactive({
  email: "",
  password: "",
  phone: "",
  userType: "",
});

function validateForm() {
  errors.email = /\S+@\S+\.\S+/.test(form.email.trim()) ? "" : "Email inválido";
  errors.password =
    form.password.length >= 8 ? "" : "Palavra-passe com mínimo de 8 caracteres";

  const phone = form.phone.trim();

  if (!phone) {
    errors.phone = "Telefone obrigatório";
  } else if (!/^\d+$/.test(phone)) {
    errors.phone = "Telefone deve conter apenas números";
  } else if (phone.length !== 9) {
    errors.phone = "Telefone deve ter 9 dígitos";
  } else {
    errors.phone = "";
  }

  errors.userType =
    form.userType.length > 0 ? "" : "Selecione pelo menos um tipo de utilizador";

  return !errors.email && !errors.password && !errors.phone && !errors.userType;
}

function handleSubmit() {
  if (!validateForm()) return;

  const payload = {
    ...form,
    phone: `+351${form.phone.replace(/\D/g, "")}`,
  };

  console.log(payload);
  alert("Formulário enviado" + JSON.stringify(payload));
  resetForm();
}

function resetForm() {
  form.email = "";
  form.password = "";
  form.phone = "";
  form.userType = [];

  errors.email = "";
  errors.password = "";
  errors.phone = "";
  errors.userType = "";
}

</script>

<template>
  <div class="layout">
    <header class="topbar">
      <img src="@/assets/images/LOGO-WDR.png" alt="WebDev" class="logo" />
    </header>

    <div class="content-wrapper">
      <SideBar />
      <main class="main">
        <section class="section">
          <div class="section-header">
            <h1>Utilizador</h1>
          </div>
          <form @submit.prevent="handleSubmit">
            <div class="card-container">
              <Card title="Tipo de utilizador">
                <CheckBox v-model="form.userType" :options="['Project Manager', 'Developer', 'Architect']"
                  @change="errors.userType" />
                <p v-if="errors.userType" class="inline-error">{{ errors.userType }}</p>
              </Card>

              <Card title="Contacto">
                <Input type="email" label="Email" name="email" id="email" v-model="form.email" :error="errors.email"
                  @blur="validateForm" @input="validateForm" />
                <Input type="password" label="Palavra-passe" name="password" id="password" v-model="form.password"
                  :error="errors.password" @input="validateForm" @blur="validateForm" />
                <Input type="tel" label="Telefone" name="telefone" id="telefone" prefix="+351" v-model="form.phone"
                  :error="errors.phone" @input="validateForm" @blur="validateForm" />
              </Card>
            </div>

            <div class="actions">
              <Button type="button" class="btn-secondary" @click="resetForm"> Cancelar </Button>
              <Button type="submit" class="btn-primary"> GUARDAR </Button>
            </div>
          </form>
        </section>
      </main>
    </div>
  </div>
</template>

<style scoped>
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #f3f6f7;
}

.topbar {
  height: 56px;
  background-color: #ffffff;
  display: flex;
  align-items: center;
  padding: 0 1rem;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.05);
}

.logo {
  height: 32px;
}

.content-wrapper {
  display: flex;
  flex: 1;
}

.main {
  flex: 1;
  background-color: #f3f6f7;
  padding: 2rem 3rem;
}

.section {
  display: flex;
  flex: 1;
  flex-direction: column;
  gap: 1.5rem;
  width: 100%;
}

.section-header {
  margin-bottom: 2rem;
}

.section-header h1 {
  font-size: 2rem;
  font-weight: 600;
  color: #0b1b3b;
}

.card-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.actions {
  display: flex;
  justify-content: flex-end;
  gap: 1.5rem;
  margin-top: 2rem;
}

.inline-error {
  margin-top: 0.5rem;
  color: #ef4444;
  font-size: 0.8rem;
  font-weight: 500;
}

.btn-primary {
  background-color: #1da1c9;
  color: #ffffff;
  font-weight: bold;
}

.btn-secondary {
  background-color: #ffffff;
  color: #0b1b3b;
  font-weight: bold;
}
</style>
