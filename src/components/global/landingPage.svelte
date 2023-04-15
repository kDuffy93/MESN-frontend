<script>
// import Partialslinks from "./partialslinks.svelte";
export let landingMainClass;
export let landingSpanText;
export let landingBrText;
export let landingPText;
export let landingH3Text;
export let landingA;
export let landingLinkText;

</script>

<!-- html -->

<main class={landingMainClass}>
    <h1><span>{landingSpanText}</span><br>{landingBrText}<br><p>{landingPText}</p></h1>
    <h3>{landingH3Text}.
      <!-- <a href={landingA} >{landingLinkText}<span></span></a> -->
    </h3>
</main>



<style>
/* container */
:global(body){
  background: url('https://i.esdrop.com/d/f/00nJAaeIIr/ARxxEA1V2j.png');
}
main{
 
  width: 100vw;
    height: 85vh;
    background-size: cover;
    background-position: center;
    background-repeat : no-repeat;
    z-index: -1;
    position: absolute;
    transition: 0.3s;
    /* opacity: 0.5; */
    color: #F5F5F5;
}
a{
    --color: #00539B;
  position: relative;
  text-decoration: none;
  color: var(--color);
  font-family: "Inter", sans-serif;
  padding: 0.2rem 0;
}
a::before{
    --line-width: 115%;
  --line-height: 1px;
  --line-easing: ease;
  --line-transition-duration: 300ms;
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  width: var(--line-width);
  height: var(--line-height);
  transform-origin: right;
  transform: scaleX(0);
  background: var(--color);
  transition: transform var(--line-transition-duration) var(--line-easing);
  z-index: 1;
}
a:hover::before {
  transform-origin: left;
  transform: scaleX(1);
}
a:hover span {
  --deg: -45deg;
}
a:hover span::before {
  transform: rotate(var(--deg));
}
a:hover span::after {
  transform: translateX(-1px) rotate(var(--deg));
}
a span {
  --line-arrow-width: 1px;
  --line-arrow-height: 6px;
  --line-arrow-easing: cubic-bezier(0.3, 1.5, 0.5, 1);
  --line-arrow-transition-duration: 200ms;
  --line-arrow-transition-delay: 240ms;
}
a span::before, a span::after {
  content: "";
  position: absolute;
  right: -18%;
  bottom: 0px;
  background: var(--color);
  transition: transform var(--line-arrow-transition-duration) var(--line-arrow-easing);
  transition-delay: var(--line-arrow-transition-delay);
  z-index: 2;
}
a span::before {
  width: var(--line-arrow-width);
  height: var(--line-arrow-height);
  transform-origin: 0% 100%;
  transform: rotate(-90deg);
}
a span::after {
  height: var(--line-arrow-width);
  width: var(--line-arrow-height);
  transform-origin: 100% 0%;
  transform: translateX(-1px) rotate(0deg);
}

/*  */
/* h1{
    font-size:large;
    width:33vw;
}
h1>span:first-of-type{
    font-size: xx-large;
    margin-left:-2.5vw;
} */
h1>p{
    text-align: center;
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