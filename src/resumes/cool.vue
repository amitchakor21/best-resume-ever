<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div v-if="person.birth" class="banner__location">{{ lang.born }} {{person.birth.year}} {{ lang.bornIn }} {{person.birth.location}}</div>
    </div>

    <div class="content">
      <div class="content__left">
        <div class="section">
          <div class="section-headline">
            {{ lang.about }}
          </div>

          <div class="section-content section-content--plain section-text-justified">
            {{ person.about }}
            <br/>
            <br/>
            {{ person.knowledge }}
          </div>
        </div>

        <div
          v-if="person.skills"
          class="section">
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.skills"
              class="grid-item"
              :key="index"
              :class="{ link: skill.url !== undefined}"
              :href="skill.url">
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain">
            <a
              class="section-link link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <a
              v-if="person.contact.website"
              class="section-link link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>

            <a
              v-if="person.contact.linkedin"
              class="section-link link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>

            <a
              v-if="person.contact.github"
              class="section-link link"
              :href="contactLinks.github">
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>

            <a
              v-if="person.contact.medium"
              class="section-link link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>

          <div class="section-left">
            <div class="section-headline">
              <i class="section-headline__icon material-icons">book</i>{{ lang.courses }}
            </div>

            <div class="section-content-left">
              <a
                v-for="(course, index) in person.courses"
                class="section-content__item"
                :key="index"
                :class="{ link: course.url !== undefined}"
                :href="course.url">

                <span class="section-content__header"> {{ course.name }} </span>
                <span class="section-content__subheader">{{ course.degree }}</span>
                <span class="section-content__text italic-timeline">{{ course.timeperiod }}</span>
                <span class="section-content__text--light"> {{ course.description }} </span>
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="content__right">
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>

          <div class="section-content">
            <a
              v-for="(experience, index) in person.experience"
              :key="index"
              class="section-content__item"
              :class="{ link: experience.website !== undefined}"
              :href="experience.website">

              <div>
                <span class="section-content__header display-inline"> {{ experience.position }} </span>
                <span class="section-content__text display-inline italic-timeline"> {{ experience.timeperiod }} </span>
              </div>
              <span class="section-content__subheader">
                {{ experience.company }}
                <span class="section-content__plain">{{ experience.location }}</span>
              </span>
              <span class="section-content__text--light">{{ experience.description }}</span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>

          <div class="section-content">
            <a
              v-for="(education, index) in person.education"
              class="section-content__item"
              :key="index"
              :class="{ link: education.website !== undefined}"
              :href="education.website">

              <div>
                <span class="section-content__header display-inline"> {{ education.degree }} </span>
                <span class="section-content__text display-inline grade"> {{ education.grade }} </span>
                <span class="section-content__text display-inline italic-timeline"> {{ education.timeperiod }} </span>
              </div>
              <span class="section-content__subheader">{{ education.school }}</span>
              <span class="section-content__text--light"> {{ education.description }} </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.projects"
              class="section">
              <div class="section-headline">
                <i class="section-headline__icon material-icons">code</i>{{ lang.projects }}
              </div>

              <div class="section-content">
                <a v-for="(project, index) in person.projects" :key="index"
                   class="section-content__item"
                   :class="{ link: project.url !== undefined}"
                   :href="project.url">
                  <div>
                    <span class="section-content__header display-inline"> {{ project.name }} </span>
                    <span class="section-content__text display-inline italic-timeline"> {{ project.timeperiod }} </span>
                  </div>
                  <div class="section-content-grid-project-infra">
                <a
                  v-for="(platform, index) in project.platform.split(',')"
                  class="grid-item"
                  :key="index"
                  :class="{ link: platform.url !== undefined}"
                  :href="platform.url">
              <span class="squarred-grid-item-project-infra">
                {{ platform }}
              </span>
                </a>
              </div>
              <span class="section-content__text"> {{ project.description }} </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.contributions"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-heart"></i>{{lang.contributions}}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(contribution, index) in person.contributions"
              class="section-content__item-grid"
              :key="index"
              :class="{ link: contribution.url !== undefined}"
              :href="contribution.url">
              <span class="section-content__header"> {{ contribution.name }} </span>
              <span class="section-content__text"> {{ contribution.description }} </span>
              <span class="section-content__text--light" style="word-break: break-all;">
                {{ contribution.url }}
              </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.achievements"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-trophy"></i>{{lang.achievements}}
          </div>

          <div class="section-content">
            <a
              v-for="(contribution, index) in person.achievements"
              class="section-content__item"
              :key="index"
              :class="{ link: contribution.url !== undefined}"
              :href="contribution.url">
              <span class="section-content-achievement-header display-inline"> {{ contribution.name }} </span>
              <span class="section-content__text display-inline italic-timeline"> {{ contribution.timeperiod }} </span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'cool';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #34495E;
@banner-color: #42b883;
@banner-height: 65px;
@picture-size: 120px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

.link {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  /*
    background-image: url('../../resume/banner.png');
    background-repeat: no-repeat;
    background-size: cover;
  */
  color: white;

  &__fullname {
    font-size: 32px;
  }

  &__position {
    font-size: 16px;
  }

  &__location {
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 20px 0;
}

.section-left {
  margin: 30px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;

  &__icon {
    color: white;
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__item {
    display: block;
    margin-bottom: 8px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-left {
  margin-top: 5px;
  padding-left: 10px;
  font-size: 14px;

  &__item {
    display: block;
    margin-bottom: 8px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-achievement-header{
  display: block;
  font-size: 0.9em;
  font-weight: 400;
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
}

.section-content-grid-project-infra {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 3px;
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  border-radius: 4px;
  color: white;
  margin-top: 5px;
  padding: 4px;
}

.squarred-grid-item-project-infra {
  display: block;
  border: 1px solid black;
  border-radius: 3px;
  color: black;
  margin-top: 2px;
  padding: 2px;
  font-size: 9px;
}

.display-inline {
  display: inline;
}

.italic-timeline {
  font-weight: 300;
  font-style: italic;
}

.grade{
  font-weight: 400;
  font-style: normal;
}

.section-text-justified{
  text-align: justify;
}
</style>
