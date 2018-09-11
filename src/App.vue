<template>
  <div class="container mt-4">
    <div class="row mb-2">
      <div class="col-md-12">
        <div class="card">
          <div class="card-body">
            <h2>{{ listName }}</h2>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <div class="form-group">
              <label for="addElement">Dodaj element</label>
              <div class="input-group mb-3">
                <input type="text" id="addElement" class="form-control" v-model="newElement">
                <div class="input-group-append">
                  <button class="btn btn-secondary" v-on:click="addElement">Dodaj element</button>
                </div>
              </div>
             <label for="changeListName">Zmień nazwę listy elementów</label>
             <input type="text" id="changeListName" class="form-control" v-model="listName">
            </div>
            <div v-if="emptyStringAlert" class="alert alert-danger" role="alert">
              Dodawany element nie może być pustym stringiem!
              <button class="btn btn-danger btn-sm float-right" v-on:click="closeAlert">X</button>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <div v-if="elements.length == 0">Dodaj element</div>
            <p v-else>Ilość elementów: {{ elements.length }}</p>
              <div class="form-inline">
                <div v-for="(element, index)  in elements" class="mt-2">
                  <input type="text" class="form-control" v-model="element.text">
                  <button class="btn btn-secondary" v-on:click="editElement" v-bind="{ 'disabled': element.text == 0 }">Edytuj</button>
                  <button class="btn btn-danger" v-on:click="deleteElement(index)">Usuń</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      text: '',
      elements: [],
      newElement: '',
      emptyStringAlert: false,
      editElementStatus: true,
      listName: 'Moja lista elementów' 
    }
  },
  methods: {
    addElement: function() {
      let text;

      text = this.newElement.trim();

      if(text) {
        this.elements.push({
          text: text,
        });

        this.newElement = '';
        this.emptyStringAlert = false;
      } else {
        this.emptyStringAlert = true;
      }
    },
    closeAlert: function() {
      this.emptyStringAlert = false;
    },
    editElement: function(element) {
      return this.editElementStatus = false;
    },
    saveElement: function() {
      return this.editElementStatus = true;
    },
    deleteElement: function(index) {
      this.elements.splice(index, 1);
    }
  }
}
</script>

