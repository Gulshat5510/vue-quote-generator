<template>
  <div id="app">
    <Header title="The Anime Quoter" />
    <Quote :quote="quote" />
    <div class="button-container">
      <button @click="getQuote">Generate</button>
    </div>
    <QuoteList :quotes="quotes" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Quote from './components/Quote.vue';
import QuoteList from './components/QuoteList.vue';

export default {
  name: 'App',
  components: {
    Header,
    Quote,
    QuoteList
  },
  data() {
    return {
      quote: {},
      quotes: []
    }
  },
  methods: {
    async getQuote() {
      if (this.quote.content) {
        this.quotes = [...this.quotes, this.quote];
      }

      const data = await fetch('https://animechan.vercel.app/api/random').
      then(res => res.json());

      this.quote = {
        content: data.quote,
        anime: data.anime,
        character: data.character
      };
    }
  },
  created () {
    this.getQuote();
  }
}
</script>

<style lang="scss">
:root {
	--primary: #D81E5B;
	--secondary: #8A4FFF;
	--tertiary: #32CBFF;
	--dark: #131A26;
	--light: #EEE;
	--grey: #848484;
}
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Fira Sans', sans-serif;
}
.button-container {
	display: flex;
	justify-content: center;
	padding: 0px 32px;
	margin: 64px auto;
	button {
		border: none;
		outline: none;
		background-color: var(--primary);
		padding: 16px 32px;
		border-radius: 99px;
		color: var(--light);
		font-size: 1.5em;
		font-weight: 700;
		text-transform: uppercase;
		cursor: pointer;
		transition: 0.4s;
		&:hover {
			background-color: var(--secondary);
		}
	}
}
</style>
