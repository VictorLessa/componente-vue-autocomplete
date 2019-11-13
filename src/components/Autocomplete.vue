<template>
  <div class="group">
    <input
      class="autocomplete-input"
      v-on:input="$emit('input', $event.target.value)"
      v-bind:value="input"
      type="text"
      required
    />
    <span class="highlight"></span>
    <span class="bar" v-bind:class="{'bar-loading': loading}"></span>
    <label class="autocomplete-label">{{ placeholder }}</label>
    <ul v-if="this.items.length > 0" class="autocomplete-list">
      <li
        v-on:click="selected(item)"
        v-for="(item, index) in items"
        :key="index"
      >{{ item.name | capitalize }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "autocomplete",
  data() {
    return {
      input: ""
    };
  },
  watch: {
    value(val) {
      if (!val) {
        this.input = "";
        return;
      }
      this.input = val;
      if (isFinite(val) && !isNaN(val)) {
        this.$emit("syncSearchInt", val);
      } else {
        this.$emit("syncSearchStr", val);
      }
    }
  },
  props: {
    value: {
      type: String,
      default: ""
    },
    items: {
      type: Array,
      default: []
    },
    loading: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      default: "Nome"
    }
  },
  methods: {
    selected(item) {
      this.input = item.name;
      this.$emit("selected", item);
    }
  }
};
</script>

<style>
/* form starting stylings ------------------------------- */
.group {
  position: relative;
  width: auto;
}
.autocomplete-input {
  font-size: 18px;
  padding: 10px 10px 0px 5px;
  display: block;
  width: 100%;
  border: none;
  border-bottom: 1px solid #757575;
}
.autocomplete-input:focus {
  outline: none;
}

/* LABEL ======================================= */
.autocomplete-label {
  color: #999;
  font-size: 18px;
  font-weight: normal;
  position: absolute;
  pointer-events: none;
  left: 5px;
  top: 10px;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}

/* active state */
.autocomplete-input:focus ~ .autocomplete-label,
.autocomplete-input:valid ~ .autocomplete-label {
  top: -20px;
  font-size: 14px;
  color: #5264ae;
}

/* BOTTOM BARS ================================= */
.bar {
  position: relative;
  display: block;
  width: 100%;
}
.bar:before,
.bar:after {
  content: "";
  height: 2px;
  width: 0;
  bottom: 1px;
  position: absolute;
  background: #5264ae;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}
.bar:before {
  left: 50%;
}
.bar:after {
  right: 50%;
}

.bar-loading {
  position: relative;
  display: block;
  width: 100%;
  content: "";
  height: 2px;
  width: 0;
  bottom: 1px;
  background: #5264ae;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
  animation: loading 500ms;
  animation-iteration-count: infinite;
}
/* active state */
.autocomplete-input:focus ~ .bar:before,
.autocomplete-input:focus ~ .bar:after {
  width: 50%;
}

/* HIGHLIGHTER ================================== */
.highlight {
  position: absolute;
  height: 60%;
  width: 100px;
  top: 25%;
  left: 0;
  pointer-events: none;
  opacity: 0.5;
}

/* active state */
.autocomplete-input:focus ~ .highlight {
  -webkit-animation: inputHighlighter 0.3s ease;
  -moz-animation: inputHighlighter 0.3s ease;
  animation: inputHighlighter 0.3s ease;
}

/* ANIMATIONS ================ */
@-webkit-keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}
@-moz-keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}
@keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}

@keyframes loading {
  from {
    width: 0px;
  }
  to {
    width: 100%;
  }
}

/* auto complete list */
.autocomplete-list {
  list-style-type: none;
  width: auto;
  margin: 0;
  padding: 0;
  max-height: 200px;
  overflow-y: scroll;
  border: 1px solid gray;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
}
.autocomplete-list li {
  text-align: left;
  padding: 10px 5px;
  cursor: pointer;
  word-wrap: break-word;
  overflow: hidden;
  text-overflow: ellipsis;
}
.autocomplete-list li:hover {
  background-color: azure;
}
.autocomplete-list li:nth-last-child(n) {
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
}
</style>
