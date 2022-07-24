<template>
    <div class="card container__left">

        <div class="container__panier">
            <a v-on:click="showShop = !showShop" class="btn btn-light a__btn__panier" href="#">
                <em class="fas fa-shopping-basket"></em>
            </a>
        </div>
        <!--badge itemtotalaccount-->
        <span v-if="cart.length > 0" class="badge ms-2">{{ itemTotalAmount }}</span>

        <div id="panier_div" v-if="cart.length > 0">
        <!-- affichage du contenu du panier -->
            <div v-if="showShop" class="mt-5 panier_modal">
                <div v-for="product in cart" :key="product.id">
                    <div style="display:flex;justify-content:space-between;margin-top:5px;">
                        <h5 class="text-info"
                        style="font-family: 'Koulen', cursive;letter-spacing: 3px;"
                        >
                        {{ product.name }}</h5>
                        <p
                        style="font-family: 'Koulen', cursive;letter-spacing: 3px;"
                        >{{ product.price }} €</p>
                    </div>
                    
                    <div class="cart-icons">
                        <button class="btn btn-light" style="color:black;">
                        <span style="text-transform:lowercase;">x</span>
                        {{ product.quantity }}</button>
                        <button
                        style="margin-left:15px;margin-right:20px;"
                        class="btn btn-info" v-on:click="cartRemoveItem(id)">
                            <em class="far fa-trash-alt"></em>
                        </button>
                    </div>
                    <br>

                    <div class="cart-icons">
                        <button class="btn btn-light" v-on:click="cartPlusOne(product)"><em class="fas fa-plus"></em></button>
                        <button class="btn btn-light" v-on:click="cartMinusOne(product, id)"
                        style="margin-left:20px;margin-right:20px;"><em class="fas fa-minus"></em></button>
                    </div>
                    <br>
                </div>
                <h5 class="card-footer"
                style="float:right;color: #42b983;"
                >
                    {{ cartTotalAmount }}€
                </h5>
            </div>
        <!-- fin affichage du contenu du panier -->
        </div>

        <div class="container__search">
            <input v-model="searchkey" class="btn btn__search" type="search" placeholder="Recherche par mot ..." autocomplete="off">
        </div>

        <a class="titre_categorie">Recherche par categorie <em class="fas fa-caret-down"></em></a>

        <div class="container__categories">
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'prepa' }" v-on:click="setFilter('prepa')">
                <em class="fas fa-caret-right"></em>
                Prepa
            </a>
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'perte' }" v-on:click="setFilter('perte')">
                <em class="fas fa-caret-right"></em>
                Perte de poids
            </a>
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'prise' }" v-on:click="setFilter('prise')">
                <em class="fas fa-caret-right"></em>
                Prise de masse
            </a>
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'boxe' }" v-on:click="setFilter('boxe')">
                <em class="fas fa-caret-right"></em>
                Boxe
            </a>
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'femme' }" v-on:click="setFilter('femme')">
                <em class="fas fa-caret-right"></em>
                Femme
            </a>
            <a class="btn btn__categorie" v-bind:class="{ active: currentFilter === 'homme' }" v-on:click="setFilter('homme')">
                <em class="fas fa-caret-right"></em>
                Homme
            </a>
            <br><br>
            <a class="btn" v-bind:class="{ active: currentFilter === 'ALL' }" v-on:click="setFilter('ALL')"
            style="color:#262626;">
                <em class="fas fa-times fa-2x"></em>
            </a>
        </div>

    </div>

    <!---------------------------------------------------->

    <div class="container__right">

        <div  v-if="searchkeyList.length < 1">
            <h1 id="result_null">Aucun resultat !</h1>
        </div>

        <div class="row row-cols-1 row-cols-md-3 g-4">
            <!--- en référence à notre méthode, on change products en searchkeyList-->
            <!--- ainsi si searchkeyList = vide, tous les éléments sont affichés -->
            <!--si searchkeyList a une valeur précise, entrée dans le input, alors -->
            <!--l'affichage se fait selon cette valeur -->
            <div class="col" v-for="product in searchkeyList" :key="product.id">
                <div class="card card__product" v-if="currentFilter === product.category || currentFilter === 'ALL'">

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

                    <div style="display:flex;justify-content:center;">
                        <button class="btn btn-light btn_shop" v-on:click="addToCart(product)"
                        style="margin-top:-23px;position:absolute;z-index:1;border:solid 2px #42b983;box-shadow:none;background-color:white;">
                            <em class="fas fa-shopping-cart btn-rounded"></em>
                        </button>
                    </div>

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
            searchkey: '',
            currentFilter: 'ALL',
            showShop: false,
            cart: [],
            products: [
                {
                    id:1,
                    category: 'prepa',
                    name: 'Preparation physique',
                    url: 'https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTE1fHxzcG9ydHxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60',
                    price: 5
                },
                {
                    id:2,
                    category: 'boxe',
                    name: 'Boxe anglaise',
                    url: 'https://images.unsplash.com/photo-1579758629938-03607ccdbaba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NTd8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 23
                },
                {
                    id:3,
                    category: 'homme',
                    name: 'Programme G - Homme',
                    url: 'https://images.unsplash.com/photo-1517838277536-f5f99be501cd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
                    price: 51
                },
                {
                    id:4,
                    category: 'femme',
                    name: 'Programme G - Femme',
                    url: 'https://images.unsplash.com/photo-1574680096145-d05b474e2155?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OTV8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 13
                },
                {
                    id:5,
                    category: 'prise',
                    name: 'Prise de masse',
                    url: 'https://images.unsplash.com/photo-1546483875-ad9014c88eba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzZ8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 52
                },
                {
                    id:6,
                    category: 'perte',
                    name: 'Perte de poids',
                    url: 'https://images.unsplash.com/photo-1616279967983-ec413476e824?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NzV8fHNwb3J0fGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60',
                    price: 9
                }
            ]
        }
    }
    ,
    computed: {
        searchkeyList() {
            // La méthode filter() sur tableau crée un nouveau tableau
            // avec des éléments qui répondent à un critère donné
            // le critère donné étant donné dans le return 
            return this.products.filter((product) => {
                // return du critère sur lequel se base le nouveau tableau
                // toLowerCase() transforme une chaine en minuscule

                // La méthode includes() permet de déterminer si un tableau
                // contient une valeur et renvoie true si c'est le cas.
                return product.name.toLowerCase().includes(this.searchkey.toLowerCase());

                // -> on veut créer un nouveau tableau qui ne stocke que des éléments répondant à un critère
                // c'est la fonction filtrer() qui permet cela
                // on passe la filtre sur product
                // puis on détermine le critère de filtre dans le return
                // ici on va chercher si product.name.toLowerCase(), soit le nom de nos produits en minuscule,
                // a une correspondant avec le mot clé 'searchkey' en minuscule entré, dans le tableau
            })
        },
        cartTotalAmount() {
            let total = 0;
            for (let item in this.cart) {
                total = total + (this.cart[item].quantity * this.cart[item].price);
            }
            return total;
        },
        itemTotalAmount() {
            let itemTotal = 0;
            for (let item in this.cart) {
                itemTotal = itemTotal + (this.cart[item].quantity);
            }
            return itemTotal;
        }
    },
    methods: {
        setFilter: function(filter) {
			this.currentFilter = filter;
		},
        addToCart(product) {
            for (let i=0; i< this.cart.length; i++) {
                if (this.cart[i].id === product.id) {
                    return this.cart[i].quantity++;
                }
            }
            this.cart.push({
                id: product.id,
                name: product.name,
                url: product.url,
                price: product.price,
                quantity: 1
            })
        },
        cartPlusOne(product) {
            product.quantity = product.quantity + 1;
        },
        cartMinusOne(product, id) {
            if (product.quantity == 1) {
                this.cartRemoveItem(id);
            }
            product.quantity = product.quantity - 1;
        },
        cartRemoveItem(id) {
            this.cart.splice(id, 1);
        }
    },
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
    position:relative;
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
/****/
#result_null{
    text-align:center;
    font-family: 'Koulen', cursive;
    letter-spacing:2px;
    font-size: 40px;
    margin:10%;
    padding:20px;
    color:white;
    background-color: #262626;
}
#panier_div{
    display:flex;
    justify-content:center;
}
.panier_modal{
    width: 250px;
    background-color:#262626;
    position:absolute;
    margin-top:10px !important;
    color:#fbfbfb;
    padding: 15px;
    padding-bottom:0px;
    border-radius:7px;
    border: solid 3px #262626;
}
.cart-icons{
    margin-left:0%;
}
</style>