<script>

// import Partialslinks from "../../components/global/partialslinks.svelte";
import LandingPage from "../../components/global/landingPage.svelte";
</script>

<!-- <main class="container">
    <h1><span>Welcome to</span><br>the Affordable Housing Community Lab's<br><p>Online Tool.</p></h1>
    <h3>If you're a community member looking for renal listings information you can view the public reports <PartialsLinks linkName={'#'} linksText={'here'}/>
        <a href="#" >here</a>
        .</h3>
</main> -->

<LandingPage landingMainClass={'container'} landingSpanText={'Welcome to'} landingBrText={"the Affordable Housing Community Lab's"} landingPText={'Online Tool.'} landingH3Text={"If you're a community member looking for renal listings information you can view the public reports "} landingA={'#'} landingLinkText={'here'}/>

<style>
h1{
    font-size:large;
    width:33vw;
}
h1>span:first-of-type{
    font-size: xx-large;
    margin-left:-2.5vw;
}
h1>p{
    text-align: right;
    padding-right:5vw;
}

h2{
    font-size: medium;
    text-align: right;
}

h3{
text-align:center;
    font-size: large;
    margin-top:25vh;
}
</style>

