<template>
  <div class="bmiVisualization">
    <p class="petName">{{ petName }}'s BMI is</p>
    <p class="bmiValue">{{ bmi }}</p>
    <div class="markerContainer">
      <div class="marker" v-bind:style="{'left': marker + '%'}"></div>
    </div>
    <div class="bmiBarContainer">
      <div class="bar underweight" v-bind:class="{ active: underweight }"></div>
      <div class="bar normal" v-bind:class="{ active: normal }"></div>
      <div class="bar overweight" v-bind:class="{ active: overweight }"></div>
    </div>
    <div class="descriptionContainer">
      <p class="description" v-bind:class="{ active: underweight }">Underweight</p>
      <p class="description normal" v-bind:class="{ active: normal }">Normal</p>
      <p class="description" v-bind:class="{ active: overweight }">Overweight</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "BmiVisualization",
  data: function ()
  {
    return {
      underweight: false,
      normal: false,
      overweight: false,
      marker: 0,
      bmi: this.bmiValue,
      min: 0,
      max: 120,
    }
  },
  props: ['petName', 'bmiValue'],
  mounted()
  {
    this.checkBmiValue();
    this.markerPosition();

    //determine which category the bmiValue belongs to
    if (this.bmi < 30)
    {
      this.underweight = true;
    }
    else if (this.bmi > 90)
    {
      this.overweight = true;
    }
    else
    {
      this.normal = true;
    }
  },
  methods: {
    //calculate the %-value of the left horizontal position of the marker
    markerPosition()
    {
      this.marker = ((100 / 120 * this.bmi));
    },
    //check if bmi is in valid range (0-120), else set bmiValue to min or max
    checkBmiValue()
    {
      if (this.bmiValue < this.min)
      {
        this.bmi = this.min;
      }
      else if (this.bmiValue > this.max)
      {
        this.bmi = this.max;
      }
    }
  },
}
</script>

<style scoped>
.bmiVisualization {
  width: 50%;
  margin: auto;
}

.petName {
  font-size: 1.618rem;
  display: block;
}

.bmiValue {
  margin: 1.25rem auto;
  font-weight: 900;
  color: #007FC8;
  font-size: 4.235801032rem;
}

.markerContainer {
  position: relative;
  /*compensate 15px size of the marker */
  left: -1rem;
}

.marker {
  position: relative;
  width: 0;
  height: 0;
  border-left: 1rem solid transparent;
  border-right: 1rem solid transparent;
  border-top: 1.25rem solid var(--main-color);
  margin-bottom: 1px;
}

.bmiBarContainer {
  display: flex;
  gap: 1px;
}

.bar {
  background-color: var(--grey);
  height: 1.5rem;
}

.underweight {
  border-radius: 100px 0 0 100px;
}

.overweight {
  border-radius: 0 100px 100px 0;
}

.normal {
  width: 50%;
}

.underweight, .overweight {
  width: 25%;
}

.bar.underweight.active, .bar.overweight.active {
  background-color: var(--red);
}

.bar.normal.active {
  background-color: var(--green);
}

.descriptionContainer {
  display: flex;
  width: 100%;
}

.description {
  width: 25%;
}

.description.normal {
  width: 50%;
}

.description.active {
  font-weight: 700;
  color: var(--main-color);
}

@media screen and (max-width: 767px) {
  .bmiVisualization {
    width: 90%;
  }

  .description {
    font-size: 0.8rem;
  }
}

@media screen and (min-width: 768px) and (max-width: 991px) {
  .bmiVisualization {
    width: 70%;
  }
}
</style>