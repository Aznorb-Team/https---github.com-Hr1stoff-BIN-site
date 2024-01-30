<template>
    <div id="map" style="width: 1440px; height: 700px;">
        <div class="filter">
            <div class="filter_div_title">
                <div class="filter_title">
                    Фильтр
                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22" fill="none">
                        <path
                            d="M2.2282 5.25662L8.93751 13.0625V19.25L13.0625 16.5V13.0625L19.7718 5.25662C20.1541 4.80975 19.833 4.125 19.2404 4.125H2.75963C2.16701 4.125 1.84595 4.80975 2.2282 5.25662Z"
                            stroke="black" stroke-width="2" stroke-miterlimit="10" stroke-linecap="round"
                            stroke-linejoin="round" />
                    </svg>
                    <input type="button" id="download_excel_button" @click="downloadExcel" value="Скачать Excel"
                        v-show="downloadButton" />
                </div>
            </div>

            <div class="filter-content">
                <fieldset class="fieldset_shop">
                    <legend>Отображать</legend>

                    <div>
                        <input type="checkbox" class="checkbox" id="nash" name="nash" value="Наш" v-model="checkShops" />
                        <label for="nash">Наш</label>
                    </div>

                    <div>
                        <input type="checkbox" class="checkbox" id="sreda" name="sreda" value="Среда"
                            v-model="checkShops" />
                        <label for="sreda">Среда</label>
                    </div>
                    <div>
                        <input type="checkbox" class="checkbox" id="nikol" name="nikol" value="Николаевский"
                            v-model="checkShops" />
                        <label for="nikol">Николаевский</label>
                    </div>

                    <div>
                        <input type="checkbox" class="checkbox" id="titan" name="titan" value="Титан"
                            v-model="checkShops" />
                        <label for="titan">Титан</label>
                    </div>
                    <div>
                        <input type="checkbox" class="checkbox" id="absolut" name="absolut" value="Абсолют"
                            v-model="checkShops" />
                        <label for="absolut">Абсолют</label>
                    </div>

                    <div>
                        <input type="checkbox" class="checkbox" id="redandwhite" name="redandwhite" value="КрасноеБелое"
                            v-model="checkShops" />
                        <label for="redandwhite">Красное&Белое</label>
                    </div>
                    <div>
                        <input type="checkbox" class="checkbox" id="bristol" name="bristol" value="Бристоль"
                            v-model="checkShops" />
                        <label for="bristol">Бристоль</label>
                    </div>
                </fieldset>
                <fieldset class="fieldset_radius">
                    <legend>Радиус</legend>

                    <div>
                        <input type="radio" id="stometrov" name="radius" value="100" v-model="radius" checked />
                        <label for="stometrov">100 метров</label>
                    </div>

                    <div>
                        <input type="radio" id="tristometrov" name="radius" v-model="radius" value="300" />
                        <label for="tristometrov">300 метров</label>
                    </div>

                    <div>
                        <input type="radio" id="fivemetrov" name="radius" v-model="radius" value="500" />
                        <label for="fivemetrov">500 метров</label>
                    </div>

                    <div>
                        <input type="radio" id="onekm" name="radius" v-model="radius" value="1000" />
                        <label for="onekm">1000 метров</label>
                    </div>
                </fieldset>
                <input type="button" id="accept_filter_input" @click="accepsFilter" value="Применить" />
            </div>

        </div>
        <div class="search_address">
            Укажите адрес:
            <input type="text" name="search" id="search" v-model="adress">
            <button type="button" @click="searchAdressFunction">Найти</button>
        </div>
    </div>
</template>
    
<script>
import * as XLSX from "xlsx";

export default {
    data() {
        return {
            radius: 100,
            adress: "",
            checkShops: ["Наш", "Среда", "Николаевский", "Титан", "Абсолют", "КрасноеБелое", "Бристоль"],
            objects: null,
            excelShops: [],
            downloadButton: false,
        };
    },
    mounted() {
        this.initMap();
    },
    methods: {
        initMap() {
            ymaps.ready(() => {
                window.myMap = new ymaps.Map("map", {
                    center: [51.834809, 107.584547],
                    zoom: 12
                });

                window.nashCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#darkOrangeDotIcon'
                });
                window.sredaCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#blueDotIcon'
                });
                window.nikolCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#redDotIcon'
                });
                window.titanCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#greenDotIcon'
                });
                window.ablosutCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#yellowDotIcon'
                });
                window.krasnoebeloeCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#pinkDotIcon'
                });
                window.bristolCollection = new ymaps.GeoObjectCollection(null, {
                    preset: 'islands#nightDotIcon'
                });
                fetch('shops.json')
                    .then(response => response.json())
                    .then(data => {


                        window.shops = data.features;

                        window.shops.forEach(shop => {


                            const placemark = new ymaps.Placemark([shop.geometry.coordinates[0], shop.geometry.coordinates[1]], {
                                iconCaption: shop.properties.balloonContent,
                                hintContent: shop.properties.hintСontent,
                                balloonContentHeader: shop.properties.balloonContent,
                                balloonContentBody: shop.properties.hintСontent,
                                balloonContentFooter: [shop.geometry.coordinates[0], shop.geometry.coordinates[1]],
                            });
                            console.log(shop.properties.hintСontent);
                            switch (shop.properties.balloonContent) {
                                case "Наш":
                                    window.nashCollection.add(placemark);
                                    break;
                                case "Среда":
                                    window.sredaCollection.add(placemark);
                                    break;
                                case "Николаевский":
                                    window.nikolCollection.add(placemark);
                                    break;
                                case "Титан":
                                    window.titanCollection.add(placemark);
                                    break;
                                case "Абсолют":
                                    window.ablosutCollection.add(placemark);
                                    break;
                                case "КрасноеБелое":
                                    window.krasnoebeloeCollection.add(placemark);
                                    break;
                                case "Бристоль":
                                    window.bristolCollection.add(placemark);
                                    break;
                            }

                        });
                    })
                    .catch(error => {
                    });
                window.myMap.geoObjects.add(window.nashCollection);
                window.myMap.geoObjects.add(window.sredaCollection);
                window.myMap.geoObjects.add(window.nikolCollection);
                window.myMap.geoObjects.add(window.titanCollection);
                window.myMap.geoObjects.add(window.ablosutCollection);
                window.myMap.geoObjects.add(window.krasnoebeloeCollection);
                window.myMap.geoObjects.add(window.bristolCollection);

                window.myMap.controls.remove('trafficControl');
                window.myMap.controls.remove('fullscreenControl');
                window.myMap.controls.remove('geolocationControl');
                window.myMap.controls.remove('listBox');
                window.myMap.controls.remove('listBoxItem');
                window.myMap.controls.remove('manager');
                window.myMap.controls.remove('routeButton');
                window.myMap.controls.remove('routeEditor');
                window.myMap.controls.remove('rulerControl');
                window.myMap.controls.remove('searchControl');
                window.myMap.controls.remove('storage');
                window.myMap.controls.remove('typeSelector');
                window.myMap.controls.remove('zoomControl');

            });
        },
        getDistanceBetweenPoints(point1, point2) {
            const R = 6378137;
            const dLat = this.degreesToRadians(point2[0] - point1[0]);
            const dLon = this.degreesToRadians(point2[1] - point1[1]);
            const a =
                Math.sin(dLat / 2) * Math.sin(dLat / 2) +
                Math.cos(this.degreesToRadians(point1[0])) * Math.cos(this.degreesToRadians(point2[0])) *
                Math.sin(dLon / 2) * Math.sin(dLon / 2);
            const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
            return R * c;
        },

        degreesToRadians(degrees) {
            return degrees * (Math.PI / 180);
        },
        drawCircle(coordinates) {
            if (this.radiusObject != null) {
                window.myMap.geoObjects.remove(this.radiusObject);
                if (window.violetCollection != null)
                    window.myMap.geoObjects.remove(window.violetCollection);
            }
            this.radiusObject = new ymaps.Circle([coordinates, this.radius], {}, { fillOpacity: 1 });

            window.myMap.geoObjects.add(this.radiusObject);
            window.violetCollection = new ymaps.GeoObjectCollection(null, {
                preset: 'islands#violetIcon'
            })
            this.excelShops = [];

            window.shops.forEach(shop => {
                if (this.radiusObject.geometry.contains([shop.geometry.coordinates[0], shop.geometry.coordinates[1]])) {
                    if (this.checkShops.indexOf(shop.properties.balloonContent) != -1) {

                        const placemark = new ymaps.Placemark([shop.geometry.coordinates[0], shop.geometry.coordinates[1]], {
                            hintContent: shop.properties.hintСontent,
                            balloonContent: shop.properties.balloonContent
                        });
                        window.violetCollection.add(placemark);

                        this.excelShops.push({
                            id: shop.id,
                            name: shop.properties.balloonContent,
                            address: shop.properties.hintСontent,
                            coordinates: shop.geometry.coordinates[0] + ";" + shop.geometry.coordinates[1],
                        });
                    }
                }
            });
            window.myMap.geoObjects.add(window.violetCollection);
        },
        searchAdressFunction() {
            if (this.radiusObject != null) {
                window.myMap.geoObjects.remove(this.radiusObject);
                if (window.violetCollection != null)
                    window.myMap.geoObjects.remove(window.violetCollection);
            }
            this.radius = 100;
            var myGeocoder = ymaps.geocode(this.adress);
            if (window.globalPlacemark != null)
                window.myMap.geoObjects.remove(window.globalPlacemark);
            myGeocoder.then(
                function (res) {
                    var firstGeoObject = res.geoObjects.get(0),
                        // Координаты геообъекта.
                        coords = firstGeoObject.geometry.getCoordinates(),
                        // Область видимости геообъекта.
                        bounds = firstGeoObject.properties.get('boundedBy');

                    firstGeoObject.options.set('preset', 'islands#darkBlueDotIconWithCaption');
                    // Получаем строку с адресом и выводим в иконке геообъекта.
                    firstGeoObject.properties.set('iconCaption', firstGeoObject.getAddressLine());
                    // console.log(firstGeoObject.geometry._coordinates);
                    // Добавляем первый найденный геообъект на карту.
                    //newCenter =
                    // Масштабируем карту на область видимости геообъекта.
                    window.myMap.setBounds(bounds, {
                        // Проверяем наличие тайлов на данном масштабе.
                        checkZoomRange: true
                    });
                    window.newCenter = firstGeoObject.geometry._coordinates;
                    //drawCircle(firstGeoObject.geometry._coordinates);

                    const placemark = new ymaps.Placemark(firstGeoObject.geometry._coordinates, {
                        hintContent: "Ваша точка",
                        balloonContent: "Ваша точка"
                    }, {
                        iconLayout: 'default#image',
                        // Своё изображение иконки метки.
                        iconImageHref: 'metka.png',
                        iconImageSize: [42, 42],
                        iconImageOffset: [-21, -42]
                    });


                    window.globalPlacemark = placemark;
                    window.myMap.geoObjects.add(window.globalPlacemark);
                    window.globalId = window.myMap.geoObjects.getLength() - 1;
                    window.globalCoordinates = firstGeoObject.geometry._coordinates;
                },
                function (err) {
                    alert('Ошибка');
                }
            );
        },
        accepsFilter() {
            this.downloadButton = true;
            console.log(this.excelShops);
            this.setFilters();
            if (this.adress != "") {
                var geoObject = window.myMap.geoObjects.get(window.globalId);
                this.drawCircle(window.globalCoordinates);

                console.log(window.violetCollection);

            }
        },
        setFilters() {
            if (this.checkShops.indexOf("Наш") != -1)
                window.myMap.geoObjects.add(window.nashCollection);
            else
                window.myMap.geoObjects.remove(window.nashCollection);

            if (this.checkShops.indexOf("Среда") != -1)
                window.myMap.geoObjects.add(window.sredaCollection);
            else
                window.myMap.geoObjects.remove(window.sredaCollection);

            if (this.checkShops.indexOf("Николаевский") != -1)
                window.myMap.geoObjects.add(window.nikolCollection);
            else
                window.myMap.geoObjects.remove(window.nikolCollection);

            if (this.checkShops.indexOf("Титан") != -1)
                window.myMap.geoObjects.add(window.titanCollection);
            else
                window.myMap.geoObjects.remove(window.titanCollection);

            if (this.checkShops.indexOf("Абсолют") != -1)
                window.myMap.geoObjects.add(window.ablosutCollection);
            else
                window.myMap.geoObjects.remove(window.ablosutCollection);

            if (this.checkShops.indexOf("КрасноеБелое") != -1)
                window.myMap.geoObjects.add(window.krasnoebeloeCollection);
            else
                window.myMap.geoObjects.remove(window.krasnoebeloeCollection);

            if (this.checkShops.indexOf("Бристоль") != -1)
                window.myMap.geoObjects.add(window.bristolCollection);
            else
                window.myMap.geoObjects.remove(window.bristolCollection);
        },
        downloadExcel() {
            const ws = XLSX.utils.json_to_sheet(this.excelShops);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'Sheet1');
            XLSX.writeFile(wb, this.adress + '.xlsx');
        }
    }
};
</script>
