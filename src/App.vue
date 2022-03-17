<template>
  <div class="flex h-screen w-full">
    <!--Side Navigation -->
    <div class="lg:w-1-5 border-r border-inherit px-2 lg:px-6 py-2">
      <div class="grid">
        <button
          class="
            h-12
            w-12
            hover:bg-sky-100
            text-3xl
            hover:border hover:border-sky-300 hover:rounded
            text-sky-300
            lg:place-self-auto
            place-self-center
          "
        >
          <box-icon type="logo" color="#7dd3fc" name="twitter"></box-icon>
        </button>
        <div>
          <button
            v-for="tab in tabs"
            @click="id = tab.id"
            :class="`focus:outline-none hover:text-sky-500 flex items-center py-2 px-4 hover:bg-zinc-100 rounded-full mr-auto mb-3 hover:fill-sky-500
           ${id === tab.id ? 'text-sky-500 fill-sky-500' : ''} `"
          >
            <box-icon
              :name="`${tab.name}`"
              size="sm"
              :type="`${tab.type}`"
            ></box-icon>
            <p class="text-lg font-sans text-left mx-2 hidden lg:block">
              {{ tab.title }}
            </p>
          </button>
        </div>
        <button
          class="
            text-white
            bg-sky-500
            rounded-full
            font-semibold
            focus:outline-none
            w-12
            h-12
            lg:w-full lg:h-auto
            p-3
            hover:bg-gradient-to-r hover:from-cyan-500 hover:to-blue-500
            lg:place-self-auto
            place-self-center
          "
        >
          <p class="hidden lg:block">Tweet</p>
          <box-icon name="plus" class="lg:hidden fill-zinc-300"></box-icon>
        </button>
      </div>
      <div class="lg:w-full relative">
        <button
          @click="dropdown = true"
          class="
            flex
            items-center
            w-full
            hover:bg-slate-100
            rounded-full
            my-3
            p-2
            focus:outline-none
          "
        >
          <img
            src="https://avatars.githubusercontent.com/u/43324519?v=4"
            alt="profile"
            class="w-10 h-10 rounded-full border border border-inherit"
          />
          <div class="hidden lg:block ml-4 px-1">
            <p class="text-xs whitespace-nowrap font-bold leading-tight">
              Mohsen Alizde
            </p>
            <p class="text-sm leading-tight text-slate-400">@maz.dev</p>
          </div>
          <box-icon
            name="chevron-down"
            class="ml-auto fill-zinc-500 hidden lg:block"
            size="sm"
          ></box-icon>
        </button>
        <div
          v-if="dropdown === true"
          class="
            absolute
            bottom-0
            left-0
            w-64
            rounded-lg
            shadow-md
            border border-inherit
            bg-stone-50
            mb-16
          "
        >
          <button
            @click="dropdown = false"
            class="
              flex
              items-center
              w-full
              hover:bg-sky-50
              rounded-full
              p-2
              focus:outline-none
            "
          >
            <img
              src="https://avatars.githubusercontent.com/u/43324519?v=4"
              alt="profile"
              class="w-10 h-10 rounded-full border border border-inherit"
            />
            <div class="ml-4">
              <p class="text-xs font-bold leading-tight">Mohsen Alizde</p>
              <p class="text-sm leading-tight text-slate-400">@maz.dev</p>
            </div>
            <box-icon
              name="check"
              class="ml-auto fill-blue-500"
              size="sm"
            ></box-icon>
          </button>
          <button
            @click="dropdown = false"
            class="
              w-full
              text-left
              hover:bg-stone-50
              border-t border-inherit
              p-3
              text-sm
            "
          >
            Add an existing account
          </button>
          <button
            @click="dropdown = false"
            class="
              w-full
              text-left
              hover:bg-stone-50
              border-t border-inherit
              p-3
              text-sm
            "
          >
            Log out @maz.dev
          </button>
        </div>
      </div>
    </div>
    <!--Tweets -->
    <div
      class="
        lg:w-1/2
        w-full
        h-full
        overflow-y-scroll
        scrollbar-thin scrollbar-thumb-sky-500 scrollbar-track-gray-100
      "
    >
      <div
        class="
          px-5
          py-3
          border-b border-inherit
          flex
          items-center
          justify-between
        "
      >
        <h1 class="text-xl font-bold">Home</h1>
        <box-icon name="star" class="fill-sky-500 text-xl"></box-icon>
      </div>
      <div class="px-5 py-3 border-b-8 border-inherit flex">
        <div class="flex-none">
          <img
            src="https://avatars.githubusercontent.com/u/43324519?v=4"
            alt="profile"
            class="flex-none w-12 h-12 rounded-full border border-inherit"
          />
        </div>
        <form v-on:submit.prevent="addNewTweet" class="w-full px-4 relative">
          <textarea
            v-model="tweet.content"
            name=""
            id=""
            placeholder="What's up?"
            class="mt-3 pb-3 w-full focus:outline-none font-sans"
          ></textarea>
          <div class="flex items-center fill-sky-400">
            <box-icon name="film" class="mr-4"></box-icon>
            <box-icon name="image-add" class="mr-4"></box-icon>
            <box-icon name="bar-chart-alt-2" class="mr-4"></box-icon>
            <box-icon name="smile" class="mr-4"></box-icon>
          </div>
          <button
            type="submit"
            class="
              h-10
              px-4
              text-white
              font-semibold
              bg-sky-400
              hover:bg-sky-600
              focus:outline-none
              font-sans
              rounded-full
              absolute
              bottom-0
              right-0
            "
          >
            Tweet
          </button>
        </form>
      </div>
      <div class="flex flex-col-reverse">
        <div
          v-for="tweet in tweets"
          class="w-full p-4 border-b hover:bg-slate-100 flex"
        >
          <div class="flex-none mr-4">
            <img
              src="https://avatars.githubusercontent.com/u/43324519?v=4"
              alt="profile"
              class="h-12 w-12 rounded-full flex-none"
            />
          </div>
          <div class="w-full">
            <div class="flex items-center w-full font-sans">
              <p class="font-semibold">maz.develop</p>
              <p class="text-sm text-slate-600 ml-1">@mazDev</p>
              <p class="text-sm text-slate-600 ml-1">2.5 hrs</p>
              <box-icon
                name="chevron-down"
                class="fill-slate-600 ml-auto"
              ></box-icon>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full font-sans">
              <div class="flex items-center text-sm text-slate-500">
                <box-icon
                  name="message-rounded"
                  class="mr-3 fill-slate-500"
                ></box-icon>
                <p class="">0</p>
              </div>
              <div class="flex items-center text-sm text-slate-500">
                <box-icon name="repost" class="mr-3 fill-slate-500"></box-icon>
                <p class="">1</p>
              </div>
              <div class="flex items-center text-sm text-slate-500">
                <box-icon
                  type="solid"
                  name="heart"
                  class="mr-3 fill-slate-500"
                ></box-icon>
                <p class="">0</p>
              </div>
              <div class="flex items-center text-sm text-slate-500">
                <box-icon
                  type="solid"
                  name="share"
                  class="mr-3 fill-slate-500"
                ></box-icon>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        v-for="follow in following"
        class="w-full p-4 border-b hover:bg-slate-100 flex"
      >
        <div class="flex-none mr-4">
          <img
            :src="`${follow.src}`"
            :alt="`${follow.name}`"
            class="h-12 w-12 rounded-full flex-none"
          />
        </div>
        <div class="w-full">
          <div class="flex items-center w-full font-sans">
            <p class="font-semibold">{{ follow.name }}</p>
            <p class="text-sm text-slate-600 ml-1">{{ follow.handle }}</p>
            <p class="text-sm text-slate-600 ml-1">{{ follow.time }}</p>
            <box-icon
              name="chevron-down"
              class="fill-slate-600 ml-auto"
            ></box-icon>
          </div>
          <p class="py-2">
            {{ follow.tweet }}
          </p>
          <div class="flex items-center justify-between w-full font-sans">
            <div class="flex items-center text-sm text-slate-500">
              <box-icon
                name="message-rounded"
                class="mr-3 fill-slate-500"
              ></box-icon>
              <p class="">{{ follow.comments }}</p>
            </div>
            <div class="flex items-center text-sm text-slate-500">
              <box-icon name="repost" class="mr-3 fill-slate-500"></box-icon>
              <p class="">{{ follow.retweet }}</p>
            </div>
            <div class="flex items-center text-sm text-slate-500">
              <box-icon
                type="solid"
                name="heart"
                class="mr-3 fill-slate-500"
              ></box-icon>
              <p class="">{{ follow.like }}</p>
            </div>
            <div class="flex items-center text-sm text-slate-500">
              <box-icon
                type="solid"
                name="share"
                class="mr-3 fill-slate-500"
              ></box-icon>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--Trending -->
    <div
      class="
        md:block
        hidden
        scrollbar-thin scrollbar-thumb-sky-500 scrollbar-track-gray-100
        w-1/3
        h-full
        border-l border-inherit
        py-2
        px-6
        overflow-y-scroll
        relative
      "
    >
      <input
        type="text"
        class="
          pl-12
          rounded-full
          w-full
          p-2
          bg-slate-100
          text-sm
          focus:outline-none
        "
        placeholder="Search Twitter"
      />
      <box-icon
        name="search-alt-2"
        class="absolute left-0 -top-1.5 mt-5 ml-12 text-sm"
      ></box-icon>
      <div class="w-full rounded-lg bg-slate-100 my-1">
        <div class="flex items-center justify-between p-3">
          <p class="text lg font-bold">Ternds For you</p>
          <box-icon name="cog" class="fill-slate-500"></box-icon>
        </div>
        <button
          v-for="trend in trending"
          class="
            w-full
            flex
            justify-between
            hover:bg-slate-50
            p-3
            border-t border-inherit
            font-sans
          "
        >
          <div>
            <p class="text-sm text-left leading-tight text-slate-500">
              {{ trend.top }}
            </p>
            <p class="font-bold text-left leading-tight">{{ trend.title }}</p>
            <p class="text-left leading-tight">{{ trend.bottom }}</p>
          </div>
          <box-icon name="chevron-down" class="fill-slate-600"></box-icon>
        </button>
        <button
          class="
            p-3
            w-full
            hover:bg-slate-50
            text-left text-sky-500
            font-sans
            border-t border-inherit
          "
        >
          Show more
        </button>
      </div>
      <div class="w-full rounded-lg bg-slate-100 my-4">
        <div class="p-3">
          <p class="text-lg font-bold font-sans">Who To Follow</p>
        </div>
        <button
          class="w-full flex hover:bg-slate-100 p-3 border-t border-inherit"
          v-for="friend in friends"
        >
          <img
            :src="`${friend.src}`"
            :alt="`${friend.name}`"
            class="w-12 h-12 rounded-full border border-inherit object-cover"
          />
          <div class="hidden lg:block ml-4">
            <p class="text-sm leading-tight font-bold">{{ friend.name }}</p>
            <p class="text-sm leading-tight">{{ friend.handle }}</p>
          </div>
          <button
            class="
              btn
              ml-auto
              font-sans
              text-sm text-sky-500
              py-1
              px-4
              rounded-full
              border-2 border-sky-500
            "
          >
            Follow
          </button>
        </button>
        <button
          class="
            p-3
            w-full
            hover:bg-slate-50
            text-left text-sky-500
            font-sans
            border-t border-inherit
          "
        >
          Show more
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tabs: [
        { name: 'home-alt', type: 'solid', id: 'home', title: 'Home' },
        { name: 'hash', type: 'solid', id: 'explore', title: 'Explore' },
        { name: 'bookmarks', type: '', id: 'bookmarks', title: 'Bookmarks' },
        {
          name: 'bell',
          type: '',
          id: 'notification',
          title: 'Notification',
        },
        {
          name: 'envelope',
          type: '',
          id: 'message',
          title: 'Message',
        },
        {
          name: 'list-ul',
          type: '',
          id: 'list',
          title: 'List',
        },
        {
          name: 'user',
          type: '',
          id: 'profile',
          title: 'Profile',
        },
        {
          name: 'dots-horizontal-rounded',
          type: '',
          id: 'more',
          title: 'More',
        },
      ],
      id: 'home',
      dropdown: false,
      trending: [
        {
          top: 'Trending in tx',
          title: 'Gigi',
          bottom: 'Trending with :Rip Gigi',
        },
        {
          top: 'Music',
          title: 'We won',
          bottom: '135k Tweets',
        },
        {
          top: 'Pop',
          title: 'Blue Ivy',
          bottom: '48k Tweets',
        },
        {
          top: 'Trending in Us',
          title: 'Denin Day',
          bottom: '40k Tweets',
        },
        {
          top: 'Trending',
          title: 'When Beyonce Day',
          bottom: '25.4k Tweets',
        },
      ],
      friends: [
        {
          src: 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Elon_Musk_Royal_Society_%28crop2%29.jpg/220px-Elon_Musk_Royal_Society_%28crop2%29.jpg',
          name: 'Elon Musk',
          handle: '@elonmusk',
        },
        {
          src: 'https://avatars.githubusercontent.com/u/463230?v=4',
          name: 'taylor otwell',
          handle: '@taylorotwell',
        },
        {
          src: 'https://www.github.com/yyx990803.png',
          name: 'Evan You',
          handle: '@youyuxi',
        },
      ],
      following: [
        {
          src: 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Elon_Musk_Royal_Society_%28crop2%29.jpg/220px-Elon_Musk_Royal_Society_%28crop2%29.jpg',
          name: 'Elon Musk',
          handle: '@elonmusk',
          time: '20 min',
          tweet: `I hereby challenge В
          ладимир Путин
          to single combat
          Stakes are Україна`,
          comments: '1,000',
          retweet: '550',
          like: '1,000,003',
        },
        {
          src: 'https://avatars.githubusercontent.com/u/463230?v=4',
          name: 'taylor otwell',
          handle: '@taylorotwell',
          time: '55 min',
          tweet: `Monday is my favorite day of the week. It's a fresh opportunity to improve yourself and those around you. Screwed up last week? No problem - this is a fresh week.
You don't have to wait until New Years to make a resolution or improve something. Do it every week. Every day. 🌱`,
          comments: '2,030',
          retweet: '50',
          like: '20,003',
        },
        {
          src: 'https://www.github.com/yyx990803.png',
          name: 'Evan You',
          handle: '@youyuxi',
          time: '1.4 hr',
          tweet: `Volar v0.33.0 Highlights:
- Supported change built-in formatters
- Supported vue-tsc watch
- Preview features is not longer need subscription

Let's check changelog for more version details:`,
          comments: '100,000',
          retweet: '1,000,003',
          like: '5,000,003',
        },
      ],
      tweets: [
        {
          content: `it's so  nice outside!`,
        },
      ],
      tweet: {
        content: ``,
      },
    };
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.tweet.content,
      };
      this.tweets.push(newTweet);
    },
  },
};
</script>
<style></style>
