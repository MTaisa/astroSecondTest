<!-- Modal.svelte -->
<script>
  import { fade } from "svelte/transition";
  import {ratingCalculator} from "../assets/utils/ratingCalculator"
    export let name;
    export let description;
    export let onClose;
    export let categories;
    export let streamingServices;
    export let lenguage;
    export let status;
    export let rating;

    let numbersOfStars = ratingCalculator(rating);
    let numberOfReviews = rating.length


</script>

<div class="overlay" on:click={onClose}  transition:fade={{ delay: 150, duration: 200 }}></div>
<div class="modal fade" transition:fade={{ delay: 150, duration: 200 }}>
    <div class="modal-content">
        <span class="close" on:click={onClose}>&times;</span>
        
        <div class="header">
            <h2>{name}</h2>
        
            <div class="star">
                {numbersOfStars} ★ {`( ${numberOfReviews} )`}
            </div>
        </div>
        
        <div class="categories">
            {#each categories as category}
                <p class="category">{category}</p>
            {/each}
        </div>

        <p>{description}</p>

        <div class="streaming-services">
            {#each Object.keys(streamingServices) as service}
                <img src={streamingServices[service]} alt={service}>
            {/each}
        </div>

        <div class="categories">
            <p class="category">{lenguage}</p>
            <p class="category">{status}</p>
        </div>

        
    </div>
</div>

<style>
    .modal {
        display: block;
        position: fixed;
        z-index: 10; /* Ajustado para estar sobre la overlay */
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal-content {
        background-color: rgb(23 23 23);
        color: #fff;
        box-shadow: 0px 0px 30px #e74d3c48;
        z-index: 11; /* Más alto que el modal */
        padding: 20px;
        border: 0.5px solid #e74c3c;
        width: 80%;
        width: 500px;
        height: 500px;
        border-radius: 10px;
        position: relative;
    }

    .close {
        color: #aaa;
        font-size: 28px;
        font-weight: bold;
        position: absolute;
        top: 10px;
        right: 10px;
        cursor: pointer;
    }

    .close:hover,
    .close:focus {
        color: #e74c3c;
        text-decoration: none;
    }

    .overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.4);
        z-index: 9; /* Más bajo que el modal */
    }

    .categories{
        display: flex;
        gap: 10px
    }

    .streaming-services {
        display: flex;
        gap: 10px;
        margin-top: 20px;
        margin-bottom: 20px;
    }

    .streaming-services img {
        width: 50px; /* Ajusta el tamaño según sea necesario */
        height: 50px; /* Ajusta el tamaño según sea necesario */
        margin-right: 10px; /* Espaciado entre las imágenes */
        border-radius: 50%;
        object-fit:cover
    }

    h2{
        font-weight: 600;
    }

    .category{
        margin-top: 0;
        background-color: #ffffff4e;
        padding: 5px 10px;
        border-radius: 5px;
    }

    .star{
        color: gold;
    }

    .header{
        display: flex;
        align-items: center;
        gap: 25px;
    }
</style>
