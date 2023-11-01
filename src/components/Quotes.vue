<template>
  <div class="progressBar">
    <h1>Quotes Progress:</h1>
    <div class="progressBackground">
        <div class="precentProgress" style="background-color: rgb(14, 114, 201); margin: 0;" :style="{width: numberOfQuotes * 10 + '%'}"></div>
        <div class="displayNumbers">
            {{ numberOfQuotes }} / {{ maxOfQuotes }}
        </div>
    </div>
  </div>
  <div class="quoteSection">
    <input @keypress.enter="addQuote" id="userInput" type="text"/>
    <div v-if="quotes.length" class="listOfQuotes">
        <ul>
            <li v-for="quote in quotes" :key="quote.id" @click="deleteQuote(quote.id, quotes)" placeholder="Please type quotes here...">
                {{ quote.statement }}
            </li>
        </ul>
    </div>
    <div v-else class="emptyQuoteList">Please enter some quotes!</div>
  </div>
  <div v-if="displayMe" class="displayMe">
    <div>
        <h4>Please enter Quotes by typing and pressing the Enter Button</h4>
        <h4>Or delete Quotes by clicking them</h4>
    </div>
  </div>
  <div v-else class="displayMeElse">
        <h4>Please delete some Quotes or make sure you actually typed something in the Input Field</h4>
  </div>
</template>

<script>
export default {
    data() {
        return {
            numberOfQuotes: 0,
            maxOfQuotes: 10, 
            quotes: [],
            counter: 0,
            displayMe: true,
        }
    },
    methods: {
        addQuote() {
            this.displayMe = true
            let newQuote = document.getElementById('userInput').value
            if (newQuote.length > 0 && this.numberOfQuotes != this.maxOfQuotes) {
                let id = Math.random()
                this.quotes[this.counter] = {statement: newQuote, id}
                document.getElementById('userInput').value = ""
                this.numberOfQuotes++
                this.counter++
            } else {
                document.getElementById('userInput').value = ""
                this.displayMe = false
            }
        },
        deleteQuote(id, quotes) {
            let findMe = quotes.findIndex((foundQuote) => foundQuote.id == id)
            quotes.splice(findMe, 1)
            this.numberOfQuotes--
            this.counter--
            this.displayMe = true
            return quotes
        },
    }
}
</script>

<style>
    .progressBackground {
        margin: auto;
        margin-top: -15px;
        height: 40px;
        width: 100%;
        max-width: 500px;
        background-color: #ccc;
        border-radius: 2rem;
    }
    .precentProgress {
        height: 40px;
        border-radius: 2rem;
    }
    .displayNumbers {
        margin-top: -30px;
    }
    .quoteSection {
        margin-top: 30px;
    }
    #userInput {
        margin: auto;
        width: 100%;
        max-width: 500px;
        height: 40px;
        border-radius: 2rem;
        border: 3px solid black;
    }
    .listOfQuotes {
        padding: 10px;
    }
    ul {
        list-style: none;
        margin: auto;
        max-width: 800px;
        width: 100%;
        border: 1px solid #ccc;
        box-shadow: 0px 3px 6px #ccc;
    }
    li {
        margin: auto;
        max-width: 745px;
        padding: 5px;
        margin: 10px;
        background-color: rgb(160, 98, 160);
        color: white;
        border-radius: 2rem;
    }
    .emptyQuoteList {
        margin: auto;
        margin-top: 10px;
        max-width: 500px;
        padding: 5px;
        background-color: rgb(160, 98, 160);
        color: white;
        border-radius: 2rem;
    }
    .displayMe {
        color: blue;
        background-color: #e4e8ff;
    }
    .displayMeElse {
        color: red;
        background-color: #ffc0c1;
    }
    h1 {
        margin-top: -30px;
    }
</style>