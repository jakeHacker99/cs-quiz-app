<template>
  <div class="a">
    <div>
      <b-nav tabs>
        <b-nav-item disabled ><b>Datateknik quiz</b></b-nav-item>
        <b-nav-item disabled>Rätt: {{numCorrect}} / {{numTotal}}</b-nav-item>
      </b-nav>
    </div>
  </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]

};

</script>

<style scoped>
.tabs{
  background: #000;
}
</style>