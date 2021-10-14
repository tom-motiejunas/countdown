<div class="bg bg-color">
    <div class='bg bg-stars'></div>
    <div class='bg bg-hills'></div>
</div>

<style>
    .bg {
        width: 100%;
        position: absolute;
        left: 0;
        background-repeat: no-repeat;
        background-size: cover;
        z-index:-1;
    }
    .bg-color {
        height: 100%;
        background-color:hsl(235, 16%, 14%);
    }
    .bg-stars {
        background-image: url('../assets/bg-stars.svg');
        height: 100%;
        
    }
    .bg-hills {
        background-image: url('../assets/pattern-hills.svg');
        height: 25%;
        bottom: 0;
    }
</style>
