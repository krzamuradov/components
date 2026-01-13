## Компонент Navbar
```
<script setup></script>

<template>
    <nav class="navbar navbar-expand-lg bg-white shadow-sm px-4 mb-3">
        <a class="navbar-brand fw-bold" href="/">
            <img src="@/assets/logo.png" alt="Logo" width="100px" />
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarContent">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <a class="nav-link active" href="#">Главная</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">О нас</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Услуги</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Контакты</a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<style scoped>
    nav {
        min-height: 100px;
    }
    .navbar-nav .nav-link {
        position: relative;
        padding: 0.5rem 1rem;
        color: #333;
        font-weight: 500;
        transition: all 0.3s ease;
    }

    .navbar-nav .nav-link::after {
        content: "";
        position: absolute;
        left: 1rem;
        bottom: 0;
        width: 0;
        height: 2px;
        background-color: #0d6efd; /* основной цвет Bootstrap */
        transition: width 0.3s ease;
    }

    .navbar-nav .nav-link:hover::after {
        width: calc(100% - 2rem); /* анимация underline */
    }

    .navbar-nav .nav-link:hover {
        color: #0d6efd;
    }

    .navbar-nav .nav-link.active {
        color: #0d6efd;
    }

    .navbar-nav .nav-link.active::after {
        width: calc(100% - 2rem);
    }
</style>
```
## Компонент Loader
```
<script setup></script>

<template>
    <div class="d-flex justify-content-center align-items-center position-absolute top-0 start-0 vh-100 w-100 bg-white z-3">
        <img src="@/assets/logo.png" alt="Logo" width="150" class="animated-logo" />
    </div>
</template>

<style scoped>
    .animated-logo {
        animation: pulse 0.9s infinite ease-in-out;
    }

    @keyframes pulse {
        0%,
        100% {
            transform: scale(0.8);
        }
        50% {
            transform: scale(1.1);
        }
    }
</style>
```
## Компонент Select
```
<script setup>
    const props = defineProps({
        type: { type: String, default: "text" },
        name: { type: String, required: true },
        label: { type: String, required: true },
        is_invalid: { type: String, default: "" },
        is_required: { type: Boolean, default: true },
    });

    const model = defineModel();
</script>

<template>
    <div class="position-relative">
        <select :name="props.name" :id="props.name" class="form-select" v-model="model" :class="{ 'is-invalid': props.is_invalid }" v-bind="$attrs">
            <slot></slot>
        </select>
        <label :for="props.name" class="position-absolute top-0 start-0 translate-middle-y bg-white px-1 ms-3 small text-secondary rounded-0">
            {{ props.label }}
            <span v-if="props.is_required" class="text-danger">*</span>
        </label>
        <div class="invalid-feedback" v-if="props.is_invalid">{{ props.is_invalid }}</div>
    </div>
</template>

<style scoped>
    select {
        height: 3rem;
    }
    select:focus {
        border-color: #417cd4 !important; /* или любой другой */
        box-shadow: 0 0 3px rgb(50, 83, 231); /* стандарт bootstrap */
    }

    select:-webkit-autofill {
        box-shadow: 0 0 0px 1000px white inset !important;
        -webkit-box-shadow: 0 0 0px 1000px white inset !important;
        -webkit-text-fill-color: #000 !important;
    }

    .is-invalid {
        box-shadow: none !important;
    }
</style>
```
## Компонент Input
```
<script setup>
    const props = defineProps({
        type: { type: String, default: "text" },
        name: { type: String, required: true },
        label: { type: String, required: true },
        is_invalid: { type: String, default: "" },
    });

    const model = defineModel();
</script>

<template>
    <div class="position-relative">
        <input :type="props.type" :name="props.name" :id="props.name" class="form-control" v-model="model" :class="{ 'is-invalid': props.is_invalid }" v-bind="$attrs" />
        <label :for="props.name" class="position-absolute top-0 start-0 translate-middle-y bg-white px-1 ms-3 small text-secondary rounded-0">{{ props.label }}</label>
        <div class="invalid-feedback" v-if="props.is_invalid">{{ props.is_invalid }}</div>
    </div>
</template>

<style scoped>
    input {
        height: 3rem;
    }
    input:focus {
        border-color: #0d6efd !important; /* или любой другой */
        box-shadow: 0 0 3px rgb(50, 83, 231); /* стандарт bootstrap */
    }

    input:-webkit-autofill {
        box-shadow: 0 0 0px 1000px white inset !important;
        -webkit-box-shadow: 0 0 0px 1000px white inset !important;
        -webkit-text-fill-color: #000 !important;
    }

    .is-invalid {
        box-shadow: none !important;
    }
</style>

```
## Компонент CARD
```
<script setup></script>

<template>
    <div class="card-root shadow-sm p-2 rounded-3 mb-1" v-bind="$attrs">
        <slot />
    </div>
</template>

<style scoped>
    /* .card-root {
        transition:
            transform 0.2s ease,
            box-shadow 0.2s ease;
        cursor: pointer;
    }

    .card-root:hover {
        transform: translateY(-4px);
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.12);
    } */
</style>
```
## Компонент pdf-vue3
```
<script setup>
    import PDF from "pdf-vue3";
    import { useRoute, useRouter } from "vue-router";

    const route = useRoute();
    const router = useRouter();
    const url = route.query.url;
    console.log(url);

    const props = defineProps({
        url: { type: String },
    });
</script>

<template>
    <div class="container mt-4">
        <button @click="router.back()" class="btn btn-outline-secondary mb-3"><i class="fa fa-reply"></i> Hujjatlar ro'yxatiga qaytish</button>
        <PDF :src="url" pdfWidth="70%" scrollThreshold="10" />
    </div>
</template>

```

## Компонент DOCX-VIEWER
```
<script setup>
    import { ref, onMounted } from "vue";
    import { renderAsync } from "docx-preview";
    import { useRoute, useRouter } from "vue-router";

    const route = useRoute();
    const router = useRouter();
    console.log(route);

    const url = route.query.url;

    const container = ref(null);
    const styleContainer = ref(null);

    async function loadAndRenderDocx() {
        if (!container.value || !(container.value instanceof HTMLElement)) {
            console.error("container.value не HTMLElement");
            return;
        }
        if (!styleContainer.value || !(styleContainer.value instanceof HTMLElement)) {
            console.error("styleContainer.value не HTMLElement");
            return;
        }

        try {
            const response = await fetch(url);
            if (!response.ok) throw new Error(`Ошибка загрузки: ${response.statusText}`);

            const arrayBuffer = await response.arrayBuffer();

            container.value.textContent = "";

            await renderAsync(arrayBuffer, container.value, styleContainer.value, {
                className: "docx-preview",
                inWrapper: false,
                experimental: true,
                ignoreWidth: true,
                ignoreHeight: true,
                renderChanges: true,
                renderAltChunks: true,
            });
        } catch (e) {
            console.error("Ошибка при рендеринге DOCX:", e);
        }
    }

    onMounted(() => {
        loadAndRenderDocx();
    });
</script>

<template>
    <button @click="router.back()" class="btn btn-outline-secondary mb-3"><i class="fa fa-reply"></i> Hujjatlar ro'yxatiga qaytish</button>
    <div class="d-flex justify-content-center align-items-center">
        <div ref="styleContainer" style="width: 0; height: 0; overflow: hidden; position: absolute; left: -9999px"></div>

        <div ref="container"></div>
    </div>
</template>

<style scoped>
    .docx-container .docx-preview {
        background-color: none !important;
        font-family: Arial, sans-serif;
        line-height: 1.5;
    }
    .docx-container [style*="background"] {
        background-color: white !important;
    }
</style>

```


## Компонент c прокруткой только в центре
```
<script setup>
import Card from "@/components/card.vue";
</script>

<template>
  <div class="layout">
    <!-- HEADER -->
    <div class="section">
      <Card>
        <h1>HEADER</h1>
      </Card>
    </div>

    <!-- CENTER (scroll) -->
    <div class="center">
      <Card v-for="i in 20" :key="i" class="mb-2">
        <h1>CENTER {{ i }}</h1>
      </Card>
    </div>

    <!-- FOOTER -->
    <div class="section">
      <Card>
        <h1>FOOTER</h1>
      </Card>
    </div>
  </div>
</template>

<style scoped>
.layout {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

/* header и footer */
.section {
  flex-shrink: 0;
}

/* центр */
.center {
  flex: 1;
  overflow-y: auto;
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
}
</style>


```

## Настройки @media в css
```
/* ================= DESKTOP / Экран больше 1200px ================= */
@media (min-width: 1201px) {}

/* ================= LAPTOP / Экран 1200px и меньше ================= */
@media (max-width: 1200px) {}

/* ================= TABLET / Экран 900px и меньше ================= */
@media (max-width: 900px) {}

/* ================= MOBILE (L) / Экран 768px и меньше ================= */
@media (max-width: 768px) {}

/* ================= MOBILE (S) / Экран 480px и меньше ================= */
@media (max-width: 480px) {}

```

