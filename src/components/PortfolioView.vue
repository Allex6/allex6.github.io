<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import { 
  Github, 
  Linkedin, 
  BookOpen,
  Activity, 
  Lock, 
  ArrowUpRight,
  Atom,
  MapPin,
  FileText
} from 'lucide-vue-next';

// --- TIPO DE DADOS PARA TRADUÇÃO ---
type ProjectData = {
  title: string;
  subtitle: string;
  desc: string;
  url: string; // Novo campo URL
  status?: string;
};

type Translation = {
  role: string;
  headline: string;
  subHeadline: string;
  projects: {
    infralens: ProjectData;
    entangle: ProjectData;
    jscience: ProjectData;
    stealth: { label: string; tooltip: string };
  };
  footer: {
    rights: string;
    location: string;
    companyIdLabel: string;
  };
};

// --- DICIONÁRIO DE TEXTOS ---
const messages: Record<'en' | 'pt', Translation> = {
  en: {
    role: "Engineer. Founder. Scientist.",
    headline: "Architecting autonomous systems and scientific tools.",
    subHeadline: "Building the future of open-source infrastructure.",
    projects: {
      infralens: { 
        title: "InfraLens",
        subtitle: "The AWS Cost & Security Scanner",
        desc: "Agentless scanner that connects securely to AWS to find idle resources and security risks.", 
        status: "Live & Profitable",
        url: "https://infralens.com.br"
      },
      entangle: { 
        title: "Entangle.ts",
        subtitle: "Physics-Inspired Event Framework",
        desc: "Treats business objects as 'Particles' and events as 'Bosons', allowing for highly decoupled logic.",
        url: "https://github.com/Allex6/Entangle.ts"
      },
      jscience: { 
        title: "JScience",
        subtitle: "Scientific Computing for Node.js",
        desc: "Essential statistical functions and probability distributions focused on performance and accuracy.",
        url: "https://github.com/Allex6/jscience"
      },
      stealth: { label: "Stealth Project", tooltip: "Loading..." }
    },
    footer: {
      rights: "All rights reserved.",
      location: "Brazil",
      companyIdLabel: "Tax ID"
    }
  },
  pt: {
    role: "Engenheiro. Founder. Cientista.",
    headline: "Arquitetando sistemas autônomos e ferramentas científicas.",
    subHeadline: "Construindo o futuro da infraestrutura open-source.",
    projects: {
      infralens: { 
        title: "InfraLens",
        subtitle: "O Scanner de Custo e Segurança AWS",
        desc: "Scanner sem agentes que encontra recursos ociosos e riscos de segurança na AWS.", 
        status: "Lucrativo & Ativo",
        url: "https://infralens.com.br"
      },
      entangle: { 
        title: "Entangle.ts",
        subtitle: "Framework de Eventos Inspirado em Física",
        desc: "Trata objetos de negócio como 'Partículas' e eventos como 'Bósons' para lógica desacoplada.",
        url: "https://github.com/Allex6/Entangle.ts"
      },
      jscience: { 
        title: "JScience",
        subtitle: "Computação Científica para Node.js",
        desc: "Funções estatísticas essenciais e distribuições de probabilidade com foco em performance.",
        url: "https://github.com/Allex6/jscience"
      },
      stealth: { label: "Projeto Secreto", tooltip: "Carregando..." }
    },
    footer: {
      rights: "Todos os direitos reservados.",
      location: "Brasil",
      companyIdLabel: "CNPJ"
    }
  }
};

// --- STATE MANAGEMENT ---
const currentLang = ref<'en' | 'pt'>('en');
const t = computed(() => messages[currentLang.value]);

const toggleLang = () => {
  currentLang.value = currentLang.value === 'en' ? 'pt' : 'en';
};

onMounted(() => {
  const userLang = navigator.language.startsWith('pt') ? 'pt' : 'en';
  currentLang.value = userLang;
});

// --- UTILS ---
// Adicionado 'block' para garantir que a tag <a> ocupe o espaço todo
const cardBaseClass = "block group relative overflow-hidden rounded-2xl border border-white/10 bg-white/5 p-6 backdrop-blur-md transition-all duration-300 hover:border-[#2563EB]/50 hover:shadow-[0_0_30px_-5px_rgba(37,99,235,0.2)]";
</script>

<template>
  <div class="min-h-screen bg-[#050505] text-gray-300 selection:bg-[#2563EB] selection:text-white font-sans pb-20 w-full flex flex-col">
    
    <header class="mx-auto max-w-6xl px-6 py-8 flex justify-between items-center w-full">
      
      <div class="group cursor-pointer select-none">
        <h1 class="font-grotesk text-2xl font-bold tracking-tight text-white group-hover:text-gray-100 transition-colors">
          alex.souza<span class="text-[#2563EB] animate-cursor-blink">_</span>
        </h1>
      </div>

      <button 
        @click="toggleLang"
        class="flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-4 py-2 text-xs font-mono font-bold uppercase tracking-wider transition-colors hover:bg-white/10 hover:border-white/20 focus:outline-none"
      >
        <span :class="{ 'text-white': currentLang === 'pt', 'text-gray-500': currentLang !== 'pt' }">BR</span>
        <span class="text-gray-600">|</span>
        <span :class="{ 'text-white': currentLang === 'en', 'text-gray-500': currentLang !== 'en' }">EN</span>
      </button>
    </header>

    <main class="mx-auto max-w-6xl px-6 pt-12 pb-20 w-full flex-grow">
      <div class="mb-16 space-y-6">
        <h1 class="max-w-3xl text-4xl font-light tracking-tight text-white sm:text-6xl lg:text-7xl">
          {{ t.role }}
        </h1>
        <p class="max-w-2xl text-lg text-gray-400 font-light leading-relaxed">
          {{ t.headline }}
        </p>
      </div>

      <div class="grid grid-cols-1 gap-6 md:grid-cols-3 md:grid-rows-2 auto-rows-[minmax(200px,auto)]">
        
        <a 
          :href="t.projects.infralens.url"
          target="_blank"
          :class="[cardBaseClass, 'md:col-span-2 md:row-span-2 flex flex-col justify-between min-h-[400px]']"
        >
          <div class="absolute inset-0 bg-gradient-to-b from-transparent via-[#050505]/60 to-[#050505]/90 z-10"></div>
          
          <div class="absolute inset-0 z-0 transition-transform duration-700 group-hover:scale-105">
            <img 
              src="/infralens-cover.png" 
              alt="InfraLens Dashboard" 
              class="h-full w-full object-cover grayscale mix-blend-luminosity opacity-50 transition-all duration-500 group-hover:grayscale-0 group-hover:opacity-100"
            />
          </div>

          <div class="relative z-20 flex justify-between items-start">
            <div class="rounded-lg bg-black/50 backdrop-blur-sm border border-white/10 p-2 transition-colors group-hover:bg-[#2563EB]/20 group-hover:border-[#2563EB]/50">
              <Activity class="h-6 w-6 text-[#2563EB] transition-transform group-hover:scale-110" />
            </div>
            <span class="inline-flex items-center rounded-full border border-green-500/30 bg-green-500/10 px-2.5 py-0.5 text-xs font-mono font-medium text-green-400">
              {{ t.projects.infralens.status }}
            </span>
          </div>

          <div class="relative z-20 mt-auto">
            <h3 class="text-2xl font-semibold text-white group-hover:text-[#2563EB] transition-colors">
              {{ t.projects.infralens.title }}
            </h3>
            <p class="text-xs font-mono text-[#2563EB] mb-1">{{ t.projects.infralens.subtitle }}</p>
            <p class="mt-2 text-sm text-gray-300 max-w-lg">{{ t.projects.infralens.desc }}</p>
            
            <div class="mt-6 flex items-center gap-3">
               <span class="text-xs font-mono border border-white/10 px-2 py-1 rounded bg-black/40 text-gray-400">Vue 3</span>
               <span class="text-xs font-mono border border-white/10 px-2 py-1 rounded bg-black/40 text-gray-400">Node.js</span>
               <span class="text-xs font-mono border border-white/10 px-2 py-1 rounded bg-black/40 text-gray-400">AWS SDK</span>
            </div>
             <div class="mt-4 flex items-center gap-2 text-sm font-mono text-[#2563EB] opacity-0 translate-y-2 transition-all group-hover:opacity-100 group-hover:translate-y-0">
              Visit Website <ArrowUpRight class="h-4 w-4" />
            </div>
          </div>
        </a>

        <a :href="t.projects.entangle.url" target="_blank" :class="cardBaseClass">
          <div class="mb-4 rounded-lg bg-white/5 w-fit p-3 transition-colors group-hover:bg-[#2563EB]/20 group-hover:border-[#2563EB]/50">
            <Atom class="h-6 w-6 text-white transition-colors group-hover:text-[#2563EB]" />
          </div>
          <h3 class="text-xl font-semibold text-white group-hover:text-[#2563EB] transition-colors">{{ t.projects.entangle.title }}</h3>
          <p class="text-[10px] uppercase tracking-wider text-gray-500 font-bold mb-2">{{ t.projects.entangle.subtitle }}</p>
          <p class="mt-2 text-sm text-gray-400">{{ t.projects.entangle.desc }}</p>
          <div class="mt-4 flex items-center gap-2 text-sm font-mono text-[#2563EB] opacity-0 translate-y-2 transition-all group-hover:opacity-100 group-hover:translate-y-0">
              View Github <ArrowUpRight class="h-4 w-4" />
            </div>
        </a>

        <a :href="t.projects.jscience.url" target="_blank" :class="cardBaseClass">
          <div class="mb-4 rounded-lg bg-white/5 w-fit p-3 transition-colors group-hover:bg-[#2563EB]/20 group-hover:border-[#2563EB]/50">
            <BookOpen class="h-6 w-6 text-white transition-colors group-hover:text-[#2563EB]" />
          </div>
          <h3 class="text-xl font-semibold text-white group-hover:text-[#2563EB] transition-colors">{{ t.projects.jscience.title }}</h3>
          <p class="text-[10px] uppercase tracking-wider text-gray-500 font-bold mb-2">{{ t.projects.jscience.subtitle }}</p>
          <p class="mt-2 text-sm text-gray-400">{{ t.projects.jscience.desc }}</p>
          <div class="mt-4 flex items-center gap-2 text-sm font-mono text-[#2563EB] opacity-0 translate-y-2 transition-all group-hover:opacity-100 group-hover:translate-y-0">
              View Github <ArrowUpRight class="h-4 w-4" />
            </div>
        </a>

        <article :class="[cardBaseClass, 'md:col-span-2 md:col-start-2 flex items-center justify-center relative']">
          <div class="absolute inset-0 bg-[#050505]/80 backdrop-blur-xl z-10 flex flex-col items-center justify-center gap-4">
             <Lock class="h-8 w-8 text-gray-600" />
             <span class="font-mono text-xs uppercase tracking-[0.2em] text-gray-500 animate-pulse">
               {{ t.projects.stealth.tooltip }}
             </span>
          </div>
          <div class="blur-sm opacity-20 flex flex-col gap-4 w-full">
            <div class="h-8 w-1/3 bg-gray-700 rounded"></div>
            <div class="h-20 w-full bg-gray-800 rounded"></div>
          </div>
          <div class="absolute bottom-4 left-6 z-20">
            <span class="text-sm font-mono text-gray-500">{{ t.projects.stealth.label }}</span>
          </div>
        </article>

      </div>
    </main>

    <footer class="mx-auto max-w-6xl px-6 border-t border-white/5 py-12 w-full mt-auto">
      <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
        
        <div class="flex flex-col gap-2">
          <div class="text-sm text-gray-400">
            &copy; 2026 Alex Souza. {{ t.footer.rights }}
          </div>
          <div class="flex gap-4 text-xs font-mono text-gray-600">
            <span class="flex items-center gap-1">
              <MapPin class="h-3 w-3" /> {{ t.footer.location }}
            </span>
            <span class="flex items-center gap-1">
              <FileText class="h-3 w-3" /> {{ t.footer.companyIdLabel }}: 48.078.381/0001-58
            </span>
          </div>
        </div>

        <div class="flex gap-6">
          <a href="https://github.com/allex6" target="_blank" class="text-gray-500 hover:text-white transition-colors" title="GitHub">
            <Github class="h-5 w-5" />
          </a>
          <a href="https://www.linkedin.com/in/alex-s-franca/" target="_blank" class="text-gray-500 hover:text-[#0A66C2] transition-colors" title="LinkedIn">
            <Linkedin class="h-5 w-5" />
          </a>
          <a href="https://medium.com/@allex6" target="_blank" class="text-gray-500 hover:text-white transition-colors" title="Medium">
            <BookOpen class="h-5 w-5" />
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&family=Space+Grotesk:wght@500;700&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap');

.font-mono { font-family: 'Space Mono', monospace; }
.font-sans { font-family: 'Inter', sans-serif; }
.font-grotesk { font-family: 'Space Grotesk', sans-serif; }
</style>