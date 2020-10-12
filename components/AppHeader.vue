<template>
    <div fluid>
        <b-navbar type='dark' class='header_style'>
            <b-navbar-brand>
                <a href='/' class='brand-text'>
                    <p id='brand-desc1'>Zigzag/Gengo</p>
                    <p id='brand-desc2'>| Senior Software Engineer Technical Test</p>
                </a>
            </b-navbar-brand>
        </b-navbar>
    </div>
</template>

<script>
    export default {}
</script>

<style>
.header_style {
    background-color: #252525;
    height: auto;
    padding-left: 2vw;
    padding-right: 2vw;
    top: 0;
    position: absolute;
    color: #fff;

    margin: 0;
    left: 0;
    right: 0;
    top: 0;

    font-family: 'GothamBook', sans-serif;
    z-index: 1;
}

.brand-text:hover {
    color: white;
    text-decoration: none;
}

#brand-desc1 {
    display: inline;
    color: gold;
}

#brand-desc2 {
    display: inline;
    color: white;
}
</style>