<template>
  <b-container>
    <b-row>
      <b-col sm="5" style="text-align: center">
        <b-row>
          <b-col md="12" style="margin: 50px">
            <b-button
              :disabled="getButtonDisabled"
              variant="dark"
              size="xl"
              @click="lanzarDado"
            >
              {{ getIntentosDisponibles }}
            </b-button>
          </b-col>
          <b-col md="12" style="margin: 50px">
            <div :class="getImagenCurrentDado"></div>
          </b-col>
        </b-row>
      </b-col>
      <b-col md-5 mt-3>
        <b-row v-if="lstJugadas.length == 3" style="margin-top: 150px">
          <b-col md="12">
            <span style="font-size: 25px; font-weight: 600; color: #cccccc">
              Fin del Juego!!!, Estos son los resultados:
            </span>
          </b-col>
          <b-col
            class="text-align:center"
            md="4"
            v-for="(k, index) in lstJugadas"
            :key="index"
          >
            <div style="margin: 20px" :class="` dadito dado-${k}`"></div>
            <br />
            <span
              style="
                margin-left: 20px;
                font-size: 18px;
                font-weight: 600;
                color: #cccccc;
              "
            >
              {{ index + 1 }} tiro: {{ k }}
            </span>
          </b-col>
        </b-row>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      disabledBtn: false,
      nIntentosDisponibles: 3,
      nNumeroDado: 0,
      lstJugadas: []
    }
  },
  mounted() {
},  methods: {
    setNumeroDado() {
      const randomDiceNum = Math.floor(Math.random() * 6) + 1
      this.nNumeroDado = randomDiceNum
    },
    lanzarDado() {
      let count = 0
      if (this.nIntentosDisponibles > 0) {
        this.disabledBtn = true
        const timer = setInterval(() => {
          this.setNumeroDado()
          if (count >= 6) {
            clearInterval(timer)
            this.lstJugadas.push(this.nNumeroDado)
            this.nIntentosDisponibles = this.nIntentosDisponibles - 1
            this.disabledBtn = false
          }
          count += 1
        }, 150)
      }
    }
  },
  computed: {
    getImagenCurrentDado() {
      return `dado dado-${this.nNumeroDado}`
    },

    getIntentosDisponibles() {
      if (this.nIntentosDisponibles == 3) {
        return 'Iniciar Juego, Tienes 3 intentos disponibles'
      } else if (
        this.nIntentosDisponibles < 3 &&
        this.nIntentosDisponibles > 0
      ) {
        return `Tienes ${this.nIntentosDisponibles} intentos disponibles`
      } else {
        return `Tienes ${this.nIntentosDisponibles} intentos disponibles`
      }
    },
    getButtonDisabled() {
      if (this.disabledBtn || this.nIntentosDisponibles <= 0) {
        return true
      }
      return false
    }
  },
  watch: {}
}
</script>

<style>
/*
 * Dice.css v1.0
 * Code - MIT License - https://github.com/diafygi/dice-css
 * Images - Public Domain - https://openclipart.org/detail/105931/sixsided-dice-faces-lio-01
 */

.dado {
  display: inline-block;
  min-height: 10em;
  padding-left: 10em;
  background-size: 10em;
  background-repeat: no-repeat;
}

.dadito {
  display: inline-block;
  min-height: 3em;
  padding-left: 3em;
  background-size: 3em;
  background-repeat: no-repeat;
}

.dado-1 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cg transform='translate(113.25%2C-494.1)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-406.5%2C374.7)'%3E%3Crect x='588' y='240.4' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(337.5%2C87.5)' cx='325' cy='227.4' r='12.5' style='fill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E ");
}
.dado-2 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cstyle%3E.s0%7Bfill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000%3B%7D%3C%2Fstyle%3E%3Cg transform='translate(109.9%2C-505.1)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-415.6%2C485.6)'%3E%3Crect x='613' y='40.4' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(326.5%2C-148.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(398.5%2C-76.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E ");
}
.dado-3 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cstyle%3E.s0%7Bfill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000%3B%7D%3C%2Fstyle%3E%3Cg transform='translate(84.9%2C-515.5)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-290.6%2C514.9)'%3E%3Crect x='413' y='2.9' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(126.5%2C-186)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(198.5%2C-114)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(162.5%2C-150)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E ");
}
.dado-4 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cstyle%3E.s0%7Bfill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000%3B%7D%3C%2Fstyle%3E%3Cg transform='translate(90.7%2C-499.7)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-302.7%2C367.8)'%3E%3Crect x='425.5' y='265.4' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(139%2C76.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(139%2C148.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(211%2C76.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(211%2C148.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E ");
}
.dado-5 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cstyle%3E.s0%7Bfill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000%3B%7D%3C%2Fstyle%3E%3Cg transform='translate(89.2%2C-510.5)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-194.9%2C372.3)'%3E%3Crect x='213' y='277.9' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(-73.5%2C89)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-73.5%2C161)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-1.5%2C89)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-1.5%2C161)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-37.5%2C125)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E ");
}
.dado-6 {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg' version='1.1' viewBox='0 0 76.5 76.5' height='21.6' width='21.6'%3E%3Cstyle%3E.s0%7Bfill%3A%23000%3Bstroke-width%3A3%3Bstroke%3A%23000%3B%7D%3C%2Fstyle%3E%3Cg transform='translate(86.2%2C-500.6)'%3E%3Cg transform='matrix(0.5%2C0%2C0%2C0.5%2C-98.2%2C356.2)'%3E%3Crect x='25.5' y='290.4' width='150' height='150' ry='50' rx='50' style='fill%3A%23fff%3Bstroke-width%3A3%3Bstroke%3A%23000'%2F%3E%3Ccircle transform='translate(-261%2C101.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-261%2C173.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-261%2C137.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-189%2C101.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-189%2C173.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3Ccircle transform='translate(-189%2C137.5)' cx='325' cy='227.4' r='12.5' class='s0'%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E");
}
</style>
