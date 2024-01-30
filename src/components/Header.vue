<template>
    <header class="header">
        <div class="container">
            <div class="header__wrapper">
                <div class="header__logo">
                    <div class="header__image">
                        <svg class="header__image-logo" viewBox="0 0 108 41">
                            <use xlink:href="#logoBIN"></use>
                        </svg>
                    </div>
                </div>
                <nav class="header__nav">
                    <ul class="header__list">
                        <li class="header__item">
                            <a href="" class="header__link">Главная</a>
                        </li>
                        <div class="header__list-inside">
                            <li class="header__item">
                                <a href="" class="header__link">Карта</a>
                            </li>
                            <li class="header__item">
                                <a href="" class="header__link">Документация</a>
                            </li>
                            <li class="header__item">
                                <a href="" class="header__link">Поддержка</a>
                            </li>
                            <li class="header__item">
                                <a href="" class="header__link">О нас</a>
                            </li>
                        </div>
                    </ul>
                </nav>
                <div class="header__search">
                    <form class="header__form" role="search" method="get" action="/search">
                        <input type="search" name="search-text" class="header__input" />
                        <button class="header__btn">
                            <svg class="header__btn-icon" viewBox="0 0 512 512">
                                <use xlink:href="#search"></use>
                            </svg>
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
export default {

}
</script>

<style>
</style>