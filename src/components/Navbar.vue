<template>
     <nav class="navbar navbar-expand-sm navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Tabellen</a>
     
      <div>
        <ul class="navbar-nav">
         
          <li class="nav-item">
            <a class="nav-link" href="#" @click="liga('bl1')">Buli</a>
          </li>
           <li class="nav-item">
            <a class="nav-link" href="#" @click="list('bl2')">2. Liga</a>
          </li>
           <li class="nav-item">
            <a class="nav-link" href="#" @click="list('bl3')">3. Liga</a>
          </li>
          
          
        </ul>
      </div>
    </nav>
</template>

<script>
export default {
  methods: {
    list(type) {
      const querystr = `/?sort=${type}:${this.direction}`;
      this.$emit("list",querystr);
    }
  }
};
</script>

<style>

</style>
