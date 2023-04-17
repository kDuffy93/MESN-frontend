<script>
</script>

<footer>

  <div>
    <div>
      <img src="./images/CountyOfSimcoeLogo.png" />
    </div>
    <div>
    <aside>
      &copy; Georgian College Web Project Studio 2023
      <br />
      Team Marshmallow
    </aside>
    </div>
    <div>
      <img src="./images/CCIS_Logo_Vertical.webp" />
    </div>
  </div>
  
</footer>

<style>
  footer {
    background-color: #f0f0f0;
    /* display: flex; */
    align-items: center;
    position:fixed;
    bottom: 0vh;
    right: 0;
    width: 100%;
    height: clamp(75px, 7.5vh, 100px);  }

  footer > div > aside, footer > div > div {
    text-align: center;
    height:100%;
    display: flex;
    align-items:center;
    justify-content: center;
  }
  footer > div > div{
  }

  footer > div {
     height: 100%;
     
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-areas: 
    "partner1 title partner2";

  }

  footer > div > div:nth-child(2) {
    grid-area: title;
    text-align: center;
    font-size: 8pt;
    margin: 0;
  }

  footer > div > div:first-of-type {
    grid-area: partner1;
    height: inherit;
    text-align: center;
  }

  footer > div > div:last-of-type {
    grid-area: partner2;
    height: inherit;
    text-align: center;
  }

  footer > div > div:last-of-type > img,
  footer > div > div:first-of-type > img {
    width: auto;
     height: clamp(60px, 7.50vh, 90px); 
  }
</style>
