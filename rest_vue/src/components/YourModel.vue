<template>
    <div>
      <div class="header">
        <div class="header_1">
          <h1>Информационные ресурсы</h1>
        </div>
        <div class="header_2">
          <a href="http://localhost:8000/admin/">Административная панель</a>
        </div>
      </div>

      <div class="content">
        <div  class="container" v-for="item in items" :key="item.id">
                      <span class="coupontooltip">
                                <div class ="description">{{item.description}} </div>  
                                <a href="{{ item.slug}}">{{ item.name }}</a>
                      </span>
                      <div class="image">
                              <img :src="item.image"  v-if="item.image"/>
                      </div>
                      <div class="name_with_tooltip">
                        <div class="name">
                               <p href="{{ item.slug}}">{{ item.name }}</p>
                        </div>            
                    </div>
        </div>
      </div>
      <div class="footer">

      </div>
    </div>
</template>
<style>
  .header{
    text-align: center;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 3fr 1fr;
    grid-column-gap: 0px;
    grid-row-gap: 0px; 
  }
  .content{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px; /* Расстояние между карточками */
    padding: 20px; /* Внутренние отступы */
  }
  .container{
    display: block;
    border: 1px solid #ccc; 
    border-radius: 8px; 
    overflow: hidden; /* Скрытие содержимого, выходящего за границы карточки */
    text-align: center; 
    background-color: #fff; 
  }
  .name_with_tooltip{
    display: grid;
    grid-template-columns: 11fr 1fr;
    grid-template-rows: 1fr;
    grid-column-gap: 0px;
    grid-row-gap: 0px; 
  }
  .name{
    font-size: 1.25em; /* Размер шрифта для названия */
    margin: 10px 0; /* Отступы сверху и снизу */
  }
  .tooltip_button{
    font-size: 25px;
    font-weight: bold;
    line-height: 20px;
    position: relative;
    text-align: center;
    width: 20px;
    margin-top: 1vh;
  }
  .image{
    padding-top: 1vh;
  }
  img{
    width: 100%; /* Ширина изображения */
    height: auto; /* Автоматическая высота */
  }
  .coupontooltip{
    display: none;
    background: #f5e8e8;
    padding: 100px;
    position: absolute;
    z-index: 1000;
    width: 45vh;
    height: 10vh;
    margin-top:19vh;
    margin-left: 9vh; 
    border-radius: 3%;
  }
  .container:hover .coupontooltip {
    display: block;
    -webkit-box-shadow: 1px 3px 45px 76px rgba(34, 60, 80, 0.2);
    -moz-box-shadow: 1px 3px 45px 76px rgba(34, 60, 80, 0.2);
    box-shadow: 1px 3px 45px 76px rgba(34, 60, 80, 0.2);
    opacity: 0.9; /* 50% прозрачность */
  }
  .coupontooltip a{
    font-size: 15px;
    position: absolute;
    bottom: 0;
    left: 0;
  }

.description {
    width: 45vh; /* Заполняем всю ширину контейнера */
    font-size: 13px;
    position: absolute;
    top: 0;
    left: 0; 
    color:black;
}
</style>
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        items: []
      };
    },
    created() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await axios.get('http://localhost:8000/api/orders/');
          this.items = response.data;
        } catch (error) {
          console.error(error);
        }
      }
    }
  };
  </script>
  