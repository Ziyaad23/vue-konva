<template>
  <main>
    <v-stage :config="configKonva">
      <v-layer>
        <v-rect
          v-for="rectangle in rectangles"
          :key="rectangle.name"
          :config="rectangle"
        />
        <v-line
          v-for="item in 10"
          :key="item"
          :config="{
            points: [0, Math.round(item * 30), width, Math.round(item * 30)],
            stroke: 'red',
            strokeWidth: 0.5,
          }"
        />
      </v-layer>
    </v-stage>
    <ul>
      <li v-for="index in 10" :key="index">{{ index }}</li>
    </ul>
  </main>
</template>

<script>
export default {
  data() {
    return {
      configKonva: {
        width: 200,
        height: 300,
      },
      rectangles: [
        {
          rotation: 0,
          x: 10,
          y: 10,
          width: 100,
          height: 100,
          scaleX: 1,
          scaleY: 1,
          fill: "red",
          name: "rect1",
        },
        {
          rotation: 0,
          x: 150,
          y: 150,
          width: 100,
          height: 100,
          scaleX: 1,
          scaleY: 1,
          fill: "green",
          name: "rect2",
        },
        {
          rotation: 0,
          x: 80,
          y: 80,
          width: 100,
          height: 100,
          scaleX: 1,
          scaleY: 1,
          fill: "blue",
          name: "rect3",
        },
      ],
    };
  },
  mounted() {},
};
</script>
