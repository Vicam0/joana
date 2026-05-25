<template>
  <transition name="intro-fade">
    <div v-if="loading" class="intro">
      <div class="intro-text">Joana</div>
    </div>
  </transition>

  <div v-if="!unlocked" class="gate">
    <div class="gate-box">
      <h2>What’s your name?</h2>
      <input v-model="name" placeholder="Type here..." @keyup.enter="checkName" />
      <button @click="checkName">Enter</button>
      <p v-if="error" class="error">Try again ❤️</p>
    </div>
  </div>

  <div v-show="unlocked" class="cinematic-overlays">
    <div class="film-grain"></div>
    <div class="vignette"></div>
    <div class="tilt-shift top"></div>
    <div class="tilt-shift bottom"></div>
  </div>

  <div class="page" v-show="unlocked">
    
    <div class="petals">
      <span v-for="n in 20" :key="n">🌸</span>
    </div>

    <div class="camera-drift-layer">
      
      <section class="hero fullscreen">
        <div class="fade-up title-group">
          <h1>Joana ❤️</h1>
          <p class="scroll-hint">Scroll for me bbg ↓</p>
        </div>
      </section>

      <section class="fullscreen photos">
        <div class="polaroid left">
          <img src="/src/assets/1.jpg"/>
        </div>

        <div class="polaroid right">
          <img src="/src/assets/3.jpg"/>
        </div>

        <div class="center-text">
          <h2>I Love Youu</h2>
        </div>
      </section>

      <section class="fullscreen glow">
        <div class="zoom-in">
          <h2>I Miss You So Much</h2>
          <p>everytime you go back to your village.</p>
          <p class="whisper">shh… it’s a village 🤍</p>
          
          <div class="polaroid left">
            <img src="/src/assets/4.jpg"/>
          </div>

          <div class="polaroid right">
            <img src="/src/assets/5.jpg"/>
          </div>
        </div>
      </section>

      <section class="fullscreen inside-joke">
        <div class="joke-wrap spin-in">
          <div class="joke-photo left-photo">
            <img src="/src/assets/forehead.jpg" alt="forehead" />
          </div>

          <div class="joke-center">
            <h2>LMAOO</h2>
            <p>You know exactly what day this is about.</p>
          </div>

          <div class="joke-photo right-photo">
            <img src="/src/assets/angry.jpg" alt="angry" />
          </div>
        </div>
      </section>

      <section class="fullscreen dreamy">
        <div class="slide-right">
          <h2>I Really</h2>
          <p>
            Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Really Apreciate What You Bring Into My Life
          </p>
        </div>
      </section>

      <section class="fullscreen final-screen">
        <div class="envelope-wrap">
          
          <transition name="fade">
            <div
              v-if="!opened"
              class="envelope"
              @click="opened = true"
            >
              <div class="envelope-emoji">💌</div>
              <p class="tap-hint">Tap to open</p>
            </div>
          </transition>

          <transition name="reveal">
            <div v-if="opened" class="letter">
              <h2>For you, Pretty Gurl</h2>
              <p>Thank you for being you.</p>

              <div class="spotlight">
                <img src="/src/assets/2.jpg" />
              </div>
            </div>
          </transition>

        </div>
      </section>

    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

const opened = ref(false)
const unlocked = ref(false)
const name = ref("")
const error = ref(false)
const loading = ref(true)

const checkName = () => {
  if (name.value.trim().toLowerCase() === "joana") {
    unlocked.value = true
  } else {
    error.value = true
  }
}

setTimeout(() => {
  loading.value = false
}, 2800)
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600&family=Cormorant+Garamond:wght@500&family=Dancing+Script:wght@700&display=swap");

body {
  margin: 0;
  overflow-x: hidden;
  background-color: #0b0507;
  background-image: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M30 15.5c-4-5-10-6-14-2-4.5 4.5-2 12 14 22 16-10 18.5-17.5 14-22-4-4-10-3-14 2z' fill='%23ff9fc5' fill-opacity='0.04' fill-rule='evenodd'/%3E%3C/svg%3E");
  animation: panBackground 40s linear infinite;
}

@keyframes panBackground {
  0% { background-position: 0 0; }
  100% { background-position: 100vw 100vh; }
}

.page {
  position: relative;
}

/* =========================================
   🎬 INTRO FADE FIX
   ========================================= */
.intro { position: fixed; inset: 0; background: black; display: flex; justify-content: center; align-items: center; z-index: 10000; }
.intro-text { font-size: 4rem; color: white; font-family: "Playfair Display"; animation: zoomFade 2.5s ease forwards; }

.intro-fade-leave-active { transition: opacity 1.2s ease-in-out; }
.intro-fade-leave-to { opacity: 0; }

@keyframes zoomFade {
  0% { transform: scale(0.8); opacity: 0; }
  50% { opacity: 1; }
  100% { transform: scale(1.3); opacity: 0; }
}

/* =========================================
   🎥 GENTLE CAMERA DRIFT
   ========================================= */
.camera-drift-layer {
  animation: cinematicDrift 14s ease-in-out infinite alternate;
}

@keyframes cinematicDrift {
  0% { transform: translateY(0) scale(1); }
  100% { transform: translateY(-15px) scale(1.01); }
}

/* =========================================
   🔍 FILM EFFECTS (Grain, Vignette, Blur)
   ========================================= */
.cinematic-overlays { position: fixed; inset: 0; pointer-events: none; z-index: 9998; }

.film-grain {
  position: absolute; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
  opacity: 0.06; mix-blend-mode: multiply;
}

.vignette { position: absolute; inset: 0; background: radial-gradient(circle at center, transparent 40%, rgba(0, 0, 0, 0.4) 120%); }

.tilt-shift { position: absolute; left: 0; right: 0; height: 20vh; backdrop-filter: blur(5px); -webkit-backdrop-filter: blur(5px); }
.tilt-shift.top { top: 0; mask-image: linear-gradient(to bottom, black 10%, transparent 100%); -webkit-mask-image: linear-gradient(to bottom, black 10%, transparent 100%); }
.tilt-shift.bottom { bottom: 0; mask-image: linear-gradient(to top, black 10%, transparent 100%); -webkit-mask-image: linear-gradient(to top, black 10%, transparent 100%); }

/* =========================================
   UI & SECTIONS
   ========================================= */
.gate { position: fixed; inset: 0; background: radial-gradient(circle, #ffd0df, #ff9fc5); display: flex; justify-content: center; align-items: center; z-index: 9999; }
.gate-box { background: white; padding: 2rem; border-radius: 20px; text-align: center; box-shadow: 0 20px 60px rgba(0,0,0,0.2); }
.gate input { padding: 0.8rem; margin-top: 1rem; border-radius: 12px; border: 1px solid #ccc; width: 200px; text-align: center; font-size: 1rem; outline: none; }
.gate button { margin-top: 1rem; padding: 0.6rem 1.2rem; border: none; border-radius: 12px; background: #6F956A; color: white; cursor: pointer; font-size: 1rem; transition: .2s; }
.gate button:hover { background: #5a7a56; }
.error { color: red; margin-top: 0.5rem; font-family: "Cormorant Garamond"; }

.fullscreen { min-height: 100svh; width: 100%; display: flex; justify-content: center; align-items: center; text-align: center; padding: 2rem; position: relative; overflow: hidden; box-sizing: border-box; }

h1 { font-family: "Playfair Display"; font-size: 5rem; color: white; margin: 0; }
h2 { font-family: "Playfair Display"; font-size: 3rem; color: #6F956A; margin: 0 0 1rem 0; }
p { font-family: "Cormorant Garamond"; font-size: 1.7rem; line-height: 1.6; margin: 0; }

.title-group { display: flex; flex-direction: column; align-items: center; gap: 1.5rem; }

.scroll-hint { font-family: "Cormorant Garamond"; font-size: 1.5rem; color: white; opacity: 0.85; animation: floatBounce 2s ease-in-out infinite; }

@keyframes floatBounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(12px); } }

.hero { background: linear-gradient(135deg,#ff9fc5,#ffcde1); }
.glow { background: radial-gradient(circle,#ffe8f1,#ffc6db); }
.photos { background: linear-gradient(135deg,#fff8f2,#ffdbe8); }
.inside-joke { background: linear-gradient(135deg,#694154,#302029); color: white; }
.dreamy { background: linear-gradient(135deg,#ffd0df,#fff2f7); }
.final-screen { background: linear-gradient(135deg,#ffb8d3,#fff3f8); }

.petals { position: fixed; inset: 0; pointer-events: none; z-index: 9000; }
.petals span { position: absolute; font-size: 2rem; animation: fall 12s linear infinite; }
.petals span:nth-child(odd) { left: 20%; animation-duration: 10s; }
.petals span:nth-child(even) { left: 80%; animation-duration: 14s; }

@keyframes fall { from { transform: translateY(-10vh) rotate(0deg); } to { transform: translateY(110vh) rotate(360deg); } }

/* =========================================
   ANIMATIONS & LAYOUT
   ========================================= */
.left { left: 12%; transform: rotate(-10deg); }
.right { right: 12%; transform: rotate(10deg); }

.fade-up { animation: fadeUp 1.3s ease; }
.zoom-in { animation: zoomIn 1s ease; }
.slide-right { animation: slideRight 1.2s ease; }
.spin-in { animation: spinIn 1s ease; }

@keyframes fadeUp { from { opacity: 0; transform: translateY(80px); } to { opacity: 1; } }
@keyframes zoomIn { from { transform: scale(.5); opacity: 0; } }
@keyframes slideRight { from { transform: translateX(-120px); opacity: 0; } }
@keyframes spinIn { from { transform: rotate(-12deg) scale(.7); opacity: 0; } }

/* =========================================
   ✨ NEW PRETTY ENVELOPE ✨
   ========================================= */
.envelope-wrap {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
  width: 100%;
}

.envelope {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.2rem;
  cursor: pointer;
  position: relative;
  z-index: 10;
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.envelope:hover {
  transform: scale(1.1) translateY(-5px);
}

.envelope-emoji {
  font-size: 7rem;
  line-height: 1;
  filter: drop-shadow(0 15px 25px rgba(255, 159, 197, 0.6));
  animation: floatEnvelope 4s ease-in-out infinite;
}

@keyframes floatEnvelope {
  0%, 100% { transform: translateY(0) rotate(-2deg); }
  50% { transform: translateY(-12px) rotate(3deg); }
}

.tap-hint {
  font-family: "Cormorant Garamond", serif;
  font-size: 1.3rem;
  color: #b05c7b;
  margin: 0;
  letter-spacing: 3px;
  text-transform: uppercase;
  font-weight: bold;
  animation: pulseGlow 2s infinite alternate;
}

@keyframes pulseGlow {
  from { opacity: 0.5; filter: drop-shadow(0 0 2px rgba(176,92,123,0)); }
  to { opacity: 1; filter: drop-shadow(0 0 10px rgba(176,92,123,0.4)); }
}

.letter {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  position: absolute;
  width: 100%;
  z-index: 5;
}

.spotlight {
  width: min(80vw, 500px);
  height: auto;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.3);
}

.spotlight img { width: 100%; display: block; }

/* Vue Transitions */
.fade-enter-active, .fade-leave-active { transition: opacity 0.5s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.reveal-enter-active { transition: all 1.2s cubic-bezier(0.16, 1, 0.3, 1); transition-delay: 0.2s; }
.reveal-leave-active { transition: all 0.5s ease; }
.reveal-enter-from, .reveal-leave-to { opacity: 0; transform: translateY(40px) scale(0.9); filter: blur(10px); }

/* =========================================
   MISC ELEMENTS
   ========================================= */
.whisper { margin-top: .5rem; font-family: "Dancing Script", cursive; font-size: 1.5rem; color: rgba(90, 90, 90, 0.65); letter-spacing: 1px; font-style: italic; animation: whisperFloat 3s ease-in-out infinite; }

@keyframes whisperFloat { 0%, 100% { transform: translateY(0); opacity: .65; } 50% { transform: translateY(-4px); opacity: .9; } }

.joke-wrap { width: 100%; max-width: 1300px; display: flex; align-items: center; justify-content: space-between; gap: 3rem; }
.joke-center { max-width: 520px; }
.joke-photo { width: 260px; border-radius: 22px; overflow: hidden; box-shadow: 0 18px 45px rgba(0,0,0,.25); }
.joke-photo img { width: 100%; display: block; }

.left-photo { transform: rotate(-8deg); animation: floatLeft 5s ease-in-out infinite; }
.right-photo { transform: rotate(8deg); animation: floatRight 5s ease-in-out infinite; }

@keyframes floatLeft { 0%,100% { transform: rotate(-8deg) translateY(0); } 50% { transform: rotate(-10deg) translateY(-14px); } }
@keyframes floatRight { 0%,100% { transform: rotate(8deg) translateY(0); } 50% { transform: rotate(10deg) translateY(-14px); } }

@media (max-width: 900px) { .joke-wrap { flex-direction: column; } .joke-photo { width: 220px; } }

.polaroid { position: absolute; background: white; padding: 1rem; width: 220px; height: 280px; border-radius: 18px; box-shadow: 0 12px 30px rgba(0,0,0,.15); display: flex; align-items: center; justify-content: center; overflow: hidden; }
.polaroid img { width: 100%; height: 100%; object-fit: cover; border-radius: 12px; }
</style>