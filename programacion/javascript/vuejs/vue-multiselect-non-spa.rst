.. _reference-programacion-javascript-vuejs-vue-multiselect-non-spa:

#######################
Vue-Multiselect non spa
#######################

* https://monterail.github.io/vue-multiselect/

**Fuentes**

* https://github.com/monterail/vue-multiselect/issues/226

--------

**HTML**

.. code-block:: html

    <main class="container">
        <section class="row">
          <div class="col-12">
            <!-- Vue component -->
            <template>
              <div>
                <multiselect v-model="value" :options="options"></multiselect>
              </div>
            </template>
          </div>
        </section>
      </main>

**Javascript**

.. code-block:: javascript

    Vue.component('multiselect', window.VueMultiselect.default);

    const app = new Vue({
      el: 'main',
      data: {
        value: 'test',
        options: [
          'just', 'for', 'test'
        ]
      }
    });
