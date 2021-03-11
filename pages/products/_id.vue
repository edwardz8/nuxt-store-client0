<template>
<b-container>
    <div>Product ID Page 
       <!--  <b-card>
            <p>{{product.category.type}}</p>
            <p>{{product.title}}</p>
            <div>
                <img :src="product.photo" />
            </div>
        </b-card>

         <b-card>
            <div>
                <p>{{ product.owner.name }}</p>
                <p>{{ product.owner.about }}</p>
                <img :src="product.owner.photo" />
            </div>
        </b-card> -->
    </div>
</b-container>
</template>

<script>
export default {
    async asyncData({ $axios, params }) {
        try {
            let singleProduct = $axios.$get(`/api/products/${params.id}`)
            let allReviews = $axios.$get(`/api/reviews/${params.id}`)

            const [ productResponse, reviewsResponse ] = await Promise.all([
                singleProduct, allReviews
            ])

            return {
                product: productResponse.product,
                reviews: reviewsResponse.reviews
            }
        } catch (err) {
            console.log(err)
        }
    }
}
</script>