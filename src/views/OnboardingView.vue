<template>
  <div class="fixed inset-0 bg-gray-50 flex flex-col">
    
    <div v-if="currentScreen === 'onboarding'" class="h-full flex flex-col">
      
      <div class="flex-1 flex items-center justify-center bg-gray-50 p-4">
        <img 
          :src="onboardingSteps[currentStep].image" 
          :alt="onboardingSteps[currentStep].title" 
          class="max-w-full max-h-[60vh] w-auto h-auto object-contain"
        >
      </div>

      <div class="p-8 bg-white shadow-2xl rounded-t-3xl">

        <div class="mb-4">
          <button class="w-full bg-red-500 text-white font-black text-xl py-5 rounded-2xl shadow-xl">
            {{ onboardingSteps[currentStep].title }}
          </button>
        </div>

        <div class="mb-8">
          <p class="text-gray-600 text-sm leading-relaxed text-center">
            {{ onboardingSteps[currentStep].description }}
          </p>
        </div>

        <div class="grid grid-cols-3 items-center">
          
          <button 
            @click="skipOnboarding" 
            class="bg-gray-100 hover:bg-gray-200 text-gray-800 font-bold px-4 py-3 rounded-xl text-base justify-self-start"
          >
            SKIP
          </button>

          <div class="flex gap-2 justify-center">
            <div
              v-for="(step, index) in onboardingSteps"
              :key="index"
              :class="['w-3 h-3 rounded-sm transition-all duration-300', index === currentStep ? 'bg-red-500 scale-110' : 'bg-gray-300']"
            ></div>
          </div>

          <button 
            @click="nextStep" 
            class="bg-red-500 hover:bg-red-600 text-white font-bold px-4 py-3 rounded-xl text-base justify-self-end"
          >
            NEXT
          </button>
        </div>
      </div>
    </div>

    <div v-else class="h-full w-full flex flex-col items-center justify-start bg-white">
      <div class="w-full h-full bg-red-500 pb-12 flex flex-col items-center">
        
        <div class="w-full max-w-md">
          
          <div class="text-center pt-10 pb-6">
            <div class="inline-block bg-white rounded-full p-4 mb-4 shadow-xl">
              <div class="text-4xl">❤️</div>
            </div>
            <h1 class="text-white text-4xl font-black tracking-wider">FATED</h1>
          </div>

          <div class="flex gap-4 px-8 mb-8">
            <button
              @click="isLoginMode = true"
              :class="[
                'flex-1 py-3 rounded-xl font-black transition-all text-lg',
                isLoginMode ? 'bg-white text-red-500 shadow-lg' : 'bg-red-400 text-white hover:bg-red-300'
              ]"
            >
              LOGIN
            </button>
            <button
              @click="isLoginMode = false"
              :class="[
                'flex-1 py-3 rounded-xl font-black transition-all text-lg',
                !isLoginMode ? 'bg-white text-red-500 shadow-lg' : 'bg-red-400 text-white hover:bg-red-300'
              ]"
            >
              REGISTER
            </button>
          </div>

          <div class="px-8 space-y-4">
            <input
              v-model="username"
              type="text"
              placeholder="user name"
              class="w-full px-5 py-4 rounded-xl text-center font-medium text-lg focus:outline-none focus:ring-4 focus:ring-white/50 shadow-md bg-red-400 placeholder-red-200"
              style="--tw-ring-color: #ffffff; color: white;"
            />
            <input
              v-model="password"
              type="password"
              placeholder="password"
              class="w-full px-5 py-4 rounded-xl text-center font-medium text-lg focus:outline-none focus:ring-4 focus:ring-white/50 shadow-md bg-red-400 placeholder-red-200"
              style="--tw-ring-color: #ffffff; color: white;"
            />
            <input
              v-if="!isLoginMode"
              v-model="email"
              type="email"
              placeholder="email"
              class="w-full px-5 py-4 rounded-xl text-center font-medium text-lg focus:outline-none focus:ring-4 focus:ring-white/50 shadow-md bg-red-400 placeholder-red-200"
              style="--tw-ring-color: #ffffff; color: white;"
            />

            <div v-if="isLoginMode" class="text-right pt-2">
              <button class="text-red-200 hover:text-white text-sm font-bold">FORGOT PASSWORD?</button>
            </div>

            <button
              @click="isLoginMode ? handleLogin() : handleRegister()"
              class="w-full bg-white text-red-500 font-black text-xl py-4 rounded-xl hover:bg-gray-100 transition-all mt-6 shadow-xl"
            >
              {{ isLoginMode ? 'LOGIN' : 'REGISTER' }}
            </button>
            
            <div class="text-center pt-4">
                <button @click="isLoginMode = !isLoginMode" class="text-red-200 text-sm hover:underline">
                    {{ isLoginMode ? "DON'T HAVE AN ACCOUNT?" : "ALREADY HAVE AN ACCOUNT?" }}
                    <span class="font-black">{{ isLoginMode ? 'REGISTER' : 'LOGIN' }}</span>
                </button>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'OnboardingView',
  data() {
    return {
      currentScreen: 'onboarding',
      currentStep: 0,
      isLoginMode: true,
      username: '',
      password: '',
      email: '',
      // Тут я змінила шляхи до зображень. Переконайтеся, що ці імена файлів існують у Вашій папці 'public'
      onboardingSteps: [
        {
          image: '/images/onboarding1.jpg', // Правильний шлях
          title: 'MEET NEW PEOPLE',
          description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer lacinia tellus quis est pharetra fermentum. Curabitur dapibus neque. Id luctus hendrerit rhoncus. Vivamus quis turpis enim metus.'
        },
        {
          image: '/images/onboarding2.jpg', // Правильний шлях 
          title: 'CHAT WITH EASE',
          description: 'Maecenas in placerat nibh. Integer sollicitudin sapien et massa varius venenatis. Nulla facilisi purus nec nibh posuere volutpat.'
        },
        {
          image: '/images/onboarding3.jpg', // Правильний шлях
          title: 'FIND YOUR MATCH',
          description: 'Nam vitae congue nulla. Aenean a orci eu ipsum congue convallis et tempus tellus. Donec porta eros ut viverra dapibus.'
        }
      ]
    };
  },
  methods: {
    nextStep() {
      // Логіка для переходу на наступний слайд, або на екран 'login'
      if (this.currentStep < this.onboardingSteps.length - 1) {
        this.currentStep++;
      } else {
        this.currentScreen = 'login';
      }
    },
    skipOnboarding() {
      // Перехід на екран 'login'
      this.currentScreen = 'login';
    },
    handleLogin() {
      alert('Login successful! 💕');
    },
    handleRegister() {
      alert('Registration successful! 💕');
    }
  }
};
</script>

<style scoped>
/* ВИПРАВЛЕННЯ ПОМИЛКИ theme() */
input::placeholder {
  /* Ми використовуємо HEX-код #fca5a5 (red-300) замість функції theme(), яка викликала помилку */
  color: #fca5a5; 
  opacity: 1; 
}
input[type="text"], input[type="password"], input[type="email"] {
  color: white; /* Колір введеного тексту */
}
</style>