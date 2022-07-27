<template>
  <div>
    <v-stage ref="stage" :config="configKonva">
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
            fontFamily: 'Calibri',
            fill: 'black',
          }"
        ></v-text>
        <v-group>
          <v-rect
            :config="{
              x: 40,
              y: 20,
              width: 50,
              height: blockSnapSize * input1,
              fill: '#4472c4',
              shadowBlur: 2,
            }"
          />
          <v-rect
            :config="{
              x: 120,
              y: total - input2 * blockSnapSize,
              width: 50,
              height: blockSnapSize * input2,
              fill: '#4472c4',
              shadowBlur: 2,
            }"
          />
          <v-rect
            :config="{
              x: 200,
              y: total - input3 * blockSnapSize,
              width: 50,
              height: blockSnapSize * input3,
              fill: '#4472c4',
              shadowBlur: 2,
            }"
          />
        </v-group>
      </v-layer>
    </v-stage>
  </div>
</template>

<script>
const width = 300;
const height = 270;
export default {
  data() {
    return {
      list: [],
      configKonva: {
        width: width,
        height: height,
      },
      input1: 10,
      input2: 6,
      input3: 1,
      blockSnapSize: 20,
      vlines: [],
      hlines: [],
      yaxis: [],
      x: 0,
      y: 0,
      charts: [],
      labelY: 0,
      labelX: 0,
      highestValue: 10,
      lowestValue: -2,
      startingValue: 0,
      total: 0,
    };
  },
  computed() {},
  methods: {},
  mounted() {
    let padding = this.blockSnapSize;
    let labelPosition = 0;
    let label = this.highestValue + 1;
    this.total = this.highestValue * this.blockSnapSize + this.blockSnapSize;

    for (var j = 0; j < height / padding; j++) {
      this.hlines.push({
        id: Math.round(Math.random() * 999).toString(),
        points: [0, Math.round(j * padding), width, Math.round(j * padding)],
      });
    }

    for (var j = 0; j < height / padding; j++) {
      this.yaxis.push({
        id: Math.round(Math.random() * 999).toString(),
        labelX: 0,
        labelY: (labelPosition += padding),
        labelText: (label -= 1),
      });
    }
  },
};
</script>
