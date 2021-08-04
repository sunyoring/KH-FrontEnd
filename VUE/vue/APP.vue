<!-- 1. template : 화면에 표시할 요소를 정의 -->
<template>
    <div id="app">
        {{message}}
    </div>
</template>


<!-- 2. script : 뷰 컴포넌트 내용 정의 -->

<script>
//ex) import Login from  './login.vue' 컴포넌트가 될 수 도있음 아래서 사용 가능해진다.
import { defineComponent } from '@vue/composition-api' 
// 외부에 있는 파일 읽어들일 때 import , 내 기능을 다른곳에서 아용할 수 있게 내보낼 때 export
export default ({ 
    data(){
        return {
            message:'intro to vue with vue3'
        }
    }
})
</script>



<!-- 3. style : 템플릿에 적용할 css를 정의 -->
<style>
    div{
        font-size:20px;
    }

</style>
