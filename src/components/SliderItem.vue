<template>
    <div class="slider-item-container">
        <div class="slider-item">
            <!--байндим путь к картинке-->
            <img :src="imgPath">
        </div>
    </div>
</template>

<script>
	export default {
		props: ['slide'],
		computed: {
			imgPath: function () {
				// рандомная генерация картинки
				return require('../assets/img/boy' + (Math.floor(Math.random() * (2)) + 1) + '.png')
			}
		}
	}
</script>

<style lang="less" scoped>
    .slider-item-container {
        height        : 135px;
        width         : 135px;
        margin        : 35px 25px;
        display       : -webkit-box;
        display       : -moz-box;
        display       : -ms-flexbox;
        display       : -webkit-flex;
        display       : flex;
        align-items   : flex-end;
        justify-content : center;
        border        : 5px solid #98e2dd;
        border-radius : 50%;
        transition    : 0.3s ease;
        &:hover {
            border-color : white;
            box-shadow   : 0 10px 10px -5px rgba(1, 1, 1, 0.4);
            transition   : 0.3s ease;
            img {
                animation-name     : jumpAnimation;
                animation-duration : 0.5s;
                transform          : translateY(15px);
                transition         : 0.5s ease;
            }
        }
        /*Анимация выпрыгивания персонажа*/
        @keyframes jumpAnimation {
            0% {
                transform         : translateY(20px);
            }
        }
        /*Стили для картинки и внутреннего блока единицы слайдера*/
        .slider-item {
            display: flex;
            display: -webkit-box;
            display: -moz-box;
            display: -ms-flexbox;
            display: -webkit-flex;
            clip-path: inset(-100% 0 0 round 0%);
            justify-content: center;
            align-items: flex-end;
            img {
                transform: translateY(2px);
                transition: 0.3s ease;
            }
        }
    }


</style>