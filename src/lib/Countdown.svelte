<script lang="ts">
    import {onMount} from 'svelte'

    const totalTime = {
        days: 8,
        hours: 23,
        minutes: 55,
        seconds: 41,
    }
    const flippers = [false, false, false, false]

    onMount(() => {  
        const secondsData = document.querySelectorAll('.seconds')
        const minutesData = document.querySelectorAll('.minutes')
        const hoursData = document.querySelectorAll('.hours')
        const daysData = document.querySelectorAll('.day')

        const allTimeData = [secondsData, minutesData, hoursData, daysData];

        async function reduceCountdown(timeData, i) {
            await setTimeout(() => {
                if(Number(timeData[1].textContent)-1 < 0) {
                    timeData[1].textContent = '60';
                    timeData[3].textContent = '60';
                }
                    timeData[1].textContent = `${Number(timeData[1].textContent)-1}`.padStart(2, '0');
                    timeData[3].textContent = `${Number(timeData[3].textContent)-1}`.padStart(2, '0');
                    flippers[i] = !flippers[i]
            }, 500)
            
            if(Number(timeData[2].textContent)-1 < 0) {
                    timeData[0].textContent = '60';
                    timeData[2].textContent = '60';
                    if(i == 3) {
                        return;
                    } else {
                        reduceCountdown(allTimeData[i+1], i+1)
                    }
            }
                timeData[0].textContent = `${Number(timeData[0].textContent)-1}`.padStart(2, '0');
                timeData[2].textContent = `${Number(timeData[2].textContent)-1}`.padStart(2, '0');
         
                flippers[i] = !flippers[i]
        }
        let totalSeconds = totalTime.days*60*60*24 + totalTime.hours*60*60 + totalTime.minutes*60 + totalTime.seconds;
       const x = setInterval(async () => {
           totalSeconds--;

            if(totalSeconds == 0) {
                clearInterval(x)
            }
        reduceCountdown(allTimeData[0], 0)
        }, 1000)
    })
</script>

<section class="countdown">

    <div class="time-block">
        <div class="time-drops">
          <div class="leaf" class:flipped={flippers[3]}>
              <figure class="rear day">{totalTime.days.toString().padStart(2, '0')}</figure>
              <figure class='front day'>{totalTime.days.toString().padStart(2, '0')}</figure>
          </div>
          <div class="top day">{totalTime.days.toString().padStart(2, '0')}</div>
          <div class="bottom day">{totalTime.days.toString().padStart(2, '0')}</div>
          <div class="semi-circles"></div>
          <div class="semi-circles"></div>
        </div>
        <h2>DAYS</h2>
    </div>


        <div class="time-block">
            <div class="time-drops">
              <div class="leaf" class:flipped={flippers[2]}>
                  <figure class="rear hours">{totalTime.hours.toString().padStart(2, '0')}</figure>
                  <figure class='front hours'>{totalTime.hours.toString().padStart(2, '0')}</figure>
              </div>
              <div class="top hours">{totalTime.hours.toString().padStart(2, '0')}</div>
              <div class="bottom hours">{totalTime.hours.toString().padStart(2, '0')}</div>
              <div class="semi-circles"></div>
              <div class="semi-circles"></div>
            </div>
        <h2>HOURS</h2>
    </div>

        <div class="time-block">
            <div class="time-drops">
              <div class="leaf" class:flipped={flippers[1]}>
                  <figure class="rear minutes">{totalTime.minutes.toString().padStart(2, '0')}</figure>
                  <figure class='front minutes'>{totalTime.minutes.toString().padStart(2, '0')}</figure>
              </div>
              <div class="top minutes">{totalTime.minutes.toString().padStart(2, '0')}</div>
              <div class="bottom minutes">{totalTime.minutes.toString().padStart(2, '0')}</div>
              <div class="semi-circles"></div>
              <div class="semi-circles"></div>
            </div>
        <h2>MINUTES</h2>
    </div>

        <div class="time-block">
            <div class="time-drops">
              <div class="leaf" class:flipped={flippers[0]}>
                  <figure class="rear seconds">{totalTime.seconds.toString().padStart(2, '0')}</figure>
                  <figure class='front seconds'>{totalTime.seconds.toString().padStart(2, '0')}</figure>
              </div>
              <div class="top seconds">{totalTime.seconds.toString().padStart(2, '0')}</div>
              <div class="bottom seconds">{totalTime.seconds.toString().padStart(2, '0')}</div>
              <div class="semi-circles"></div>
              <div class="semi-circles"></div>
            </div>
        <h2>SECONDS</h2>
    </div>
</section>


<style>
    .countdown {
        display: flex;
        justify-content: center;
        width: 100%;
    }
    .time-block {
        margin: 1rem;
    }
    .time-block h2 {
        text-align: center;
        font-size: 14px;
        color: var(--primary-blue);
        letter-spacing: 5px;
    }
    .time-drops {
        background-color: var(--neutral-desaturated-blue);
        position: relative;
        width: 125px;
        height: 125px;
        border-radius: 10px;
        margin-bottom: 1rem;
        box-shadow: var(--neutral-very-dark-blue) 0 8px;
    }
    .time-drops:after {
        content: '';
        z-index: 2;
        position: absolute;
        bottom: 0;
        width: 100%;
        height: 50%;
        border-radius: 10px;
        border-top: 1px rgba(42, 43, 65, 0.39) solid;
    }
    .time-drops div, figure {
        margin: 0;
        position: absolute;
        text-align: center;
        font-size: 55px;
        border-radius: 10px;
        color: var(--primary-red);

    }
    .time-drops .leaf {
        height: 100%;
        width: 100%;
        z-index: 1;
        transform-style: preserve-3d;
        
    }
    .flipped {
        transition: all 0.5s linear;
        transform: rotateX(-180deg)
    }
    .time-drops .rear {
        height: 50%;
        width: 100%;
        overflow: hidden;
        line-height: 0;
        transform: rotateX(-180deg);
        background-color: var(--neutral-desaturated-blue);
        border-radius: 0px 0px 10px 10px;
      
    }
    .time-drops .front {
        height: 50%;
        width: 100%;
        overflow: hidden;
        line-height: 125px;
        transform: rotateX(0deg);
        backface-visibility: hidden;
        -webkit-backface-visibility: hidden;
        background-color: rgb(42, 43, 65);
        border-radius: 10px 10px 0 0;
     
    } 
    .time-drops .top {
        height: 50%;
        width: 100%;
        overflow: hidden;
        line-height: 125px;
        background-color: rgb(42, 43, 65);
        border-radius: 10px 10px 0 0;
    
    }
    .time-drops .bottom {
        height: 50%;
        width: 100%;
        overflow: hidden;
        background-color: var(--neutral-desaturated-blue);
        line-height: 0;
        bottom: 0;
    }
    .semi-circles {
        position: absolute;
        width:6px;
        height: 10px;
        background-color: var(--neutral-very-dark-blue);
        top:calc(50% - 5px);
        z-index: 10;
        border-radius: 0 !important;
        border-top-right-radius: 20px !important;
        border-bottom-right-radius: 20px !important;
    }
    .semi-circles:last-child {
        left:auto;
        right:0px;
        border-radius: 0 !important;
        border-top-left-radius: 20px !important;
        border-bottom-left-radius: 20px !important;
    }
    @media only screen and (max-width: 650px) {
        .time-block {
            margin: 0.5rem
        }
        .time-drops {
            width: 70px;
            height: 70px;
        }
        h2 {
            font-size: 7px !important;
        }
        .front, .top {
            line-height: 70px !important;
        }
        div, figure {
            font-size: 40px !important;
        }
    }
</style>