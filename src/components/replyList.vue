<template>
  <div>
    <div class="container">
      <div class="avatar">
        <router-link
          :to="{ name: 'user-tweets', params: { id: reply.UserId } }"
        >
          <img :src="reply.avatar | emptyImage" alt="" class="avatar__pic" />
        </router-link>
      </div>
      <div class="tweet-content">
        <div class="title">
          <router-link
            :to="{ name: 'user-tweets', params: { id: reply.UserId } }"
            class="title__name"
            >{{ reply.name }}</router-link
          >
          <router-link
            :to="{ name: 'user-tweets', params: { id: reply.UserId } }"
            class="title__id"
            >@{{ reply.UserId }}</router-link
          >
          <router-link to="" class="title__formNow"
            >．{{ reply.createdAt | fromNow }}</router-link
          >
        </div>
        <div class="hashtag">
          <router-link to="" class="hashtag__reply">回覆</router-link>
          <router-link to="" class="hashtag__userid">@{{ name }}</router-link>
        </div>
        <p class="description">{{ reply.comment }}</p>
      </div>
    </div>
  </div>
</template>
<script>
import moment from "moment";
import { emptyImageFilter } from "../utils/mixins";
//換moment語言到中文
moment.locale("zh-tw");
export default {
  mixins: [emptyImageFilter],
  props: {
    reply: {
      type: Object,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
  },
  filters: {
    fromNow(dateTime) {
      return dateTime ? moment(dateTime).fromNow() : "-";
    },
  },
};
</script>
<style lang="scss" scoped>
.container {
  width: 600px;
  min-height: 100px;
  display: flex;
  border-top: 1px #e6ecf0 solid;
  margin-bottom: 5px;
  .description {
    word-break: break-all;
    font-size: 15px;
  }
  .tweet-content {
    display: flex;
    flex-direction: column;
    margin-top: 15px;
    .title {
      margin-bottom: 6px;
      font-size: 15px;
      display: flex;
      &__name {
        color: #1c1c1c;
        margin-right: 5px;
        font-weight: bold;
      }
      &__id,
      &__formNow {
        color: #657786;
        font-weight: 500;
      }
    }
  }
  .avatar {
    .avatar__pic {
      margin-right: 10px;
      margin-top: 15px;
      margin-left: 10px;
      height: 50px;
      width: 50px;
      border-radius: 100%;
    }
  }
  .hashtag {
    font-size: 15px;
    margin: 0 0 5px 0;
    &__reply {
      color: #657786;
    }
    &__userid {
      color: #ff6600;
    }
  }
}
</style>