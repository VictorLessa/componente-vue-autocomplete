<template>
  <div>

    <div class="group">      
      <input @input="search" type="text" v-bind:value="value" v-on:input="$emit('input', $event.target.value)" required>
      <span class="highlight"></span>
      <span class="bar"></span>
      <label>{{ label }}</label>
    <ul class="list-autocomplete" v-if="hasResults">
      <li v-for="(item, index) in items" :key="index">{{ item.name }}</li>
    </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Autocomplete",
  data() {
    return {
      lovingVue: "",
      hasResults: false
    };
  },
  props: {
    items: {
      type: Array,
      default: [{name: 'Sem items'}]
    },
    label: {
      type: String,
      default: 'texto'
    },
    value: String
  },
  methods: {
    search () {
      if (this.items.length > 0) {
        this.hasResults = true
      } else {
        this.hasResults = false
      }
    }
  }
};
</script>

<style>
.group 			  { 
  position:relative; 
  margin-bottom:45px;
  max-width: 500px;
}
input 				{
  font-size:18px;
  padding:10px 0px 10px 0px;
  display:block;
  width:100%;
  border:none;
  border-bottom:1px solid #757575;
}
input:focus 		{ outline:none; }

/* LABEL ======================================= */
label 				 {
  color:#999; 
  font-size:18px;
  font-weight:normal;
  position:absolute;
  pointer-events:none;
  left:5px;
  top:10px;
  transition:0.2s ease all; 
  -moz-transition:0.2s ease all; 
  -webkit-transition:0.2s ease all;
}

/* active state */
input:focus ~ label, input:valid ~ label 		{
  top:-20px;
  font-size:14px;
  color:#5264AE;
}

/* BOTTOM BARS ================================= */
.bar 	{ position:relative; display:block; width:auto; }
.bar:before, .bar:after 	{
  content:'';
  height:2px; 
  width:0;
  bottom:1px; 
  position:absolute;
  background:#5264AE; 
  transition:0.2s ease all; 
  -moz-transition:0.2s ease all; 
  -webkit-transition:0.2s ease all;
}
.bar:before {
  left:50%;
}
.bar:after {
  right:50%; 
}

/* active state */
input:focus ~ .bar:before, input:focus ~ .bar:after {
  width:50%;
}

/* HIGHLIGHTER ================================== */
.highlight {
  position:absolute;
  height:60%; 
  width:100px; 
  top:25%; 
  left:0;
  pointer-events:none;
  opacity:0.5;
}

/* active state */
input:focus ~ .highlight {
  -webkit-animation:inputHighlighter 0.3s ease;
  -moz-animation:inputHighlighter 0.3s ease;
  animation:inputHighlighter 0.3s ease;
}

/* ANIMATIONS ================ */
@-webkit-keyframes inputHighlighter {
	from { background:#5264AE; }
  to 	{ width:0; background:transparent; }
}
@-moz-keyframes inputHighlighter {
	from { background:#5264AE; }
  to 	{ width:0; background:transparent; }
}
@keyframes inputHighlighter {
	from { background:#5264AE; }
  to 	{ width:0; background:transparent; }
}

/* LIST ITEMS */
.list-autocomplete {
  background-color: var(--mdc-theme-surface, #fff);
  /* border: 1px solid #e5e5e5;
  padding: 5px;
  text-align: left; */
  padding: 0;
  margin: 0;
  border-bottom-right-radius: 10px;
  border: 1px solid purple;
  width: 100%;
  border-bottom-left-radius: 10px;
  border: 1px solid #eeeeee;
  max-height: 400px;
  overflow-y: scroll;
}

.list-autocomplete li {
  list-style: none;
  text-align: left;
  padding: 15px 8px 15px 8px;
  cursor: pointer;
  word-wrap: break-word
}
.list-autocomplete li:hover {
  background-color: #fafafa;
  transition-duration: 250ms;
}
</style>
