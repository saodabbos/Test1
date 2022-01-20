<template>
    <div class=" br p-4">
    <div class = "wrapper">
                <div class='d-flex flex-row-reverse justify-content-between my-2 w-100'> 
                     <div>
                     <button type="button" @click='isQuest=!isQuest' class='btn btn-outline-primary'> {{isQuest?'Скрыть все ответы':'Показать все ответы '}}</button>
                     </div>
                    <div>
                        <h2 class='mx-5 main'> ИНФОРМАЦИОННЫЙ ТЕХНОЛОГИИ</h2>
                    </div>
               </div> 
               <div class='w-75 fontf'>
                 <span style='color:red'> Примечания:</span>  Пишите ответа заглавном или маленьком. Разницы нет. После  того как вводите ответ нажмите на Enter! 
               </div > 
            <div v-for ='(question, index) in questions' :key="question.id">
                <div class='quest'> {{question.id}}. {{question.question}}  
                <transition name="slide-fade">
                <p class='answers px-2' v-if='isQuest'>  {{question.answer}}</p>
                </transition>
                </div>
                
                <div class=' w-75 d-flex justify-content-around my-2'>                    
                   <div class=' w-50'>
                        <input type = "text" class='form-control d-block px-2 mx-4' placeholder = "Введите ответ и нажмите Enter " v-model.trim = 'question.mod' 
                        @keydown.enter = 'func(index, $event)' v-on:input = 'del(index, $event)'>
                    </div>                       
                   
                   <div  class='w-25'>
                   <transition name="bounce">
                        <p class='anss' style = "color: green" v-if = "question.color == 'green'"> Правильно!</p>
                        <p class='anss' style = "color: red" v-if = "question.color == 'red'" > Не правильно!</p>
                   </transition>
                   </div>
                </div>
                <br>
            </div>
    </div>
        
    </div>
</template>

<script>
export default {
    props:{
        questions:Array
    },
    data () {
        return {
            isQuest:false
        }
    },
    methods:{
    del(index, event){
        let target = event.target;
        target.classList.remove('elem1');
        target.classList.remove('elem2');
        this.questions[index].color = '';
    },
    func(index, event){
        if(!(this.questions[index].mod == '')){
        let target = event.target;
        if(this.questions[index].mod.toUpperCase() == this.questions[index].answer.toUpperCase()){
            this.questions[index].color = 'green';
            target.classList.add('elem1');
            target.classList.remove('elem2');
        }
        else{
            this.questions[index].color = 'red';
            target.classList.add('elem2');
            target.classList.remove('elem1');
        }
    }
    }
} 
}
</script>

<style lang="scss" scoped>
.br{
    box-shadow: 0 0 5px 2px grey;
}
.main{
    color: aqua;
    text-align:center;
}
.fontf{
    font-family:Tahoma;
    font-size:20px;
    color:orange;
    text-align:justify;
}
.elem1 {
        background-color: green;
        border: none;
        color: white;
    }
    .elem2 {
        background: red;
        border: none;
        color:white;
    }
    input{
        background:white;
        max-width:250px;
    }
    .quest{
        font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        font-size:20px;
    }
    .answers{
        display:inline-block;
        background:green;
        color:white;
        border-radius:10px;
        font-size:17px;
        margin:0;
    }
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to {
  transform: translateX(50px);
  opacity: 0;
}
.anss{
    display:inline-block;
}
.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>