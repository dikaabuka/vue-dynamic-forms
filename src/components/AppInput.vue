<template>
  <li class="plain">
    <label :for="newIndex">
      <input
          :id="newIndex"
          :name="model.id"
          v-model="model.value"
          type="text"
          ref="newIndex"
          class="row-input"
          placeholder=" Enter a value"
      />
    </label>
    <button class="transparent" @click="move(newIndex,-1)"
            :disabled="fields.length===0">
      <svg class="row-up"
           xmlns="http://www.w3.org/2000/svg"
           fill="none" viewBox="0 0 24 24" stroke="currentColor" color="teal">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 11l3-3m0 0l3 3m-3-3v8m0-13a9 9 0 110 18 9 9 0 010-18z"></path>
      </svg>
    </button>

    <button class="transparent" @click="move(newIndex,1)"
            :disabled="fields.length===0">
      <svg class="row-down"
           width="32px" height="32px"
           xmlns="http://www.w3.org/2000/svg"
           fill="none" viewBox="0 0 24 24" stroke="currentColor" color="tomato">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M15 13l-3 3m0 0l-3-3m3 3V8m0 13a9 9 0 110-18 9 9 0 010 18z"></path>
      </svg>
    </button>

    <button class="transparent" @click="remove(newIndex)">
      <svg class="row-delete"
           width="32px" height="32px"
           xmlns="http://www.w3.org/2000/svg"
           fill="none" viewBox="0 0 24 24" stroke="currentColor" color="crimson">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
      </svg>
    </button>
  </li>
</template>
<script>
export default {
  name: "AppInput",
  props: {
    input: {
      type: Object,
      default: () => {
      },
    },
    index: {
      type: [String, Number],
      default: '',
    },
    fields: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      model: {},
      newIndex: '',
    };
  },
  watch: {
    input: {
      immediate: true,
      handler(update) {
        if (update != null) {
          this.model = update;
        }
      }
    },
    index: {
      immediate: true,
      handler(value) {
        if (value != null) {
          this.newIndex = value;
        }
      }
    },
  },
  methods: {
    move(index, mode) {
      if (String(index) !== '' && String(mode) !== '') {
        let payload = {
          "index": String(index),
          "mode": String(mode)
        }
        this.$emit('moveHandler', payload);
      }
    },
    remove(index) {
      if (String(index) !== '') {
        let payload = {
          "index": String(index),
        }
        this.$emit('removeHandler', payload);
      }
    },
  },
}
</script>
<style scoped>
body {
  font-family: 'Open Sans', sans-serif;
  background-color: #4894D6;
}

.plain {
  list-style: none !important;
}

#formFields div {
  cursor: pointer;
  width: 98.5%;
  height: 50px;
  font-weight: bold;
  text-align: center;
  line-height: 2em;
  background: white;
  border-radius: 3px;
  box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
  border: 1px solid black;
  margin: 0 5px 5px 5px;
  float: left;
  transition: all 0.2s ease;
}

#formFields div:hover {
  background-color: #f4f4f4;
  cursor: pointer;
}

#formFields button.add-btn {
  cursor: pointer;
  width: 21.5%;
  height: 36px;
  font-weight: bold;
  text-align: center;
  line-height: 2em;
  border-radius: 3px;
  background: lightsalmon;
  color: white;
  box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
  margin: 0 5px 11px 5px;
  float: left;
  transition: all 0.2s ease;
}

.row-input {
  width: 69.5%;
  height: 44px;
  margin: 2px;
  border: none;
  box-shadow: none;
  background: transparent;
  display: inline-block;
  float: left;
  padding: 0 10px;
}

.row-input:hover {
  border: 1px solid transparent;
  border-top: none;
  border-bottom: 1px solid #DDD;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .39), 0 -1px 1px #FFF, 0 1px 0 #FFF;
}

.row-input:focus {
  border: 1px solid black;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .39), 0 -1px 1px #FFF, 0 1px 0 #FFF;
}

.transparent {
  border: none !important;
  text-decoration: none;
  outline: none !important;
  background: none !important;
  box-shadow: none !important;
  font-size: 27px;
  width: 8%;
  padding: 0 2px;
  height: 77%;

}

.transparent svg {
  width: 100%;
  height: 100%;
  font-size: 38px;
  box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
  border-radius: 4px;
}

svg {
}

.row-up, .row-delete, .row-down {
  width: 6%;
  display: inline-block;
  float: none;
  text-align: center;
  margin: 4px auto auto auto;
  border: 1px solid rgba(0, 0, 0, 0.3);
}

.row-up:hover {
  cursor: pointer;
  border: 1px solid teal;
}

.row-down:hover {
  cursor: pointer;
  border: 1px solid tomato;
}

.row-delete:hover {
  cursor: pointer;
  border: 1px solid crimson;
}


@media only screen and (max-width: 600px) {

  #formFields div {
    cursor: pointer;
    width: 96.5%;
    height: 50px;
    font-weight: bold;
    text-align: center;
    line-height: 2em;
    background: white;
    border-radius: 3px;
    box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
    border: 1px solid black;
    margin: 0 5px 5px 5px;
    float: left;
    transition: all 0.2s ease;
  }


  .row-input {
    width: 53%;
    height: 44px;
    margin: 2px;
    border: none;
    box-shadow: none;
    background: transparent;
    display: inline-block;
    float: left;
    padding: 0 10px;
  }

  .transparent {
    border: none !important;
    text-decoration: none;
    outline: none !important;
    background: none !important;
    box-shadow: none !important;
    font-size: 27px;
    width: 12%;
    padding: 2px;
    height: 77%;
  }
}


</style>