<template>

        <ul>
            <li @click="setCrypto('BTC')" :className="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
            <li @click="setCrypto('ETH')" :className="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
            <li @click="setCrypto('USDT')" :className="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
        </ul>

 

</template>

<script>


export default {
   props: {
    setCrypto: {
    type: Function,
    required: true,
   },
   cryptoNow:{
    type: String,
    required: true
   }},
 
}
</script>

<style scoped>

ul{
    list-style: none;
    width: 300px;
    border: 3px solid #000;
    border-radius: 5px;
    padding: 0;
    align-content: center;
}
li{
    display: block;
    color: #fff;
    background:  rgba(102, 47, 47, 0.56);
}
li:hover, .active {
    cursor: pointer;
    background:#000;
}
</style>