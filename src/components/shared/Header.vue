<template>
    <div>
       <nav class="navbar navbar-expand-lg navbar-dark" style="background-color: #563F7A">
            <router-link 
            to="/"
            tag="a"
            class="navbar-brand">List of products</router-link>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mr-auto">
                    <router-link
                    active-class="active"
                    to="/urun-islemleri"
                    tag="li"
                    class="nav-item" ><a class="nav-link">Product Purchase</a> 
                    </router-link>
                    <router-link 
                    active-class="active"
                    to="/urun-cikisi"
                    tag="li"
                    class="nav-item"><a class="nav-link">Product Sell</a>
                    </router-link>
                    
                </ul>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    

}
</script>


<style >
    
</style>