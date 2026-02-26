<template>
  <div class="landing-container">

    <div id="sakura-container" ref="sakuraContainer"></div>

    <div class="side-decorations">
      <div class="paper-plane">
        <i class="fa-solid fa-paper-plane"></i>
      </div>
      <div class="deco-lantern left-lantern">
        <div class="lantern-body"></div>
        <div class="lantern-string"></div>
      </div>
      <div class="deco-lantern right-lantern">
        <div class="lantern-body" style="background: var(--blue-soft)"></div>
        <div class="lantern-string"></div>
      </div>
    </div>

    <transition name="modal-fade">
      <div v-if="isModalOpen" class="modal-overlay active" @click.self="closeModal">
        <div class="modal-content">
          <div class="modal-close" @click="closeModal">
            <i class="fa-solid fa-xmark"></i>
          </div>

          <img :src="currentModalData.img" alt="City" class="modal-img">

          <div class="modal-header-info">
            <span class="badge" style="font-size: 0.9rem;">{{ currentModalData.dates }}</span>
            <span class="badge" style="background: var(--pink-pop); color: white;">{{ currentModalData.fee }}</span>
          </div>

          <h2 class="modal-title">{{ currentModalData.city }}</h2>
          <h4 style="color: #666; margin-bottom: 15px;">{{ currentModalData.title }}</h4>

          <p class="modal-desc">
            Eveniment academic BEST în <strong>{{ currentModalData.country }}</strong>.
            <br>O oportunitate unică de a învăța și a călători.
          </p>

          <a :href="currentModalData.link" target="_blank" class="btn-pop" style="padding: 10px 30px; font-size: 0.9rem;">
            <i class="fa-solid fa-heart"></i> Mă înscriu
          </a>
        </div>
      </div>
    </transition>

    <nav>
      <div class="logo mouse-hover">
        <img src="/images/logo.png" alt="BEST Logo" class="nav-logo-img" style="height: 55px">
      </div>
      <div class="nav-links">
        <a href="#hero" class="mouse-hover">Home</a>
        <a href="#courses" class="mouse-hover">Destinații</a>
        <a href="#process" class="mouse-hover">Proces</a>
        <a href="#essentials" class="mouse-hover">Pack-it</a>
        <a href="#faq" class="mouse-hover">FAQ</a>
        <a href="#contact" class="mouse-hover">Contact</a>
      </div>
      <a href="#courses" class="btn-pop mouse-hover" style="padding: 10px 25px; font-size: 0.9rem;">Leave a massage</a>
    </nav>

    <section id="hero" class="hero">
      <div class="blob-bg" style="background: var(--pink-soft); top: 10%; left: 10%; width: 300px; height: 300px; border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;"></div>
      <div class="blob-bg" style="background: var(--blue-soft); bottom: 10%; right: 10%; width: 400px; height: 400px; border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;"></div>

      <h4 style="color: var(--blue-sky); letter-spacing: 4px; margin-bottom: 15px; font-weight: 800;">SEASON 2026</h4>
      <h1>Time to <span ref="typedText" class="highlight"></span></h1>
      <p>Experiențe legendare, prieteni noi și cursuri academice de calitate/calitative în toată Europa. <br>Aventura ta începe aici.</p>
      <div style="margin-top: 40px;">
        <a href="#courses" class="btn-pop mouse-hover"><i class="fa-solid fa-rocket"></i> Explorează Cursuri</a>
      </div>
    </section>

    <section class="stats-bar" data-aos="fade-up">
      <div class="stat-item">
        <h3>8</h3>
        <p>Destinații</p>
      </div>
      <div class="stat-item">
        <h3>80€</h3>
        <p>Cost Mediu</p>
      </div>
      <div class="stat-item">
        <h3>100%</h3>
        <p>Fun Garantat</p>
      </div>
    </section>

    <section class="section-padding">
      <h2 class="text-center" data-aos="fade-up">De ce sa aplici?</h2>
      <div class="card-container">
        <div class="tilt-card" ref="tiltElements" data-tilt data-tilt-glare data-tilt-max-glare="0.8">
          <div class="tilt-icon"><i class="fa-solid fa-piggy-bank" style="color: var(--pink-pop)"></i></div>
          <h3>Super Cheap</h3>
          <p>Cazare, masă și distracție asigurate la un preț studențesc imbatabil.</p>
        </div>
        <div class="tilt-card" ref="tiltElements" data-tilt data-tilt-glare data-tilt-max-glare="0.8">
          <div class="tilt-icon"><i class="fa-solid fa-graduation-cap" style="color: var(--blue-sky)"></i></div>
          <h3>Academic Boost</h3>
          <p>Primești diplomă recunoscută internațional și credite ECTS extra.</p>
        </div>
        <div class="tilt-card" ref="tiltElements" data-tilt data-tilt-glare data-tilt-max-glare="0.8">
          <div class="tilt-icon"><i class="fa-solid fa-champagne-glasses" style="color: var(--accent-gold)"></i></div>
          <h3>Social Life</h3>
          <p>Petreceri tematice, International Evening și prieteni din toată Europa.</p>
        </div>
      </div>
    </section>

    <section id="courses" class="section-padding" style="background: rgba(255,255,255,0.4);">
      <h2 class="text-center" style="margin-bottom: 50px;" data-aos="zoom-in">Destinatii Europene</h2>
      <p class="text-center" style="margin-top: -30px; margin-bottom: 50px; color: var(--pink-pop); font-weight: 700; letter-spacing: 1px;">CLICK PE IMAGINI PENTRU DETALII</p>

      <div class="swiper mySwiper">
        <div class="swiper-wrapper">
          <div
              v-for="(course, index) in coursesList"
              :key="index"
              class="swiper-slide mouse-hover"
              @click="openModal(course)"
              :style="{ backgroundImage: `url(${course.img})` }"
          >
            <div class="slide-content">
              <span class="badge">{{ course.country }}</span>
              <h3>{{ course.city }}</h3>
              <p style="font-size: 0.85rem; opacity: 0.9; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden;">
                {{ course.title }}
              </p>
            </div>
          </div>
        </div>
        <div class="swiper-pagination"></div>
      </div>
    </section>

    <section id="process" class="section-padding" style="background: #fff;">
      <h2 class="text-center" data-aos="fade-down">Ghid de Aplicare</h2>

      <div class="tabs-container">
        <div class="tabs-header">
          <button @click="activeTab = 'cine'" :class="{active: activeTab === 'cine'}">Cine poate?</button>
          <button @click="activeTab = 'cum'" :class="{active: activeTab === 'cum'}">Cum aplic?</button>
          <button @click="activeTab = 'scrisoare'" :class="{active: activeTab === 'scrisoare'}">Motivație</button>
          <button @click="activeTab = 'validare'" :class="{active: activeTab === 'validare'}">Validare Cont</button>
        </div>

        <div class="tab-content card-pop" data-aos="fade-up">
          <div v-if="activeTab === 'cine'">
            <h3><i class="fa-solid fa-user-graduate"></i> Eligibilitate</h3>
            <p>{{ aplicareContent.cine.text }}</p>
            <ul class="styled-list">
              <li v-for="rule in aplicareContent.cine.rules" :key="rule">{{ rule }}</li>
            </ul>
          </div>

          <div v-if="activeTab === 'cum'">
            <h3><i class="fa-solid fa-list-check"></i> Pașii necesari</h3>
            <div class="process-grid">
              <div v-for="(step, i) in aplicareContent.cum.steps" :key="i" class="mini-step">
                <span>{{ i + 1 }}</span> {{ step }}
              </div>
            </div>
            <p class="note"><strong>Sfat:</strong> Taxa pentru participanții din România este de 60% din taxa afișată!</p>
          </div>

          <div v-if="activeTab === 'scrisoare'">
            <h3><i class="fa-solid fa-pen-nib"></i> Scrisoarea de Motivație</h3>
            <p>Este cel mai important document! Arată-le cine ești, pasiunile tale și de ce ai ales acea destinație.</p>
            <div class="tip-box">
              <i class="fa-solid fa-lightbulb"></i> Fii original! Organizatorii apreciază umorul și autenticitatea.
            </div>
          </div>

          <div v-if="activeTab === 'validare'">
            <h3><i class="fa-solid fa-user-check"></i> Cum îți activezi contul?</h3>
            <p>După înregistrarea pe site-ul european, trimite-ne un mesaj cu: Nume, Email, Telefon, Facultate și An.</p>
            <p><strong>Urmează:</strong> O scurtă conversație în limba engleză pentru confirmare!</p>
          </div>
        </div>
      </div>
    </section>

    <section id="essentials" class="section-padding">
      <h2 class="text-center" data-aos="fade-down">Pack with me</h2>
      <div class="checklist-grid" data-aos="fade-up">
        <div v-for="(item, index) in checklistItems" :key="index"
             class="check-item mouse-hover"
             :class="{ checked: item.checked }"
             @click="toggleCheck(index)">
          <i :class="item.icon"></i>
          <p>{{ item.text }}</p>
        </div>
      </div>
    </section>

    <section id="rules" class="section-padding" style="background: linear-gradient(to right, #fdfbfb, #ebedee);">
      <div class="rules-grid">
        <div class="rules-column" data-aos="fade-right">
          <h2 style="font-size: 2rem;"><i class="fa-solid fa-gift" style="color: var(--pink-pop)"></i> Beneficii</h2>
          <div class="rule-card">
            <ul>
              <li><i class="fa-solid fa-check"></i> Aproximativ 20h cursuri/săptămână</li>
              <li><i class="fa-solid fa-check"></i> Cazare și 3 mese pe zi incluse</li>
              <li><i class="fa-solid fa-check"></i> Certificat oficial + credite ECTS</li>
              <li><i class="fa-solid fa-check"></i> Program social și petreceri tematice</li>
            </ul>
          </div>
        </div>
        <div class="rules-column" data-aos="fade-left">
          <h2 style="font-size: 2rem;"><i class="fa-solid fa-shield-halved" style="color: var(--blue-sky)"></i> Responsabilitati</h2>
          <div class="rule-card">
            <ul>
              <li><i class="fa-solid fa-circle-exclamation"></i> Prezență la întreaga parte academică</li>
              <li><i class="fa-solid fa-circle-exclamation"></i> Comportament civilizat și respectuos</li>
              <li><i class="fa-solid fa-circle-exclamation"></i> Completarea formularului de evaluare final</li>
              <li><i class="fa-solid fa-circle-exclamation"></i> Plata depozitului de confirmare</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <section id="faq" class="section-padding" style="background: #fdfbfb;">
      <h2 class="text-center">Întrebari Frecvente</h2>
      <div class="faq-container">
        <div class="faq-item" v-for="(faq, i) in faqs" :key="i" @click="faq.open = !faq.open" :class="{ open: faq.open }">
          <div class="faq-question">
            <h4>{{ faq.question }}</h4>
            <i class="fa-solid fa-chevron-down"></i>
          </div>
          <div class="faq-answer" v-if="faq.open">
            <p>{{ faq.answer }}</p>
          </div>
        </div>
      </div>
    </section>

    <section id="responsible" class="section-padding" style="background: linear-gradient(to bottom, #fff, #fff0f5);">
      <h2 class="text-center" data-aos="zoom-in">Responsabil Vivaldi 👑</h2>

      <div class="responsible-wrapper" data-aos="flip-up">
        <div class="responsible-card mouse-hover">
          <img src="/images/diana.jpg" class="resp-img" alt="Diana Georgescu">
          <div class="resp-content">
            <h3>Diana Georgescu</h3>
            <span class="resp-role">Main Organizer & Responsible</span>
            <p>Ea se asigură că ajungi cu bine la destinație și că ai cea mai tare experiență academică. Orice întrebare ai, ea este persoana potrivită!</p>
          </div>
        </div>
      </div>
    </section>

    <section class="section-padding" style="background: #fff;">
      <h2 class="text-center" style="margin-bottom: 40px;">Wall of Memories</h2>
      <div class="gallery-wrapper">
        <img
            v-for="(img, index) in wallPhotos"
            :key="index"
            :src="`/images/wallofmemories/${img}`"
            class="gallery-img"
            data-aos="fade-up"
            :alt="'Memory ' + index"
        >
      </div>
    </section>

    <section id="contact" class="section-padding">
      <h2 class="text-center" style="margin-bottom: 50px;">Hai sa povestim</h2>
      <div class="contact-box" data-aos="zoom-in">
        <div class="contact-info">
          <h3>BEST Brasov</h3>
          <p>brasov@best-eu.org</p>
        </div>
        <div class="contact-form">
          <form>
            <input type="text" placeholder="Numele tău" class="mouse-hover">
            <input type="email" placeholder="Email" class="mouse-hover">
            <textarea rows="3" placeholder="Mesaj..." class="mouse-hover"></textarea>
            <button type="button" class="btn-pop mouse-hover" style="width: 100%;">Trimite Mesaj</button>
          </form>
        </div>
      </div>
    </section>

    <footer>
      <div class="text-center" style="padding: 60px 40px;">
        <h2 style="color: var(--blue-sky); margin-bottom: 20px;">BEST Travel</h2>

        <div class="footer-socials" style="margin-bottom: 25px;">
          <a href="https://www.instagram.com/bestbrasov/" target="_blank" class="social-icon">
            <i class="fa-brands fa-instagram"></i>
          </a>
          <a href="https://www.facebook.com/BESTBrasov" target="_blank" class="social-icon">
            <i class="fa-brands fa-facebook-f"></i>
          </a>
        </div>

        <p style="font-size: 0.9rem; opacity: 0.6;">
          Designed with <i class="fa-solid fa-heart" style="color:var(--pink-pop)"></i> for BEST Brasov
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Swiper from 'swiper/bundle';
import 'swiper/css/bundle';
import AOS from 'aos';
import 'aos/dist/aos.css';
import Typed from 'typed.js';
import VanillaTilt from 'vanilla-tilt';

const cursorDot = ref(null);
const cursorOutline = ref(null);
const typedText = ref(null);
const tiltElements = ref([]);
const sakuraContainer = ref(null);

const isModalOpen = ref(false);
const currentModalData = ref({});

const coursesList = ref([
  {
    city: 'Bordeaux',
    country: 'France',
    title: 'Surf on an ecological wave: Designing the next gen surf Board',
    dates: '14 - 21 June 2026',
    fee: '70.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2mno9q',
    img: 'https://st4.depositphotos.com/1000633/38184/i/450/depositphotos_381841026-stock-photo-bordeaux-france-june-2016-place.jpg'
  },
  {
    city: 'Istanbul',
    country: 'Turkiye',
    title: 'The Wolf of Digital Street: Sell Me This Product!',
    dates: '17 - 24 June 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11q',
    img: 'https://images.unsplash.com/photo-1524231757912-21f4fe3a7200?auto=format&fit=crop&w=800&q=80'
  },
  {
    city: 'Maribor',
    country: 'Slovenia',
    title: 'Pax Informatica: Advanced usage of Generative AI and LLMs',
    dates: '27 June - 4 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3ljmak',
    img: 'https://media.istockphoto.com/id/1163181078/photo/maribor-and-its-bridges-over-drava-river.jpg?s=612x612&w=0&k=20&c=cJwvBcBqGpx7tYVDf0KabnXy_U0eVYoLOipgaMmGTbQ='
  },
  {
    city: 'Tallinn',
    country: 'Estonia',
    title: 'Think Like a CFO, Act Like a Leader - The Basics of Finance, Investing & Leadership',
    dates: '28 June - 8 July 2026',
    fee: '75.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=o1nrq8q',
    img: 'https://media.digitalnomads.world/wp-content/uploads/2021/03/20120553/tallinn-digital-nomads-1024x683.jpg'
  },
  {
    city: 'Louvain-la-Neuve',
    country: 'Belgium',
    title: 'Giving shape to the unknown: Machine Design and Rapid Prototyping',
    dates: '2 - 11 July 2026',
    fee: '85.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11y',
    img: 'https://blog.martinshotels.com/content/images/2024/11/12-MLLN-vue-aerienne-2022-PTE-CMYK---copyright-Simon-Schmitt.jpg'
  },
  {
    city: 'Istanbul',
    country: 'Turkiye',
    title: 'Paradise on Marketing: Where Brands Catch Waves',
    dates: '4 - 12 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3ljmah',
    img: 'https://images.unsplash.com/photo-1541432901042-2d8bd64b4a9b?auto=format&fit=crop&w=800&q=80'
  },
  {
    city: 'Košice',
    country: 'Slovakia',
    title: 'Lord of the Things: Create your own smart household with IoT!',
    dates: '5 - 12 July 2026',
    fee: '65.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=i4afz2n',
    img: 'https://s.inyourpocket.com/gallery/253753.jpg'
  },
  {
    city: 'Patras',
    country: 'Greece',
    title: 'Journal 4: Clean energy, New technologies & suSTANable buildings',
    dates: '5 - 13 July 2026',
    fee: '72.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=i4afz2p',
    img: 'https://www.greeka.com/photos/peloponnese/patra/hero/patra-1920.jpg'
  },
  {
    city: 'Skopje',
    country: 'North Macedonia',
    title: 'Designing Digital Experiences: Why Some Apps Feel Amazing',
    dates: '5 - 13 July 2026',
    fee: '66.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11g',
    img: 'https://cdn.tripspoint.com/uploads/photos/5106/skopje-city-tour-the-best-of-skopje_VlPmA.jpeg'
  },
  {
    city: 'Leuven',
    country: 'Belgium',
    title: 'Double Trouble: When Physical Systems Go Digital',
    dates: '7 - 16 July 2026',
    fee: '100.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11n',
    img: 'https://dynamic-media-cdn.tripadvisor.com/media/photo-o/04/4e/92/c5/old-market-square-oude.jpg?w=1200&h=700&s=1'
  },
  {
    city: 'Vienna',
    country: 'Austria',
    title: "Gru's Guide for Minion Space Engineering: Tonight we steal the moon!",
    dates: '11 - 19 July 2026',
    fee: '75.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11k',
    img: 'https://dynamic-media-cdn.tripadvisor.com/media/photo-o/17/78/c3/76/caption.jpg?w=1200&h=-1&s=1'
  },
  {
    city: 'Iași',
    country: 'Romania',
    title: 'Empowered Diversity: International Mobility, Wellbeing, and Inclusive Campus Cultures',
    dates: '11 - 22 July 2026',
    fee: '50.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=g59bx2x',
    img: 'https://covinnus.com/wp-content/uploads/2021/11/Palace-of-Culture-Iasi.jpg'
  },
  {
    city: 'Bucharest',
    country: 'Romania',
    title: 'Once Upon a Model: Bring Your Design Concepts to Life in Software',
    dates: '12 - 21 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2mno9k',
    img: 'https://static01.nyt.com/images/2018/11/18/travel/18Hours-Bucharest1/18Hours-Bucharest1-superJumbo-v3.jpg'
  },
  {
    city: 'Wrocław',
    country: 'Poland',
    title: 'Racing against hackers: Advanced Cybersecurity and Digital Forensics for IoT',
    dates: '14 - 22 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=i4afz2k',
    img: 'https://wa-uploads.profitroom.com/hastonoldtown/1920x850/17472937705063_wroclove.jpeg'
  },
  {
    city: 'Coimbra',
    country: 'Portugal',
    title: 'Space Safety: Your Guide to the Final Frontier',
    dates: '15 - 24 July 2026',
    fee: '90.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2co30m',
    img: 'https://images.winalist.com/blog/wp-content/uploads/2025/03/23063825/adobestock-164104316-1500x734.jpeg'
  },
  {
    city: 'Chișinău',
    country: 'Moldova',
    title: 'When Code Makes Decisions: A Gentle Introduction to Agentic AI',
    dates: '21 - 28 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3ljman',
    img: 'https://www.aviontourism.com/images/1260-2600-fix/573c3c8e-00d8-4a30-9384-3aeddfa9f5fc'
  },
  {
    city: 'Aveiro',
    country: 'Portugal',
    title: 'Data Science: Turning Stranger Data the Rightside Up',
    dates: '22 - 29 July 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2mno9n',
    img: 'https://bulgarianonthego.blog/wp-content/uploads/2022/05/things-to-do-in-aveiro-25-min.jpg'
  },
  {
    city: 'Rome',
    country: 'Italy',
    title: 'Fly Me To The Moon: Engineering The BEST Space Supply Chain',
    dates: '26 July - 1 August 2026',
    fee: '70.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11s',
    img: 'https://images.unsplash.com/photo-1552832230-c0197dd311b5?auto=format&fit=crop&w=800&q=80'
  },
  {
    city: 'Messina',
    country: 'Italy',
    title: 'TRON: The Rise of Autonomous Vehicles',
    dates: '26 July - 2 August 2026',
    fee: '50.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11j',
    img: 'https://www.sightseeing-experience.com/magazine/wp-content/uploads/2024/08/AdobeStock_46229260-scaled.jpeg'
  },
  {
    city: 'Mostar',
    country: 'Bosnia and Herzegovina',
    title: 'Attention Economy: How Brands Win Minds',
    dates: '26 July - 1 August 2026',
    fee: '70.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2co30g',
    img: 'https://media.cntraveller.com/photos/650c037b9a4941357e144469/16:9/w_2112,h_1188,c_limit/Mostar,%20Bosnia%20and%20Herzegovina-GettyImages-909655800.jpeg'
  },
  {
    city: 'Cluj-Napoca',
    country: 'Romania',
    title: 'Where is Perry? Bring your own Summer Invention to life!',
    dates: '27 July - 3 August 2026',
    fee: '70.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=i4afz2d',
    img: 'https://cdn.britannica.com/09/226309-050-F0352A58/City-of-Cluj-Napoca-in-Romania.jpg'
  },
  {
    city: 'Belgrade',
    country: 'Serbia',
    title: 'The Alchemy of Startup Creation: Turn Your Idea into Gold!',
    dates: '8 - 15 August 2026',
    fee: '60.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=g59bx3h',
    img: 'https://lp-cms-production.imgix.net/2023-03/shutterstockRF_383722246.jpg'
  },
  {
    city: 'Prague',
    country: 'Czech Republic',
    title: 'Hash me if you can: Blockchain most wanted',
    dates: '14 - 23 August 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=k3bk11v',
    img: 'https://www.gokitetours.com/wp-content/uploads/2025/01/Top-10-Must-See-Tourist-Attractions-in-Prague-Czech-Republic.webp'
  },
  {
    city: 'Ljubljana',
    country: 'Slovenia',
    title: 'Solving Cold Cases in the Genome: Mystery of Gene and Cell Therapies',
    dates: '24 - 31 August 2026',
    fee: '80.0€',
    link: 'https://best-eu.org/event/details.jsp?activity=m2co30y',
    img: 'https://images.goway.com/production/hero_image/Ljubljana_Slovenia_AdobeStock_262853364.jpeg'
  }
]);

const wallPhotos = ref([
  'PIQ_0381.JPG',
  'PIQ_0461.JPG',
  'PIQ_9483.jpg',
  'PIQ_9533.jpg',
  'PIQ_9687.jpg',
  'PIQ_9925.jpg',
]);

const activeTab = ref('cine');

const aplicareContent = {
  cine: {
    title: "Cine poate aplica?",
    text: "Orice student din cadrul Universităţii Transilvania poate aplica la cursurile de sezon BEST. Dacă este în an terminal, acesta trebuie să fie student doar în momentul aplicării.",
    rules: [
      "Maxim 3 cursuri BEST (BEST Courses)",
      "Maxim 3 evenimente despre educație (Symposium on Education)",
      "Maxim 2 cursuri BEST în sezoanele de vară",
      "Maxim 1 curs BEST pe sezon"
    ]
  },
  cum: {
    title: "Procedura de Aplicare",
    steps: [
      "Creează cont pe www.best.eu.org",
      "Scrie o scrisoare de motivație (Motivation Letter)",
      "Răspunde la întrebările specifice cursului",
      "Contactează-ne pentru validarea contului",
      "Plătește depozitul de 40€ (returnabil) după acceptare"
    ]
  },
  motivație: {
    title: "Scrisoarea de Motivație",
    tips: "Organizatorii vor să știe: Cine ești? De ce acest curs? De ce acest oraș? Fii creativ, adaugă puțin umor și evită scrisorile standard!"
  }
};

const faqs = ref([
  { question: "Care este taxa pentru români?", answer: "Participanții români plătesc doar 60% din taxa cursului ales pentru a face educația mai accesibilă.", open: false },
  { question: "De ce sunt prețurile atât de mici?", answer: "Datorită parteneriatelor cu universitățile și companiile locale care subvenționează costurile pentru studenți.", open: false },
  { question: "Primesc credite ECTS?", answer: "Da, vei primi un certificat BEST semnat de profesorul coordonator care include numărul de credite ECTS alocat.", open: false },
  { question: "Cum se face selecția?", answer: "Se bazează pe scrisoarea de motivație, diversitate geografică și experiența anterioară în domeniu.", open: false },
  { question: "Pot aplica dacă nu am experiență?", answer: "Da! Cursurile BEST sunt concepute pentru studenți de toate nivelele. Motivația contează cel mai mult!", open: false },
  { question: "Ce include taxa?", answer: "Taxa acoperă cazarea, 3 mese pe zi și transportul în timpul evenimentului, plus activitățile sociale.", open: false },
  { question: "Cum îmi scriu scrisoarea de intenție?", answer: "Fii creativ și sincer! Spune-ne de ce vrei să mergi acolo și ce aduci unic în grup.", open: false },
  { question: "Trebuie să fiu membru BEST?", answer: "Nu, cursurile sunt deschise pentru toți studenții din universitatea noastră.", open: false },
]);

const openModal = (course) => {
  currentModalData.value = course;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const checklistItems = ref([
  { icon: 'fa-solid fa-passport', text: 'Pașaport/ID', checked: false },
  { icon: 'fa-solid fa-utensils', text: 'Mâncare Tradițională', checked: false },
  { icon: 'fa-solid fa-bottle-water', text: 'Apă', checked: false },
  { icon: 'fa-solid fa-camera', text: 'Cameră Foto', checked: false },
  { icon: 'fa-solid fa-flag', text: 'Steag RO', checked: false },
  { icon: 'fa-solid fa-face-smile-wink', text: 'Good Mood', checked: false },
]);

const toggleCheck = (index) => {
  checklistItems.value[index].checked = !checklistItems.value[index].checked;
};

onMounted(() => {
  AOS.init({ duration: 1000, once: true });

  if (tiltElements.value.length) {
    VanillaTilt.init(tiltElements.value);
  }

  new Typed(typedText.value, {
    strings: ['Travel.', 'Learn.', 'Party.', 'Explore.', 'BEST.'],
    typeSpeed: 80, backSpeed: 50, loop: true
  });

  new Swiper(".mySwiper", {
    effect: "coverflow",
    grabCursor: true,
    centeredSlides: true,
    slidesPerView: "auto",
    initialSlide: 1,
    coverflowEffect: {
      rotate: 30, stretch: 0, depth: 200, modifier: 1, slideShadows: true,
    },
    pagination: { el: ".swiper-pagination" },
    autoplay: { delay: 3000, disableOnInteraction: false },
  });

  const createPetals = () => {
    const container = sakuraContainer.value;
    if(!container) return;

    const petalCount = 40;
    for (let i = 0; i < petalCount; i++) {
      const petal = document.createElement('div');
      petal.classList.add('petal');

      const startLeft = Math.random() * 100;
      const duration = Math.random() * 5 + 6;
      const delay = Math.random() * 5;
      const size = Math.random() * 15 + 10;

      petal.style.left = startLeft + 'vw';
      petal.style.width = size + 'px';
      petal.style.height = size + 'px';
      petal.style.animationDuration = duration + 's';
      petal.style.animationDelay = delay + 's';

      petal.style.position = 'absolute';
      petal.style.background = '#ff9a9e';
      petal.style.borderRadius = '150% 0 150% 0';
      petal.style.top = '-10%';

      container.appendChild(petal);
    }
  };
  createPetals();

  const hoverElements = document.querySelectorAll('.mouse-hover');
  window.addEventListener('mousemove', (e) => {
    const posX = e.clientX;
    const posY = e.clientY;
    if(cursorDot.value) {
      cursorDot.value.style.left = `${posX}px`;
      cursorDot.value.style.top = `${posY}px`;
    }
    if(cursorOutline.value) {
      cursorOutline.value.animate({ left: `${posX}px`, top: `${posY}px` }, { duration: 500, fill: "forwards" });
    }
  });

  hoverElements.forEach(el => {
    el.addEventListener('mouseenter', () => document.body.classList.add('hovering'));
    el.addEventListener('mouseleave', () => document.body.classList.remove('hovering'));
  });
});
</script>

<style>
:root {
  --pink-pop: #ff9a9e;
  --pink-soft: #fad0c4;
  --blue-sky: #a18cd1;
  --blue-soft: #fbc2eb;
  --accent-gold: #ffdd00;
  --text-main: #2d3748;
  --white: #ffffff;
  --shadow-pop: 0 20px 40px -5px rgba(0, 0, 0, 0.1), 0 10px 20px -6px rgba(0, 0, 0, 0.05);
  --radius-blob: 30px;
}

* { margin: 0; padding: 0; box-sizing: border-box; cursor: auto; }

html, body {
  width: 100%;
  overflow-x: hidden;
  font-family: 'Nunito', sans-serif;
  color: var(--text-main);
  line-height: 1.6;
}

.landing-container {
  background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
  min-height: 100vh;
  width: 100%;
  position: relative;
  overflow: hidden;
}

#sakura-container {
  position: fixed;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  z-index: 999;
  pointer-events: none;
  overflow: hidden;
}

.petal {
  position: absolute;
  top: -10%;
  background: var(--pink-pop);
  border-radius: 150% 0 150% 0;
  opacity: 0.8;
  animation: fall linear infinite;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  z-index: 999;
}

@keyframes fall {
  0% { top: -10%; transform: translateX(0) rotate(0deg); opacity: 0; }
  20% { opacity: 1; }
  100% { top: 110%; transform: translateX(50px) rotate(360deg); opacity: 0; }
}

.side-decorations {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  pointer-events: none; z-index: 1;
}

.deco-lantern {
  position: absolute; width: 40px; height: 60px;
  animation: floatLantern 5s ease-in-out infinite;
}

.footer-socials {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.social-icon {
  font-size: 1.8rem;
  color: var(--text-main);
  transition: all 0.3s ease;
  opacity: 0.7;
  text-decoration: none;
}

.social-icon:hover {
  opacity: 1;
  transform: translateY(-5px);
}

.social-icon .fa-instagram:hover {
  color: #E1306C;
}

.social-icon .fa-facebook-f:hover {
  color: #1877F2;
}

.lantern-body {
  width: 100%; height: 100%; background: var(--pink-pop);
  border-radius: 10px; opacity: 0.7; box-shadow: 0 5px 15px rgba(255, 154, 158, 0.4);
}
.lantern-string {
  position: absolute; top: -100px; left: 50%; width: 2px; height: 100px;
  background: #ccc; transform: translateX(-50%);
}
.left-lantern { top: 30%; left: 3%; }
.right-lantern { top: 60%; right: 3%; animation-delay: 1s; }

@keyframes floatLantern {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

.paper-plane {
  position: absolute; top: 20%; left: -50px;
  font-size: 2rem; color: var(--blue-sky); opacity: 0.6;
  animation: flyPlane 15s linear infinite;
}
@keyframes flyPlane {
  0% { transform: translate(-50px, 0) rotate(10deg); }
  100% { transform: translate(110vw, 20vh) rotate(20deg); }
}

@media (max-width: 1024px) {
  .side-decorations { display: none; }
}

.cursor-dot, .cursor-outline {
  display: none;
  position: fixed; top: 0; left: 0;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  z-index: 10000;
  pointer-events: none;
}
.cursor-dot { width: 8px; height: 8px; background-color: var(--pink-pop); }
.cursor-outline {
  width: 40px; height: 40px;
  border: 2px solid var(--pink-pop);
  transition: width 0.2s, height 0.2s, background-color 0.2s;
}
:global(body.hovering) .cursor-outline {
  width: 60px; height: 60px;
  background-color: rgba(255, 154, 158, 0.1);
  border-color: transparent;
}

h1, h2, h3, h4 { font-family: 'Fredoka', sans-serif; font-weight: 700; }
.highlight { color: var(--pink-pop); }
.section-padding { padding: 120px 8%; position: relative; z-index: 2;}
.text-center { text-align: center; }
h2 { font-size: 3rem; margin-bottom: 40px; letter-spacing: -1px; color: #1a202c; }

.btn-pop {
  display: inline-block; padding: 16px 45px;
  background: linear-gradient(45deg, var(--pink-pop), #ec77ab);
  color: white; border-radius: 50px; font-weight: 700;
  text-decoration: none; box-shadow: 0 10px 25px rgba(255, 154, 158, 0.4);
  transition: all 0.3s; border: none; font-family: 'Fredoka', sans-serif;
  font-size: 1.1rem; cursor: pointer; letter-spacing: 0.5px;
}
.btn-pop:hover { transform: translateY(-3px) scale(1.02); box-shadow: 0 15px 30px rgba(255, 154, 158, 0.6); }

nav {
  display: flex; justify-content: space-between; align-items: center;
  padding: 15px 5%; position: fixed; width: 90%; left: 5%; top: 20px;
  border-radius: 50px; background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(15px); box-shadow: var(--shadow-pop);
  z-index: 1000; border: 1px solid rgba(255,255,255,0.8);
}
.logo { font-size: 1.5rem; font-weight: 800; color: var(--text-main); letter-spacing: -0.5px; }
.nav-links a { margin-left: 25px; text-decoration: none; color: var(--text-main); font-weight: 700; transition: 0.3s; font-size: 1rem;}
.nav-links a:hover { color: var(--pink-pop); }

.hero {
  min-height: 100vh; display: flex; flex-direction: column;
  justify-content: center; align-items: center; text-align: center;
  position: relative; padding-top: 80px; z-index: 1;
}
.hero h1 { font-size: 5rem; margin-bottom: 25px; line-height: 1.1; letter-spacing: -2px; font-weight: 800; }
.hero p { font-size: 1.25rem; opacity: 0.8; max-width: 600px; margin: 0 auto; }
.blob-bg {
  position: absolute; filter: blur(90px); z-index: -1; opacity: 0.5;
  animation: floatBlob 10s infinite alternate;
}
@keyframes floatBlob { from { transform: translate(0,0); } to { transform: translate(30px, -30px); }}

.stats-bar {
  display: flex; justify-content: center; gap: 50px; flex-wrap: wrap;
  padding: 40px; background: rgba(255,255,255,0.6); backdrop-filter: blur(10px);
  margin: 0 10%; border-radius: 30px; box-shadow: 0 10px 30px rgba(0,0,0,0.05);
  transform: translateY(-50px); z-index: 5; position: relative;
}
.stat-item { text-align: center; }
.stat-item h3 { font-size: 2.5rem; color: var(--blue-sky); margin-bottom: 5px; }
.stat-item p { font-weight: 700; text-transform: uppercase; letter-spacing: 1px; font-size: 0.9rem; opacity: 0.7; }

.card-container {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px; padding: 20px;
}
.tilt-card {
  background: var(--white); border-radius: var(--radius-blob); padding: 40px 30px;
  box-shadow: var(--shadow-pop); transform-style: preserve-3d;
  transform: perspective(1000px); text-align: center;
  border: 1px solid rgba(255,255,255,0.5);
}
.tilt-icon { font-size: 3.5rem; margin-bottom: 25px; transform: translateZ(30px); display: inline-block; }
.tilt-card h3 { font-size: 1.5rem; margin-bottom: 15px; }
.tilt-card p { opacity: 0.7; }

.swiper { width: 100%; padding-top: 50px; padding-bottom: 60px; }
.swiper-slide {
  background-position: center; background-size: cover;
  width: 340px; height: 500px; border-radius: 35px;
  overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.25);
  position: relative; transition: 0.3s;
}
.swiper-slide:hover { transform: scale(1.02); }
.slide-content {
  position: absolute; bottom: 0; left: 0; width: 100%;
  padding: 40px 25px;
  background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.6) 50%, transparent 100%);
  color: white; transform: translateY(10px); transition: 0.4s;
}
.swiper-slide:hover .slide-content { transform: translateY(0); }
.badge { background: var(--accent-gold); color: black; padding: 6px 14px; border-radius: 20px; font-weight: 800; font-size: 0.75rem; display: inline-block; margin-bottom: 10px; text-transform: uppercase; letter-spacing: 1px;}

.process-container { display: flex; justify-content: center; align-items: center; gap: 30px; flex-wrap: wrap; text-align: center; }
.process-step { flex: 1; min-width: 250px; padding: 20px; }
.step-num {
  width: 60px; height: 60px; background: var(--pink-pop); color: white;
  border-radius: 50%; display: flex; align-items: center; justify-content: center;
  font-size: 1.5rem; font-weight: 800; margin: 0 auto 20px;
  box-shadow: 0 10px 20px rgba(255, 154, 158, 0.4);
}
.process-line { width: 100px; height: 4px; background: #eee; border-radius: 2px; }

@media (max-width: 768px) {
  .process-line { display: none; }
  .process-container { flex-direction: column; gap: 50px; }
}

.faq-container { max-width: 800px; margin: 0 auto; display: flex; flex-direction: column; gap: 20px; }
.faq-item {
  background: white; border-radius: 20px; overflow: hidden;
  box-shadow: 0 5px 15px rgba(0,0,0,0.05); transition: 0.3s;
  border: 1px solid #f0f0f0;
}
.faq-question {
  padding: 25px; display: flex; justify-content: space-between; align-items: center;
  cursor: pointer; background: #fff;
}
.faq-question h4 { margin: 0; font-size: 1.1rem; }
.faq-answer { padding: 0 25px 25px; color: #666; display: none; }
.faq-item.open .faq-answer { display: block; animation: fadeIn 0.3s; }
.faq-item.open .faq-question { color: var(--pink-pop); }
.faq-item.open i { transform: rotate(180deg); transition: 0.3s; }

@keyframes fadeIn { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }

.modal-overlay {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(40, 40, 40, 0.6); backdrop-filter: blur(10px);
  z-index: 9999; display: flex; justify-content: center; align-items: center;
  transition: 0.4s ease;
}
.modal-content {
  background: white; width: 90%; max-width: 550px;
  border-radius: 40px; padding: 40px;
  box-shadow: 0 30px 60px rgba(0,0,0,0.3);
  text-align: center; position: relative; border: none;
}
.modal-close {
  position: absolute; top: 20px; right: 20px;
  background: #f1f1f1; color: #333;
  width: 40px; height: 40px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem; cursor: pointer; transition: 0.3s;
}
.modal-close:hover { background: var(--pink-pop); color: white; transform: rotate(90deg); }
.modal-img {
  width: 100%; height: 250px; object-fit: cover;
  border-radius: 25px; margin-bottom: 25px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.15);
}
.modal-title { color: var(--text-main); font-size: 2.2rem; margin-bottom: 10px; }
.modal-desc { color: #666; font-size: 1.05rem; line-height: 1.7; margin-bottom: 30px; }
.modal-header-info { display: flex; justify-content: center; gap: 10px; margin-bottom: 15px; }

.checklist-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 25px; margin-top: 40px; }
.check-item {
  background: white; padding: 25px; border-radius: 25px; text-align: center;
  box-shadow: 0 10px 20px rgba(0,0,0,0.05); transition: 0.3s; border: 2px solid transparent;
}
.check-item.checked { border-color: #4ade80; background: #f0fdf4; transform: scale(0.95); }
.check-item i { font-size: 2.2rem; margin-bottom: 15px; color: var(--blue-sky); }
.check-item p { font-weight: 600; }

.responsible-wrapper { display: flex; justify-content: center; margin-top: 30px; }
.responsible-card {
  display: flex; align-items: center; background: white;
  padding: 40px; border-radius: 40px; max-width: 800px; width: 100%;
  box-shadow: var(--shadow-pop); border: 2px solid var(--pink-soft);
  gap: 40px; transition: 0.3s;
}
.responsible-card:hover { transform: translateY(-5px); box-shadow: 0 20px 40px rgba(255, 154, 158, 0.2); }
.resp-img { width: 180px; height: 180px; border-radius: 50%; object-fit: cover; border: 5px solid var(--pink-pop); }
.resp-content { text-align: left; }
.resp-content h3 { font-size: 2rem; color: var(--text-main); margin-bottom: 5px; }
.resp-role { color: var(--pink-pop); font-weight: 800; text-transform: uppercase; font-size: 0.9rem; letter-spacing: 1px; }
.resp-content p { margin-top: 15px; opacity: 0.8; }
.resp-socials { margin-top: 20px; font-size: 1.5rem; color: #aaa; }
.resp-socials i { margin-right: 15px; transition: 0.3s; cursor: pointer; }
.resp-socials i:hover { color: var(--blue-sky); }

@media(max-width: 768px) {
  .responsible-card { flex-direction: column; text-align: center; }
  .resp-content { text-align: center; }
}

.gallery-wrapper { column-count: 3; column-gap: 25px; }
.gallery-img {
  width: 100%; border-radius: 25px; margin-bottom: 25px;
  transition: transform 0.4s ease; box-shadow: var(--shadow-pop);
  filter: grayscale(20%);
}
.gallery-img:hover { transform: scale(1.03); filter: grayscale(0%); z-index: 2; position: relative;}

.contact-box {
  background: var(--white); border-radius: 40px; box-shadow: var(--shadow-pop);
  overflow: hidden; display: flex; flex-wrap: wrap; position: relative;
}
.contact-info { flex: 1; padding: 60px; background: linear-gradient(135deg, var(--blue-sky), #8fd3f4); color: white; display: flex; flex-direction: column; justify-content: center; }
.contact-info h3 { font-size: 2.5rem; margin-bottom: 10px; }
.contact-form { flex: 1.5; padding: 60px; }
input, textarea {
  width: 100%; padding: 18px 25px; margin-bottom: 25px;
  border: 2px solid #f0f0f0; border-radius: 18px; background: #fcfcfc; outline: none; transition: 0.3s;
  font-family: inherit;
}
input:focus, textarea:focus { border-color: var(--pink-pop); background: white; }

@media (max-width: 768px) {
  .gallery-wrapper { column-count: 1; }
  .hero h1 { font-size: 3rem; }
  .section-padding { padding: 80px 5%; }
  nav { width: 95%; left: 2.5%; padding: 15px; }
  .nav-links { display: none; }
  .contact-box { flex-direction: column; }
  .stats-bar { gap: 30px; }
}

.tabs-header {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}

.tabs-header button {
  padding: 12px 25px;
  border-radius: 30px;
  border: 2px solid var(--pink-soft);
  background: white;
  font-weight: 700;
  transition: 0.3s;
}

.tabs-header button.active {
  background: var(--pink-pop);
  color: white;
  border-color: var(--pink-pop);
  box-shadow: 0 5px 15px rgba(255, 154, 158, 0.4);
}

.tab-content {
  background: white;
  padding: 50px;
  border-radius: 40px;
  box-shadow: var(--shadow-pop);
  min-height: 300px;
}

.styled-list {
  list-style: none;
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.styled-list li::before {
  content: '✦';
  color: var(--pink-pop);
  margin-right: 10px;
  font-weight: bold;
}

.rules-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
}

.rule-card {
  background: white;
  padding: 30px;
  border-radius: 30px;
  box-shadow: var(--shadow-pop);
}

.rule-card ul { list-style: none; }
.rule-card li { margin-bottom: 15px; display: flex; align-items: center; gap: 10px; }

.tip-box {
  background: #fff8e1;
  padding: 20px;
  border-radius: 20px;
  margin-top: 20px;
  border-left: 5px solid var(--accent-gold);
}

@media (max-width: 768px) {
  .rules-grid { grid-template-columns: 1fr; }
  .tab-content { padding: 30px 20px; }
}
</style>