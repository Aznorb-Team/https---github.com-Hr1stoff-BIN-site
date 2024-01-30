<template>
    <div class="metrics">
        <div class="container">
            <div class="metrics_wrapper">
                <div class="metric_div_title">
                    <p class="metric_title">Метрика</p>
                </div>
                <div class="table_div">
                    <div class="adress">
                        На указанный вами адрес в радиусе:
                        <div class="form_radio_btn">
                            <input id="radio-1" type="radio" name="radio" value="100" checked>
                            <label for="radio-1">100 м</label>
                        </div>
                        
                        <div class="form_radio_btn">
                            <input id="radio-2" type="radio" name="radio" value="300">
                            <label for="radio-2">300 м</label>
                        </div>
                        
                        <div class="form_radio_btn">
                            <input id="radio-3" type="radio" name="radio" value="500">
                            <label for="radio-3">500 м</label>
                        </div>

                        <div class="form_radio_btn">
                            <input id="radio-4" type="radio" name="radio" value="1000">
                            <label for="radio-4">1 км</label>
                        </div>
                        
                        <input type="text" name="text" id="adress_input" placeholder="Напишите адрес">
                        <input type="button" id="accept_input" value="Применить" />
                        
                    </div>
                    <div class="table">
                        <table class="tbl-size">
                            <thead>
                                <tr>
                                    <th>Наименование</th>
                                    <th>Адрес</th>
                                    <th><a href="#"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
<path fill-rule="evenodd" clip-rule="evenodd" d="M15 3.41421V7H18.5858L15 3.41421ZM19 9H15C13.8954 9 13 8.10457 13 7V3H5V21H19V9ZM5 1H15.4142L21 6.58579V21C21 22.1046 20.1046 23 19 23H5C3.89543 23 3 22.1046 3 21V3C3 1.89543 3.89543 1 5 1ZM11 14.5858V10H13V14.5858L14.2929 13.2929L15.7071 14.7071L12 18.4142L8.29289 14.7071L9.70711 13.2929L11 14.5858Z" fill="white"/>
</svg></a></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Абсолют</td>
                                    <td>Профсоюзная улица, 44, Улан-Удэ, Республика Бурятия, 670000</td>
                                </tr>
                                <tr>
                                    <td>Абсолют</td>
                                    <td>Профсоюзная улица, 44, Улан-Удэ, Республика Бурятия, 670000</td>
                                </tr>
                                <tr>
                                    <td>Абсолют</td>
                                    <td>Профсоюзная улица, 44, Улан-Удэ, Республика Бурятия, 670000</td>
                                </tr>
                                <tr>
                                    <td>Абсолют</td>
                                    <td>Профсоюзная улица, 44, Улан-Удэ, Республика Бурятия, 670000</td>
                                </tr>
                                <tr>
                                    <td>Абсолют</td>
                                    <td>Профсоюзная улица, 44, Улан-Удэ, Республика Бурятия, 670000</td>
                                </tr>
                            </tbody>
                        
                        </table>
                    </div>
                    <hr>
                    <div class="result">
                        <div class="result_div_title">
                            <p class="result_title">Итог</p>
                        </div>
                        <div class="result_div_content">
                            <p class="result_content">В радиусе 1 км найдено: 10</p>
                            <p class="result_content">В радиусе 500 м найдено: 5</p>
                            <p class="result_content">В радиусе 300 м найдено: 3</p>
                            <p class="result_content">В радиусе 100 м найдено: 1</p>
                        </div>
                    </div>
                </div>
                
            </div>
        </div>
    </div>
 </template>
 
 <script>
     export default {
         
     }
 </script>
 
 <style lang="scss" scoped>
 
 </style>