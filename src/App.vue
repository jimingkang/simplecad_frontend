<template>
  <v-stage ref="stage" :config="stageSize">
    <v-layer ref="layer" >
      <v-rect
        @click="handleMouseClick"
        @mousemove="handleMouseMove"
        @mouseout="handleMouseOut"

        :config="{
            x: 0,
            y: 0,
width:800,
height:600,
            fill: '#00D2FF',
            stroke: 'black',
            strokeWidth: 1
          }"
      />
      <v-text ref="text" :config="{
          x: 10,
          y: 10,
          fontFamily: 'Calibri',
          fontSize: 24,
          text: text,
          fill: 'black'
        }" />
      <v-line ref="li" :config="{
        x: 0,
        y: 0,
        points:li,
        tension: 0,
        closed: true,
        stroke: 'black',
        fillLinearGradientStartPoint: { x: -50, y: -50 },
        fillLinearGradientEndPoint: { x: 50, y: 50 },
        fillLinearGradientColorStops: [0, 'red', 1, 'yellow']
      }"/>
    </v-layer>
  </v-stage>
</template>

<script>
    const width = window.innerWidth;
    const height = window.innerHeight;

    export default {
        data() {
            return {
                stageSize: {
                    width: width,
                    height: height
                },
                text:'',
                li: []
            };
        },
        methods: {
            writeMessage(message) {
                this.text = message;
            },
            handleMouseOut(event) {
                this.writeMessage('Mouseout triangle');
            },
            handleMouseClick(event) {
               // this.writeMessage(event);
                const mousePos = this.$refs.stage.getStage().getPointerPosition();
                const x = mousePos.x ;
                const y = mousePos.y ;
               this.li.push(x);
                this.li.push(y);
               // this.writeMessage('click');
                //console.log('handleMouseClick');

            },
            handleMouseMove(event) {
                const mousePos = this.$refs.stage.getStage().getPointerPosition();
                const x = mousePos.x ;
                const y = mousePos.y ;
                this.writeMessage('x: ' + x + ', y: ' + y);
            }
        }
    };
</script>
