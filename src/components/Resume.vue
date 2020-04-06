<template>
  <div class="root rootWraper" ref="resume">
    <button @click="$emit('close')">close</button>
    <main class="content contentScrollable">
      <section class="section">
        <h1 class="head-title">Обо мне</h1>

        <article class="about-article">
          <p class="paragraph">Я программист-самоучка. Вошел в разработку в 2013, активно начал заниматься с 2015.
          </p>
          <p class="paragraph">В 2013 окончил курсы по web-дизайну. После этого немного фрилансил. Затем был
            перерыв на 2 года.</p>
          <p class="paragraph">В 2015 меня взяли младшим разработчиком в Beta Digital Production, где я сильно
            вырос. Получил опыт проектирования интерфейсов, приобрел чувство стиля в сайтах, научился чувствовать
            анимацию.</p>
          <p class="paragraph">В 2018 я перешел работать в OZON. На тот момент он переезжал на новые рельсы. И я в
            участвовал в переезде с самого начала. Приобрел опыт продуктовой разработки больших и запутанных систем.
            Понял как происходит разработка с кучей зависимостей и согласований.</p>
          <p class="paragraph">В разные моменты жизни пытался запустить запустить свои проекты. На последнем проекте
            спроектировал интерфейс, спроектировал базу, написал бэкенд на node, фронт на vue, задеплоил все на хостинге.
            Получил представление и опыт о полном цикле разработки.</p>
          <p class="paragraph">Куда хочу двигаться?<br>Последнее время все больше начал смотреть в сторону
            управления. Хочется продумывать и развивать продукты. Планирую дальше расти как технический менеджер.</p>
        </article>
      </section>
      <section class="section">
         <picture class="avatar">
            <source srcset="./../assets/mock.jpeg" type="image/jpeg" class="avatar-source" />
            <img src="./../assets/mock.jpeg" alt="Pavel Gonzales Avatar" class="avatar-source" />
          </picture>
        <ul class="social-list">
          <li class="social-item">
            <a href="mailto:develop.gonzales@gmail.com" target="_blank">
              <img src="./../assets/icons/google.svg" alt="gmail" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="https://www.linkedin.com/in/pavelgonzales/" target="_blank">
              <img src="./../assets/icons/linkedin.svg" alt="linkedin" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="https://www.facebook.com/develop.gonzales" target="_blank">
              <img src="./../assets/icons/facebook.svg" alt="facebook" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="https://www.instagram.com/pavelgonzales/" target="_blank">
              <img src="./../assets/icons/instagram.svg" alt="instagram" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="https://medium.com/@pavelgonzales" target="_blank">
              <img src="./../assets/icons/medium.svg" alt="medium" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="https://github.com/PavelGonzales" target="_blank">
              <img src="./../assets/icons/github.svg" alt="github" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="tg://resolve?domain=pavelgonzales" target="_blank">
              <img src="./../assets/icons/telegram.svg" alt="telegram" class="social-img">
            </a>
          </li>
          <li class="social-item">
            <a href="/pavel-gonzales.pdf" target="_blank">
              <img src="./../assets/icons/download.svg" alt="download" class="social-img">
            </a>
          </li>
        </ul>
      </section>
    </main>
  </div>
</template>

<script>
// TODO сделать реверсивную рамку как на главной, что бы вместо бордера там был видосик и подумать как анимировать
/* eslint-disable */
import { TimelineMax, TweenLite, Power4 } from 'gsap'

export default {
  name: 'Resume',
}
</script>

<style scoped>
.root {
  position: fixed;
  top: 15px;
  left: 15px;
  width: calc(100vw - 30px);
  height: calc(100vh - 30px);
  z-index: 1;
  background-color: #fff;
  overflow-y: auto;
}

.content {
  padding: 50px 16px;
}

.resumeContent {
  position: absolute;
  top: 0px;
}

.avatar {
  width: calc(50vw - 32px);
  display: block;
  margin-right: 16px;
}

.avatar-source {
  width: 100%;
  height: 100%;
}

.head-title {
  font-size: 100px;
  margin: 0;
}

.about-article {
  position: relative;
  width: calc(100% / 3 * 2);
  column-count: 2;
  margin-left: auto;
  margin-top: 46px;
}

.section {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 46px;
}

.paragraph {
  font-size: 24px;
  margin-top: 0;
}

.social-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.social-item {
  width: 50px;
}

.social-img {
  width: 100%;
  height: 100%;
}
</style>
