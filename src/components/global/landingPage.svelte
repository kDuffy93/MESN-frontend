<script>
// import Partialslinks from "./partialslinks.svelte";
export let landingMainClass;
export let WelcomeText;
export let LabText;
export let toolText;
export let landingH3Text;
export let h3Text;
export let h3TextTwo;
export let h3TextThree;
export let landingA;
export let landingLinkText;
export let textContent;
export let imageContent;
export let linkDiv;
export let landingImage;
</script>

<!-- html -->

<main class={landingMainClass}>
  <section>
    <div class={textContent}>
      <h1>{WelcomeText}<br>{LabText}<br><p>{toolText}</p></h1>
      <h3>{landingH3Text}<br>{h3Text}<br>{h3TextTwo}<br>{h3TextThree}</h3>
      <div class={linkDiv}>
        <a href={landingA} >{landingLinkText}<span></span></a>
      </div>
    </div>
    <div class={imageContent}><img src={landingImage} /></div>
  </section>
</main>



<style>
:global(body){
  background: url('https://i.esdrop.com/d/f/00nJAaeIIr/ARxxEA1V2j.png');
}
section {
  display: grid;
  grid-template-rows: repeat(1, 1fr);
  grid-template-columns: 770px 891px;
  height: inherit;
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
    color: #efefef;
    background-color: #819796;
}
.imageContent {
  background: url('https://i.esdrop.com/d/f/00nJAaeIIr/ARxxEA1V2j.png');
  background-repeat : no-repeat;
  background-size: cover;
  align-items:center; 
  display: flex; 
  justify-content:center;
}
.textContent{
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-template-rows: repeat(3, 1fr);
  height: inherit;
}

/* Here link */
.linkDiv {
  padding-left: 380px;
  padding-bottom: 210px;
}
a{
    --color: #00539B;
  position: relative;
  text-decoration: none;
  color: var(--color);
  font-family: "Inter", sans-serif;
  font-size: 20px;
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

/* text */
h1{
  font-size: 40px;
  padding-top: 140px;
  text-align: center;
  padding-left: 10px;
}

h2{
  font-size: medium;
  text-align: right;
}

h3{
  text-align:center;
  font-size: 23px;
  padding-left: 40px;
}
/* logo image center */
.imageContent > img{
  width: 400px;
  opacity: 0.5;
}

</style>