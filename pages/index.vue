<template>
  <div>
    <div class="root">
      <section class="cover">
        <h1 class="cover__title">#раклечится</h1>
        <img class="cover__arrow" src="../static/images/arrow_down.svg" />
      </section>

      <section class="video">
        <container>
          <div class="two-column-content video__container">
            <div class="video__text">
              <section-title>
                Истории людей, победивших рак, но не свои привычки
              </section-title>
              <section-subtitle>
                Есть вещи, которые не лечатся. Вещи ставшие частью нашего «я»,
                фобии, страхи. Но это точно не рак. Рак лечится. Лучшее
                доказательство&nbsp;— люди с их историями.
              </section-subtitle>
              <div class="slider-button-container">
                <button
                  aria-label="Previous video"
                  type="button"
                  class="slider-button slider-button_previous"
                ></button>
                <button
                  aria-label="Next video"
                  type="button"
                  class="slider-button slider-button_next"
                ></button>
              </div>
            </div>
            <div class="video__content">
              <rak-slider :videos="videos" />
            </div>
            <p class="video__description">
              Все видео вы можете найте на нашем
              <a
                class="video__link"
                href="https://www.youtube.com/results?search_query=%23%D1%8D%D1%82%D0%BE%D0%BD%D0%B5%D0%BB%D0%B5%D1%87%D0%B8%D1%82%D1%81%D1%8F"
                >YouTube канале</a
              >.
            </p>
          </div>
          <banner theme="dark">
            <h2 class="banner__text">
              и в отличие от рака,
              <span class="important-text">#этонелечится</span>
            </h2>
          </banner>
        </container>
      </section>

      <section class="stories">
        <container>
          <section-title>Истории неизлечимых привычек</section-title>
          <div class="stories__cards-container">
            <card
              v-for="obj in getPieceOfStories"
              :key="obj.id"
              :source="obj"
            />
          </div>
          <nuxt-link to="/stories" class="link_underline_false">
            <banner theme="light"><span>Больше статей</span></banner>
          </nuxt-link>
        </container>
      </section>

      <section class="instagram">
        <container>
          <banner theme="dark">
            <h2 class="banner__text banner__text_wide">
              рассказывайте ваши истории в инстаграм <br />
              <span class="important-text">#этонелечится</span>
            </h2>
          </banner>
          <div class="two-column-content">
            <div class="instagram__text">
              <section-title>
                <a
                  class="title-link"
                  href="https://www.instagram.com/raklechitsa/"
                  target="_blank"
                  >Инстаграм
                </a>
              </section-title>
              <section-subtitle>
                Два раза в неделю мы просматриваем все посты по хештегу
                #этонелечится. Все истории, где нет нецензурных выражений и
                запрещенного контента попадают сюда. Следите за правильным
                написанием хештега, чтобы мы не пропустили вашу историю.
              </section-subtitle>
            </div>
            <div class="instagram__grid-container">
              <img
                v-for="obj in getPieceOfInstagram"
                :key="obj.id"
                :src="obj.img"
                alt="картинка из инстаграма"
                class="instagram__image"
              />
            </div>
          </div>
        </container>
      </section>

      <section class="your-story">
        <container>
          <div class="two-column-content">
            <div class="your-story__text">
              <section-title>Расскажите свою историю</section-title>
              <section-subtitle>
                Мы публикуем новые истории на сайте раз в неделю. Есть 2
                варианта поделиться своей историей неизлечимых привычек,
                навязчивых идей и болезненных привязанностей.
              </section-subtitle>
            </div>
            <nxt-options
              class="your-story__options"
              theme="light"
              type="form"
            />
          </div>
        </container>
      </section>

      <section class="statistics">
        <container>
          <section-title>Статистика по онкозаболеваниям</section-title>
          <div class="statistics__grid">
            <statistics-card
              v-for="obj in statistics"
              :key="obj.id"
              :data="obj"
            />
          </div>
        </container>
      </section>

      <section class="info">
        <container>
          <h2 class="info__title">#раклечится</h2>
          <div class="two-column-content">
            <div class="info__text">
              <section-title class="section-title_white"
                >О проекте</section-title
              >
              <section-subtitle class="section-subtitle_light">
                Этот проект был создан благотворительным фондом Константина
                Хабенского.
              </section-subtitle>
            </div>
            <nxt-options class="info__options" theme="dark" type="about" />
          </div>
        </container>
      </section>
    </div>
  </div>
</template>

<script>
import VideoIframe from '@/components/VideoIframe';
import VideoSlider from '@/components/VideoSlider';
import Banner from '@/components/Banner';
import Card from '@/components/Card';
import Button from '@/components/ui/Button';
import StatisticsCard from '@/components/StatisticsCard';
import WidthAdjustContainer from '@/components/WidthAdjustContainer';
import Options from '@/components/Options';
import SectionTitle from '@/components/ui/SectionTitle';
import SectionSubtitle from '@/components/ui/SectionSubtitle';
export default {
  components: {
    container: WidthAdjustContainer,
    'section-title': SectionTitle,
    'section-subtitle': SectionSubtitle,
    'rak-video': VideoIframe,
    'rak-slider': VideoSlider,
    banner: Banner,
    card: Card,
    'rak-button': Button,
    'statistics-card': StatisticsCard,
    'nxt-options': Options,
  },
  computed: {
    videos() {
      return this.$store.getters['videos/getVideos'];
    },
    statistics() {
      return this.$store.getters['statistics/getStatistics'];
    },
    stories() {
      return this.$store.getters['stories/getStories'];
    },
    getPieceOfStories() {
      if (process.browser) {
        let copy = this.stories.slice(0);
        // console.log(window.innerWidth)
        let partOfStories = [];
        if (window.innerWidth <= 768) {
          this.storiesOnPage = 9;
        }
        if (window.innerWidth <= 425) {
          this.storiesOnPage = 6;
        }
        partOfStories = copy.splice(0, this.storiesOnPage);
        return partOfStories;
      }
    },
    getPieceOfInstagram() {
      if (process.browser) {
        let copy = this.stories.slice(0);
        // console.log(window.innerWidth)
        let partOfInstagram = [];
        partOfInstagram = copy.splice(0, this.instagramOnPage);
        return partOfInstagram;
      }
    },
  },
  data() {
    return {
      storiesOnPage: 8,
      instagramOnPage: 8,
    };
  },
};
</script>

<style scoped>
.root {
  width: 100vw;
}

.cover {
  width: 100vw;
  min-height: 689px;
  background: #613a93;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.cover__title {
  font-weight: 800;
  font-size: 92px;
  line-height: 111px;
  text-transform: uppercase;
  color: #fff;
}

.cover__arrow {
  align-self: center;
  position: absolute;
  left: calc(50% - (36px / 2));
  bottom: 40px;
}

.video__container {
  grid-row-gap: 10px;
}

.video__content {
  display: flex;
  overflow: hidden;
  flex-direction: column;
  margin-top: 100px;
}

.two-column-content {
  max-width: 1320px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 2.1fr;
  grid-column-gap: 40px;
  overflow: hidden;
}

.video__text {
  margin-top: 14px;
  display: flex;
  flex-direction: column;
}

.slider-button-container {
  display: flex;
  flex-direction: row;
  margin-top: auto;
  width: 80px;
  height: 40px;
  /* background: #fbfbfb; */
}

.slider-button {
  width: 40px;
  height: 40px;
  padding: 0;
  margin: 0;
  color: #000000;
  background: #fbfbfb;
  background-repeat: no-repeat;
  background-size: auto;
  background-position: 50% 50%;
  border: none;
  cursor: pointer;
}

.slider-button_previous {
  background-image: url('../static/images/arrow-enabled-right.svg');
  transform: rotate(180deg);
}

.slider-button_next {
  background-image: url('../static/images/arrow-enabled-right.svg');
}

.slider-button_disabled {
  opacity: 0.3;
}

.section-title_white {
  color: white;
}

.section-subtitle_light {
  color: #dedede;
}

.video__description {
  grid-row: 2;
  grid-column: 2;
  font-size: 12px;
  line-height: 16px;
  color: #666666;
}

.video__link {
  color: #666666;
}

.banner__text {
  max-width: 1000px;
  font-size: 30px;
  line-height: 46px;
  font-weight: 500;
  color: #ffffff;
  text-transform: uppercase;
  text-align: center;
  margin: 20px 0 13px;
}

.link_underline_false {
  text-decoration: none;
  color: inherit;
}

.important-text {
  font-weight: 800;
  font-size: 40px;
}

.stories__cards-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-column-gap: 40px;
  grid-row-gap: 70px;
  margin: 70px 0;
}

.title-link {
  display: inline-block;
  text-decoration: none;
  border-bottom: solid black 2px;
  color: inherit;
  transition: 0.3s ease;
}

.title-link:hover {
  color: #121212;
  opacity: 0.8;
  border-bottom-color: rgba(18, 18, 18, 0.8);
}

.instagram__grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 30px;
  margin: 100px 0;
}

.instagram__image {
  width: 100%;
}

.your-story {
  background: #f7f7f7;
  position: relative;
  display: block;
  margin-left: 50%;
  transform: translateX(-50%);
  min-height: 520px;
  width: 100vw;
  /* padding-top: 100px; */
}

.two-column-text {
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-column-gap: 40px;
  margin-top: 100px;
}

.two-column-text_light {
  margin-top: 68px;
}

.two-column-text__brief {
  text-align: right;
  font-weight: 500;
  font-size: 18px;
  line-height: 22px;
}

.two-column-text__brief_light {
  color: #dedede;
  max-width: 150px;
}

.two-column-text__main {
  font-size: 18px;
  line-height: 22px;
  color: #666666;
}

.two-column-text__main_light {
  color: #dedede;
  margin-bottom: 20px;
}

.two-column-text__main_light:last-of-type {
  margin-bottom: 0;
}

.your-story__button {
  margin-top: 80px;
}
.your-story__options {
  margin-top: 204px;
}
.statistics {
  margin-top: 100px;
}

.statistics__grid {
  margin: 70px 0 100px 0;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  column-gap: 40px;
}

.info {
  background: #613a93;
  position: relative;
  display: block;
  margin-left: 50%;
  transform: translateX(-50%);
  width: 100vw;
  min-height: 626px;
}

.info__text {
  position: relative;
  bottom: 100px;
}

.info__title {
  font-weight: 800;
  font-size: 64px;
  line-height: 77px;
  text-align: center;
  color: #ffffff;
  text-transform: uppercase;
  padding-top: 90px;
  margin-bottom: 70px;
}
.info__options {
  margin-top: 68px;
}

@media screen and (max-width: 1280px) {
  .cover {
    min-height: 620px;
  }

  .cover__title {
    font-size: 78px;
    line-height: 94px;
  }

  .video__content {
    margin-top: 90px;
  }

  .two-column-content {
    max-width: 1180px;
    grid-column-gap: 40px;
  }

  .video__text {
    margin-top: 10px;
  }

  .banner__text {
    font-size: 28px;
    line-height: 46px;
    font-weight: 500;
    word-spacing: 0.6;
  }

  .important-text {
    font-size: 38px;
  }

  .stories__cards-container {
    grid-row-gap: 60px;
    margin: 60px 0;
  }

  .instagram__text {
    margin-top: 10px;
  }

  .instagram__grid-container {
    grid-gap: 27px;
    margin: 91px 0;
    margin-left: 8px;
  }

  .your-story {
    min-height: 448px;
    width: 100vw;
  }

  .your-story__options {
    margin-top: 184px;
  }

  .statistics {
    margin-top: 90px;
  }

  .statistics__grid {
    margin: 60px 0 90px 0;
  }

  .info__title {
    font-weight: 800;
    font-size: 58px;
    line-height: 70px;
    padding-top: 80px;
    margin-bottom: 60px;
  }

  .info__text {
    bottom: 90px;
  }
}

@media screen and (max-width: 1024px) {
  .cover {
    min-height: 540px;
  }

  .video__content {
    margin-top: 80px;
  }

  .two-column-content {
    max-width: 1180px;
    grid-column-gap: 30px;
  }

  .video__text {
    margin-top: 10px;
  }

  .banner__text {
    font-size: 24px;
    line-height: 40px;
    font-weight: 400;
  }

  .important-text {
    font-size: 36px;
  }

  .stories__cards-container {
    grid-row-gap: 46px;
    grid-column-gap: 30px;
    margin: 46px 0;
  }

  .instagram__grid-container {
    grid-gap: 20px;
    margin: 79px 0;
  }

  .your-story {
    min-height: 436px;
  }

  .your-story__options {
    margin-top: 156px;
  }

  .statistics {
    margin-top: 80px;
  }

  .statistics__grid {
    margin: 46px 0 80px 0;
    grid-column-gap: 30px;
  }

  .info {
    min-height: 570px;
  }

  .info__title {
    font-weight: 800;
    font-size: 52px;
    line-height: 63px;
    margin-bottom: 46px;
  }

  .info__text {
    bottom: 80px;
  }

  .info__options {
    margin-top: 46px;
  }
}

@media screen and (max-width: 768px) {
  .cover {
    min-height: 780px;
  }

  .cover__title {
    font-size: 64px;
    line-height: 77px;
  }

  .two-column-content {
    margin: 0 auto;
    grid-template-columns: 1fr;
    grid-row-gap: 0;
    grid-template-rows: auto auto;
    position: relative;
  }
  .video__text {
    margin-top: 0px;
  }

  .video__description {
    grid-row: 3;
    grid-column: 1;
    margin: 20px auto 0;
    width: 580px;
  }

  .video__content {
    margin-top: 60px;
  }
  .slider-button-container {
    position: absolute;
    left: 0;
    top: 65.5%;
    width: 100%;
    justify-content: space-between;
  }

  .banner__text {
    max-width: 444px;
    margin: auto;
    font-size: 22px;
    line-height: 36px;
  }

  .banner__text_wide {
    max-width: 628px;
    line-height: 32px;
  }

  .important-text {
    font-size: 32px;
    font-weight: 800;
  }

  .stories__cards-container {
    grid-template-columns: 1fr 1fr 1fr;
    grid-column-gap: 20px;
    grid-row-gap: 40px;
    margin: 60px 0 0 0;
  }

  .instagram__text {
    margin-top: 0;
  }

  .instagram__grid-container {
    grid-gap: 20px;
    margin: 60px 0 80px;
  }

  .your-story__options {
    margin-top: 76px;
  }

  .statistics__grid {
    overflow-x: scroll;
    padding-bottom: 20px;
    margin: 60px 0;
    grid-column-gap: 20px;
  }

  .info__title {
    display: none;
  }

  .info__text {
    position: static;
    margin-bottom: 30px;
  }
}

@media screen and (max-width: 320px) {
  .cover {
    min-height: 480px;
  }

  .cover__title {
    font-size: 36px;
    line-height: 44px;
  }

  .cover__arrow {
    bottom: 30px;
  }

  .video__description {
    display: none;
  }

  .video__content {
    margin-top: 40px;
  }

  .slider-button-container {
    z-index: 5;
    top: 75%;
    justify-content: space-between;
  }

  .slider-button {
    width: 30px;
    height: 30px;
    opacity: 0.5;
  }

  .banner__text {
    font-size: 16px;
    line-height: 18px;
    letter-spacing: 1px;
  }

  .important-text {
    font-size: 22px;
    font-weight: 800;
  }

  .stories__cards-container {
    grid-template-columns: 1fr;
    grid-row-gap: 30px;
    margin-top: 40px;
  }

  .instagram__grid-container {
    grid-template-columns: 1fr 1fr;
    margin: 40px 0 50px;
    grid-gap: 10px;
  }

  .your-story__options {
    margin-top: 40px;
  }

  .statistics {
    margin-top: 50px;
  }

  .statistics__grid {
    margin: 30px 0;
    grid-column-gap: 10px;
  }

  .info__text {
    position: static;
    margin-bottom: 0;
    letter-spacing: -0.5px;
  }

  .info__options {
    margin-top: 40px;
  }
}
</style>
