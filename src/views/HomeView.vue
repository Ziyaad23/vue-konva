<template>
  <div class="container mx-auto p-10">
    <div class="grid grid-cols-1 gap-4 mb-10 sm:grid-cols-3">
      <div>
        <label class="form-label inline-block mb-2 text-gray-700"
          >Chart 1 input</label
        >
        <input
          type="number"
          class="form-control block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-500 focus:outline-none"
          v-model="input1"
        />
      </div>
      <div>
        <label class="form-label inline-block mb-2 text-gray-700"
          >Chart 2 input</label
        >
        <input
          type="number"
          class="form-control block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-500 focus:outline-none"
          v-model="input2"
        />
      </div>
      <div>
        <label class="form-label inline-block mb-2 text-gray-700"
          >Chart 3 input</label
        >
        <input
          type="number"
          class="form-control block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-500 focus:outline-none"
          v-model="input3"
        />
      </div>
      <div>
        <label class="form-label inline-block mb-2 text-gray-700"
          >Highest value</label
        >
        <input
          type="number"
          class="form-control block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-500 focus:outline-none"
          v-model="highestValue"
        />
      </div>
      <div>
        <label class="form-label inline-block mb-2 text-gray-700"
          >Lowest value</label
        >
        <input
          type="number"
          class="form-control block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-500 focus:outline-none"
          v-model="lowestValue"
        />
      </div>
    </div>
    <div>
      <v-stage :config="configKonva">
        <v-layer>
          <v-line
            v-for="hl in hlines"
            :key="hl.id"
            :config="{
              id: hl.id,
              points: hl.points,
              stroke: 'lightgrey',
              strokeWidth: 0.3,
            }"
          ></v-line>
          <v-text
            v-for="t1 in yaxis"
            :key="t1.id"
            :config="{
              id: t1.id,
              x: t1.labelX,
              y: t1.labelY,
              text: t1.labelText,
              fontSize: 10,
              fill: 'black',
            }"
          ></v-text>
          <v-group>
            <v-rect
              :config="{
                x: 40,
                y: total - input1 * blockSnapSize,
                width: 50,
                height: blockSnapSize * input1,
                fill: '#4472c4',
                shadowBlur: 3,
              }"
            />
            <v-rect
              :config="{
                x: 120,
                y: total - input2 * blockSnapSize,
                width: 50,
                height: blockSnapSize * input2,
                fill: '#4472c4',
                shadowBlur: 3,
              }"
            />
            <v-rect
              :config="{
                x: 200,
                y: total - input3 * blockSnapSize,
                width: 50,
                height: blockSnapSize * input3,
                fill: '#4472c4',
                shadowBlur: 3,
              }"
            />
          </v-group>
        </v-layer>
      </v-stage>
    </div>
  </div>
</template>

<script>
//Konva layout
const width = 300;
const height = 350;
export default {
  data() {
    return {
      list: [],
      configKonva: {
        width: width,
        height: height,
      },
      input1: 8,
      input2: 6,
      input3: 1,
      blockSnapSize: 20,
      hlines: [],
      yaxis: [],
      labelY: 0,
      labelX: 0,
      highestValue: 10,
      lowestValue: -2,
      total: 0,
    };
  },
  methods: {
    renderChart() {
      let padding = this.blockSnapSize;
      let labelPosition = 0;
      let label = this.highestValue + 1;
      this.total = this.highestValue * this.blockSnapSize + this.blockSnapSize;

      //Display horizontal line
      for (var j = 0; j < height / padding; j++) {
        this.hlines.push({
          id: crypto.randomUUID().slice(0, 6),
          points: [0, Math.round(j * padding), width, Math.round(j * padding)],
        });
      }

      //Display label on y-axis
      for (var j = this.lowestValue - 1; j < this.highestValue; j++) {
        this.yaxis.push({
          id: crypto.randomUUID().slice(0, 6),
          labelX: 0,
          labelY: (labelPosition += padding),
          labelText: (label -= 1),
        });
      }
    },
  },
  mounted() {
    //Render chart
    this.renderChart();
  },
  updated() {
    //Reset values
    this.hlines = [];
    this.yaxis = [];
    this.labelY = 0;
    this.labelX = 0;
    //Re render chart
    this.renderChart();
  },
};
</script>
