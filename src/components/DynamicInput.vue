<template>
  <div id="app">

    <div id="formContainer">

      <div class="addButtonContainer">
        <button class="add-row" @click="addField()">Add A New Field</button>
      </div>

      <div v-if="dynamicFields.length > 0" id="formFields">
        <div
            v-for="(input, i) in dynamicFields"
            :key="i"
        >
          <AppInput
              :fields="dynamicFields"
              :index="i"
              :input="input"
              @moveHandler="moveField"
              @removeHandler="removeField"
          />
        </div>
      </div>

    </div>

  </div>
</template>

<script>

import AppInput from "@/components/AppInput.vue";


export default {
  name: "DynamicInput",
  components: {
    AppInput
  },
  data() {
    return {
      dynamicFields: [],
    };
  },
  methods: {
    randomId() {
      return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, (c) => {
        let r = (Math.random() * 16) | 0,
            v = c === "x" ? r : (r & 0x3) | 0x8;
        return v.toString(16);
      });
    },
    addField() {
      this.dynamicFields.push({value: '', id: this.randomId()});
      this.$nextTick(() => {
        if (this.dynamicFields.length > 0) {
          document.getElementById(this.dynamicFields.length - 1).focus();
        }
      });

    },
    moveField(payload) {
      if (payload) {
        const arr = this.dynamicFields;
        const {index, mode} = payload;
        const newIndex = parseInt(index) + parseInt(mode);
        const indexes = [parseInt(index), newIndex].sort((a, b) => a - b);

        if (newIndex < 0) {
          document.getElementById(0).focus();
          return
        }

        if (newIndex === arr.length) {
          document.getElementById(this.dynamicFields.length - 1).focus();
          return
        }

        arr.splice(indexes[0], 2, arr[indexes[1]], arr[indexes[0]]);

        if (parseInt(mode) === -1) {
          this.$nextTick(() => {
            if (this.dynamicFields.length > 0) {
              const target = this.dynamicFields.length - 2;
              if (target) {
                document.getElementById(target).focus();
              }
            }
          });
        }

        if (parseInt(mode) === 1) {

          this.$nextTick(() => {
            if (this.dynamicFields.length > 0) {
              const target = this.dynamicFields.length - 3;
              if (target) {
                document.getElementById(target).focus();
              }

            }
          });
        }

      }
    },
    removeField(payload) {
      if (payload) {
        const arr = this.dynamicFields;
        const index = payload.index;
        if (!Array.isArray(arr) || arr.length === 0 || !index) return;
        arr.splice(index, 1);
        this.$nextTick(() => {
          if (this.dynamicFields.length === 0) {
            return;
          }
          const target = this.dynamicFields.length - 1;
          if (target) {
            document.getElementById(target).focus();
          }

        });
      }

    },
  }

}
</script>

<style scoped>
#app {
  display: flex;
  width: 100%;
}

body {
  font-family: 'Open Sans', sans-serif;
}

#formContainer {
  background-color: #f7f7f7;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 16px;
  padding: 1.7em 1em 1em 0.8em;
  margin: auto;
  width: 550px;
  clear: both;
  display: table;
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

.add-row {
  float: right;
  display: inline-block;
  cursor: pointer;
  width: auto;
  height: 36px;
  font-weight: bold;
  text-align: center;
  line-height: 2em;
  border-radius: 4px;
  padding: 0 10px;
  background: lightsalmon;
  color: white;
  border: 1px solid black;
  box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
  margin: 0 5px 11px 5px;
  transition: all 0.2s ease;
}

.addButtonContainer {
  width: 97.7%;
  height: 37px;
  display: block;
  background: white;
  border-radius: 3px;
  box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(0, 0, 0, 0.5);
  margin: 0 5px 10px 5px;
  padding: 10px 2px;
}

@media only screen and (max-width: 600px) {

  #formContainer {
    background-color: #f7f7f7;
    border-radius: 3px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    padding: 1px;
    margin: auto;
    height: auto;
    width: 100%;
    clear: both;
    display: inline-block;
    position: relative;
  }

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

  .addButtonContainer {
    width: 95.5%;
    height: 38px;
    display: block;
    background: white;
    border-radius: 3px;
    box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
    border: 1px solid rgba(0, 0, 0, 0.5);
    margin: 5px 5px 10px 5px;
    padding: 10px 2px;
  }

    }
</style>