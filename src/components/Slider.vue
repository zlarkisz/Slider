<template>
    <div class="slider">
        <button @click="goToPrev()"><i class="fa fa-chevron-left"></i>НАЗАД</button>
        <div class="slider-items">
            <div class="translation" ref="translation">
                <!--выводим количество слайдов через v-for-->
                <slider-item ref="slider1" :key="i" v-for="(slide, i) in slides"/>
            </div>
        </div>
        <button @click="goToNext()">ДАЛІ<i class="fa fa-chevron-right"></i></button>
    </div>
</template>

<script>
	import SliderItem from './SliderItem'
	export default {
		components: {
			SliderItem
		},
		data () {
			return {
				// кол-во слайдов
				slides: 10,
				// номер текущего слайда
				currentIndex: 5
			}
		},
		methods: {
			// Методы для свапа слайдов. 195 - ширина слайда, изменяю положение слайдов свойством стилей left. $refs - локальная референция Vue
			goToPrev () {
				let oldIndex = this.currentIndex
				this.currentIndex++
				this.currentIndex %= (this.slides - 2)
				this.$refs.translation.style.left = -(195 * this.currentIndex) + 'px'
				this.$refs.slider1[oldIndex].$el.style.opacity = 0
				this.$refs.slider1[oldIndex].$el.style.transform = 'scale(1.3)'
				setTimeout(() => {
					this.$refs.slider1[oldIndex].$el.style.opacity = 1
					this.$refs.slider1[oldIndex].$el.style.transform = 'scale(1)'
				}, 600)
			},
			goToNext () {
				let oldIndex = this.currentIndex + 2
				if (this.currentIndex <= 0) {
					this.currentIndex = this.slides - 2
				}
				this.currentIndex--
				this.currentIndex %= (this.slides - 2)
				this.$refs.translation.style.left = -(195 * this.currentIndex) + 'px'
				this.$refs.slider1[oldIndex].$el.style.opacity = 0
				this.$refs.slider1[oldIndex].$el.style.transform = 'scale(1.3)'
				setTimeout(() => {
					this.$refs.slider1[oldIndex].$el.style.opacity = 1
					this.$refs.slider1[oldIndex].$el.style.transform = 'scale(1)'
				}, 600)
			}
		},
		// mounted для того, чтобы изначально свапнуть на нужный текущий слайд, указанный выше
		mounted () {
			this.$refs.translation.style.left = -(195 * this.currentIndex) + 'px'
		}
	}
</script>

<style lang="less" scoped>
    .translation {
        display    : block;
        position   : relative;
        transition : left 0.6s ease-out;
    }

    /*стили блока слайдера*/
    .slider {
        display         : -webkit-box;
        display         : -moz-box;
        display         : -ms-flexbox;
        display         : -webkit-flex;
        display         : flex;
        justify-content : space-between;
        align-items     : center;
        margin          : 50px;
        width           : 100%;
        .slider-items {
            overflow : hidden;
            width    : 585px;
            height : 200px;
        }
        div {
            display : flex;
            display : -webkit-box;
            display : -moz-box;
            display : -ms-flexbox;
            display : -webkit-flex;
        }
        button {
            font-weight   : bold;
            background    : none;
            color         : white;
            border        : 2px solid white;
            border-radius : 5px;
            width         : 150px;
            padding       : 15px 0;
            font-size     : 24px;
            /*поворот книпок, чтобы соответствовали макету*/
            &:first-child {
                transform : perspective(20em) rotateY(30deg);
            }
            &:last-child {
                transform : perspective(20em) rotateY(-30deg);
            }
            &:hover {
                cursor : pointer;
                background : white;
                color      : #16ADAB;
                transition : 0.3s;
            }
            &:focus {
                outline : none;
            }
        }
    }
</style>