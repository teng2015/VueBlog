<template>
    <div class="tag_div" v-if="show">
        <input
                type="text"
                class="newInput"
                placeholder="标签"
                v-model="text"
                onfocus="this.placeholder=''"
                onblur="this.placeholder='标签'"
                @keydown.enter="addTag"
        />
        <i class="iconfont icon-shanchu1" @click="delTag"></i>
    </div>
</template>

<script>
export default {
    data () {
        return {
            show: true
        }
    },
    props: {
        text: String,
        tags: Array,
        index: Number
    },
    methods: {
        delTag () {
            this.tags.splice(this.index, 1)
        },
        addTag () {
            let currentIndex = this.index
            let currentValue = this.tags[currentIndex]
            let isOnly = true
            while (currentIndex) {
                if (currentValue.toLowerCase() === this.tags[currentIndex - 1].toLowerCase()) {  // 标签去重
                    alert('标签不能重复！')
                    isOnly = false
                    this.tags.splice(this.index, 1)
                    break
                } else {
                    currentIndex--
                }
            }
            if (isOnly) {
                this.tags.push('')
                setTimeout(() => {
                    document.getElementsByClassName('newInput')[this.index + 1].focus()
                }, 0)
            }
        }
    },
    computed: {
        text: {
            get () {
                return this.tags[this.index]
            },
            set (value) {
                this.tags[this.index] = value.trim()
            }
        }
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.tag_div {
    position: relative;
    display: inline-block;
    &:hover i{
         opacity: 1;
         transition: 1s;
     }
    .newInput {
        border: none;
        border-bottom: 2px solid #ffc520;
        outline: none;
        background: transparent;
        color: #ffffff;
        margin-bottom: 10px;
        margin-right: 5px;
        text-align: center;
        width: 100px;
        height: 30px;
        font-size: 16px;
    }
    i {
        position: absolute;
        right: 0;
        top: -5px;
        font-size: 16px;
        color: #ffc520;
        cursor: pointer;
        opacity: 0;
        transition: 1s;
        &:hover {
             color: darkturquoise;
             font-weight: bolder;
         }
    }
}
</style>
