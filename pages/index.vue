<template>
  <section class="home">
    <template v-if="content.length">
      <div ref="tilesContainer" class="tiles-container">
        <div class="title">Connecting people and spaces</div>
        <TilesComponent
          v-for="(item, index) in content"
          :key="index"
          :ref="`card${index}`"
          :item="item"
          :class="getClass(index)"
        />
        <div class="button">
          <button class="btn" @click.prevent="$fetch">Load More</button>
        </div>
      </div>
    </template>
  </section>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      content: [],
      limit: 7,
      page: 1,
    }
  },

  async fetch() {
    const { env } = this.$nuxt.context
    const url = new URL('https://api.unsplash.com/photos')
    const urlParams = new URLSearchParams({
      client_id: env.NUXT_ENV_UNSPLASH_ACCESS_KEY,
      page: this.page,
      per_page: this.limit,
    }).toString()
    try {
      const response = await fetch(`${url}?${urlParams}`)
      if (!response.ok)
        return console.error('An error occurred while trying to fetch images')
      this.content = [...this.content, ...(await response.json())]
      this.page++
    } catch (error) {
      console.error(error)
    }
  },

  watch: {
    content: function (val) {
      if (val.length > 7) {
        const { tilesContainer } = this.$refs
        if (!tilesContainer.style.gridAutoFlow) {
          tilesContainer.style.gridAutoFlow = 'dense'
        }
      }
    },
  },

  fetchOnServer: false,

  methods: {
    getClass(index) {
      const classes = [
        'featured',
        'card-1',
        'card-2',
        'card-3',
        'card-4',
        'card-5',
        'card-6',
      ]
      return classes[index % classes.length]
    },
  },
}
</script>

<style lang="scss">
.home {
  background-color: #191919;
  min-height: 100vh;
  padding: 4.375rem;
  color: #fff;
  padding: 1rem;

  @media only screen and (min-width: 768px) {
    padding: 2rem;
  }

  @media only screen and (min-width: 1024px) {
    padding: 4rem;
  }

  .tiles-container {
    display: grid;
    gap: 1.25rem;
    max-width: 100%;
    grid-template-columns: 1fr;
    grid-auto-rows: 10.5rem;
    // grid-auto-flow: dense;

    @media only screen and (min-width: 600px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media only screen and (min-width: 768px) {
      grid-template-columns: repeat(3, 1fr);
    }

    @media only screen and (min-width: 1024px) {
      grid-template-columns: repeat(4, 1fr);
    }

    @media only screen and (min-width: 1440px) {
      grid-template-columns: repeat(12, 1fr);
      grid-auto-rows: 4.875rem;
    }

    .featured {
      @media only screen and (min-width: 600px) {
        grid-column: auto / span 1;
        grid-row: auto / span 3;
      }

      @media only screen and (min-width: 768px) {
        grid-column: auto / span 1;
      }

      @media only screen and (min-width: 1024px) {
        grid-column: auto / span 2;
      }

      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 6;
        grid-row: auto / span 4;
      }
    }

    .card-1 {
      @media only screen and (min-width: 768px) {
        grid-column: auto / span 1;
        grid-row: auto / span 2;
      }

      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 4;
        grid-row: auto / span 2;
      }
    }

    .card-2 {
      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 3;
        grid-row: auto / span 2;
      }
    }

    .card-3 {
      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 2;
        grid-row: auto / span 2;
      }
    }

    .card-4 {
      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 4;
        grid-row: auto / span 4;
      }
    }

    .card-5 {
      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 3;
        grid-row: auto / span 3;
      }
    }

    .card-6 {
      @media only screen and (min-width: 1440px) {
        grid-column: auto / span 3;
        grid-row: auto / span 2;
      }
    }

    .title {
      font-weight: 400;
      font-size: 1.5rem;
      line-height: 2.75rem;
      letter-spacing: -0.04em;
      display: flex;
      justify-content: flex-start;
      align-items: center;

      @media only screen and (min-width: 768px) {
        grid-column: 1 / span 2;
        font-size: 2rem;
      }

      @media only screen and (min-width: 1024px) {
        grid-column: 1 / span 2;
      }

      @media only screen and (min-width: 1440px) {
        grid-column: 1 / span 4;
        grid-row: 1 / span 2;
      }
    }

    .button {
      .btn {
        margin-top: .5rem;
        color: #fff;
        text-transform: uppercase;
        padding: .5rem 1.25rem;
        background: #4a52ff;
        border-radius: 1.563rem;
        cursor: pointer;
        outline: none;
      }
      @media only screen and (min-width: 1440px) {
        grid-column: 10 / span 2;
        grid-row: auto / span 2;
      }
    }
  }
}
</style>
