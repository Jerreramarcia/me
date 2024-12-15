<template>
  <div class="w-full">
    <div ref="cy" class="h-full w-full" style="height: 100vh"></div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import cytoscape from 'cytoscape';

export default {
  name: 'Graph',
  setup() {
    const cyRef = ref(null);

    onMounted(() => {
      if (cyRef.value) {
        cytoscape({
          container: cyRef.value, // Accede correctamente al contenedor

          elements: [
            { data: { id: 'A', label: 'Node A' } },
            { data: { id: 'B', label: 'Node B' } },
            { data: { source: 'A', target: 'B' } },
          ],

          style: [
            {
              selector: 'node',
              style: {
                'background-color': '#0074D9',
                label: 'data(label)',
                color: '#fff',
              },
            },
            {
              selector: 'edge',
              style: {
                'line-color': '#ccc',
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
