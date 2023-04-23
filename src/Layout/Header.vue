<template>
    <header class="header">
        <div class="header_side left">
            <img src="../../assets/header/Logo.svg" alt="">
            <div class="header_live">
                <img src="../../assets/header/Live.svg" alt="" class="header_live-icon">
            </div>
            <div class="header_degrees">
                <img src="../../assets/header/Weather.svg" alt="" class="header_degrees-icon">
                <span class="temp">{{ temp }}</span>
            </div>
            <div class="header_winter-summer">
                <span class="time choosed">Лето</span>
                <span class="time">Зима</span>
            </div>
            <div class="header_search">
                <img src="../../assets/header/Search.svg" alt="" class="header_search-icon">
            </div>
        </div>
        <div class="header_side right">
            <div class="header_right-btn lang">RU</div>
            <div class="header_right-btn avatar"><img src="../../assets/header/Profile.svg" alt=""></div>
            <div class="header_right-btn heart"><img src="../../assets/header/Saved.svg" alt=""></div>
            <div class="header_right-btn cart"><img src="../../assets/header/Cart.svg" alt=""></div>
        </div>
    </header>
</template>
<script>
export default {
    props: {
        temp: {
            type: String
        }
    },
    data(){
        return {

        }
    }
}
</script>
<style lang="scss" scoped>
    .header * {
        display: flex;
        align-items: center;
    }
    img{
        width: auto;
        height: 6vh;
        object-fit: cover;
        cursor: pointer;
        &:active{
            cursor: default;
        }
        &:hover{
            opacity: 0.79;
        }
    }
    .header{
        font-family: 'Inter';
        font-size: 1.3vw;
        justify-content: space-between;
        display: flex;
        align-items: center;
        padding: 0.91% 2.1%;
        max-width: 100%;
        overflow: hidden;
        &_side.left{
            gap: 32px;
            justify-content: space-between;
        }
        &_side.right{
            gap: 32px;
            justify-content: space-between;
        }
        @media (max-width: 1133px) {
        &_side.right, &_side.left{
            gap: 3.2vw;
        }
        }
        .temp{
            margin: -6.8px 0 0 9.13px;
            font-size: 1.3vw;
        }
    }
</style>