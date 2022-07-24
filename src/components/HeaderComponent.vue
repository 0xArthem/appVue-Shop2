<template>
    <div class="card container__left">

        <div class="container__panier">
            <a class="btn btn-light a__btn__panier" href="#">
                <em class="fas fa-shopping-basket"></em>
            </a>
        </div>
        <span class="badge ms-2">9</span>

        <div class="container__search">
            <input class="btn btn__search" type="search" placeholder="Recherche par mot ..." autocomplete="off">
        </div>

        <a class="titre_categorie">Recherche par categorie <em class="fas fa-caret-down"></em></a>

        <div class="container__categories">
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Prepa</a>
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Perte de poids</a>
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Prise de muscle</a>
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Boxe</a>
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Femme</a>
            <a class="btn btn__categorie"><em class="fas fa-caret-right"></em> Homme</a>
        </div>

        <!-- <div style="height:2px;background-color:#262626;transform:rotate(-22deg);margin-top:100px;width:362px;margin-left:-50px;"></div> -->
    </div>

    <!---------------------------------------------------->

    <div class="container__right">

        <div class="row row-cols-1 row-cols-md-3 g-4">
            <div class="col" v-for="product in products" :key="product.id">

                <div class="card card__product">

                    <img v-bind:src="product.url" class="card-img-top" alt="product.name"/>

                    <button class="btn btn-dark btn_price">
                        {{product.price }} €
                    </button>

                    <div class="card-body">
                        <h5 class="card-title"><em class="fas fa-caret-right"></em>{{ product.name }}</h5>
                        <p class="card-text">
                        This is a longer card with supporting text below as a natural lead-in to
                        additional content. This content is a little bit longer.
                        </p>
                    </div>
                </div>

                <div style="display:flex;justify-content:center;">
                    <button class="btn btn-light btn_shop" style="margin-top:-23px;position:absolute;z-index:1;border:solid 2px #42b983;box-shadow:none;background-color:white;">
                        <em class="fas fa-shopping-cart btn-rounded"></em>
                    </button>
                </div>
            </div>
            <!-------------------->

        </div>

    </div>
</template>

<script>
export default {
    name: 'HeaderComponent',
    data() {
        return {
            products: [
                {
                    id:1,
                    name: 'Programme 1',
                    url: 'https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTE1fHxzcG9ydHxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60',
                    price: 5
                },
                {
                    id:2,
                    name: 'Programme 2',
                    url: 'https://images.unsplash.com/photo-1579758629938-03607ccdbaba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NTd8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 23
                },
                {
                    id:3,
                    name: 'Programme 3',
                    url: 'https://images.unsplash.com/photo-1517838277536-f5f99be501cd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
                    price: 51
                },
                {
                    id:4,
                    name: 'Programme 4',
                    url: 'https://images.unsplash.com/photo-1574680096145-d05b474e2155?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OTV8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 13
                },
                {
                    id:5,
                    name: 'Programme 5',
                    url: 'https://images.unsplash.com/photo-1546483875-ad9014c88eba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzZ8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 52
                },
                {
                    id:6,
                    name: 'Programme 6',
                    url: 'https://images.unsplash.com/photo-1616279967983-ec413476e824?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NzV8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 9
                }
            ]
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Koulen&display=swap');
.container__left{
    width:300px;
    background-color: #fbfbfb;
    border-right:solid 3px #262626;
    height:1020px;
    border-radius: 1px;
    float:left;
}
.container__right{
    background-color: white;
    width: 1219px;
    height:950px;
    float:right;
}
/*** card__product***/
.row{
    margin:2%;
    margin-top:-15px;
}
.col{
    margin-top:50px;
}
.card__product{
    widows: 200px !important;
    border-radius: 1px;
    border-bottom: solid 2px #42b983;
}
.card-img-top{
    border-radius: 1px;
    height:250px;
    transition-duration: 1.2s;
    cursor: pointer;
}
.card-img-top:hover{
    transform: scale(1.4);
    z-index:1;
    transition-duration: 1.2s;
}
.card-title{
    text-align: center;
    color: black;
    font-family: 'Koulen', cursive;
    letter-spacing: 3px;
}
.fa-caret-right{
    color:#42b983;
    margin-right: 10px;
}
.btn_price{
    border-radius: 1px !important;
    letter-spacing: 1.5px;
    color: #42b983 !important;
    font-family: 'Koulen', cursive;
    font-size:17px !important;
}
.btn_shop:hover{
    transition-duration: 0.2s;
    background-color: #42b983 !important;
    color: #fbfbfb !important;
}

/**********************************************************/
.container__panier{
    margin-top:37px;
    display:flex;
    justify-content: center;
}
.a__btn__panier{
    border-radius: 1px !important;
    background-color: #262626 !important;
}
.fa-shopping-basket{
    font-size: 22px;
    color: #42b983;
    padding:10px;
}
.badge{
    border-radius: 1px;
    color: #42b983;
    z-index: 1 !important;
    width:30px;
    margin-top:-27px !important;
    margin-left:160px !important;
}
.container__search{
    margin-top:130px;
    display: flex;
    justify-content: center;
}
.btn__search{
    border-radius: 1px;
    border-bottom: solid 4px #42b983;
    /* background-color: #262626; */
    /* box-shadow: none; */
    width: 230px;
    color:#262626;
    font-family: 'Koulen', cursive;
    letter-spacing:2px;
    font-size: 14px;
    text-align: center;
}
.btn__search::placeholder{
    color:#262626;
    font-family: 'Koulen', cursive;
    letter-spacing:2px;
    font-size: 14px;
}
.titre_categorie{
    margin-top: 30px;
    text-align: center;
    color:#262626;
    font-family: 'Koulen', cursive;
    letter-spacing:2px;
    font-size: 15px;
}
.fa-caret-down{
    color: #42b983;
}
.container__categories{
    margin-top:10px;
    display:list-item;
    /* width: 250px; */
    text-align: center;
}
.btn__categorie{
    margin:7px;
    border-radius:1px;
    border-bottom:solid 4px #262626;
    /* box-shadow: none; */
}
.btn__categorie:hover{
    border-bottom:solid 4px #42b983;
}
</style>