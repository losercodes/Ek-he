<template>
  <div class="h-screen grid grid-cols-3 divide-x">
    <!-- Left section for the form input and preview buttons -->
    <div class="col-span-2 h-screen flex flex-col bg-gradient-to-b from-slate-100 to-slate-200">
      <div class="flex-1 overflow-y-auto p-8">
        <!-- Profile form component -->
        <app-form-profile
          v-model:name="data.n"
          v-model:desc="data.d"
          v-model:image="data.i"
        />
        <app-form-hr />
        <!-- Social links form component -->
        <app-form-social-links
          v-model:facebook="data.f"
          v-model:twitter="data.t"
          v-model:instagram="data.ig"
          v-model:github="data.gh"
          v-model:telegram="data.tg"
          v-model:linkedin="data.l"
          v-model:email="data.e"
          v-model:whatsapp="data.w"
          v-model:youtube="data.y"
        />
        <app-form-hr />
        <!-- Additional links form component -->
        <app-form-links v-model="data.ls" />
      </div>
      
      <!-- Button section for actions like adding demo data, publishing -->
      <div class="border-t bg-white flex items-center shadow-md rounded-lg p-2">
        <!-- Add demo data button -->
        <button
          @click="prefillDemoData"
          class="h-12 flex items-center space-x-2 px-4 border-r text-xs font-medium text-white bg-blue-500 hover:bg-blue-600 transition duration-200 rounded-lg"
        >
          <span> Add demo data </span>
          <icon name="mdi:code-json" class="h-4 w-4" />
        </button>
        <!-- Publish button -->
        <button
          @click="publish"
          class="h-12 flex items-center space-x-2 px-4 border-r text-xs font-medium text-white bg-green-500 hover:bg-green-600 transition duration-200 rounded-lg"
        >
          <span> Publish </span>
          <icon name="ph:paper-plane-tilt-bold" class="h-4 w-4" />
        </button>
        <!-- Github link -->
        <a
          href="https://github.com/losercodes/Ek-he"
          target="_blank"
          class="h-12 flex items-center space-x-2 px-4 border-r text-xs font-medium text-white bg-gray-700 hover:bg-gray-800 transition duration-200 rounded-lg"
        >
          <span> Github </span>
          <icon name="mdi:github" class="h-4 w-4" />
        </a>
      </div>
    </div>
    
    <!-- Preview section displaying the filled data -->
    <app-form-preview :data="data" />
    
    <!-- Attribution link at the bottom right -->
    <a
      href="https://twitter.com/AmanPandey_x"
      target="_blank"
      class="absolute bottom-0 right-0 bg-white rounded-tl-lg shadow-lg px-4 py-2 font-medium text-sm text-gray-500 hover:bg-gray-100 transition duration-200"
    >
      Made by redhanumn(AMN)
    </a>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { encodeData } from "../utils/transformer";

// Initializing data with ref to make it reactive
const data = ref({
  n: "",  // Name field
  d: "",  // Description field
  i: "",  // Image URL
  f: "",  // Facebook link
  t: "",  // Twitter link
  ig: "", // Instagram link
  gh: "", // Github link
  tg: "", // Telegram link
  l: "",  // LinkedIn link
  e: "",  // Email
  w: "",  // WhatsApp number
  y: "",  // YouTube link
  ls: [], // Additional links list
});

// Function to prefill the form with demo data
const prefillDemoData = () => {
  data.value = {
    n: "John", // Prefilled name
    d: "I’m John, the king in the north. I know Nothing.", // Prefilled description
    i: "https://i.insider.com/56743fad72f2c12a008b6cc0", // Prefilled image URL
    f: "https://www.facebook.com/john_snow", // Prefilled Facebook link
    t: "https://twitter.com/john_snow", // Prefilled Twitter link
    ig: "https://www.instagram.com/john_snow", // Prefilled Instagram link
    e: "mail@john_snow.cc", // Prefilled email
    gh: "https://github.com/john_snow", // Prefilled Github link
    tg: "https://t.me/john_snow", // Prefilled Telegram link
    w: "+918888888888", // Prefilled WhatsApp number
    y: "https://youtube.com/@john_snow", // Prefilled YouTube link
    l: "https://linkedin.com/john_snow", // Prefilled LinkedIn link
    ls: [  // Prefilled additional links
      {
        l: "My Website",
        i: "ph:globe-duotone",
        u: "https://example.com",
      },
      {
        l: "Amazon wishlist",
        i: "ant-design:amazon-outlined",
        u: "https://amazon.in",
      },
      {
        l: "React JS course",
        i: "grommet-icons:reactjs",
        u: "https://reactjs.org/",
      },
      {
        l: "Donate for our cause",
        i: "iconoir:donate",
        u: "https://who.int",
      },
      {
        l: "Download my resume",
        i: "ph:file-pdf",
        u: "https://google.com",
      },
    ],
  };
};

// Function to publish data and copy the link to the clipboard
const publish = () => {
  const url = `${window.location.origin}/1?data=${encodeData(data.value)}`;
  navigator.clipboard.writeText(url).then(() => {
    alert("Link copied to clipboard");
  });
};
</script>
