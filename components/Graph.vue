<template>
  <div class="w-full">
    <div ref="cy" class="h-full w-full" style="height: 100vh"></div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import cytoscape from 'cytoscape';
import data from '~/files/data.json';

export default {
  name: 'Graph',
  setup() {
    const cyRef = ref(null);

    onMounted(() => {
      if (cyRef.value) {
        cytoscape({
          container: cyRef.value, // Accede correctamente al contenedor

          elements: data,

          style: [
            {
              selector: 'node',
              style: {
                'background-color': '#0074D9',
                label: 'data(label)',
                color: '#bc1313',
              },
            },
            {
              selector: 'edge',
              style: {
                'line-color': 'rgba(26,126,114,0)',
              },
            },
          ],

          layout: {
            name: 'grid',
          },
        });
      } else {
        console.error('El contenedor del grafo no está disponible.');
      }
    });

    return {
      cy: cyRef,
    };
  },
};
</script>
