<script>
  import { Router, Link, Route } from "svelte-routing";
  export let url = "";

  //import partials
  import Footer from "./components/partials/footer.svelte";
  import Header from "./components/partials/header.svelte";
  //import Pages
  import LandingPage from "./routes/landingPage/+page.svelte";
  import Login from "./routes/login/+page.svelte";
  import Register from "./routes/register/+page.svelte";
  import HeatMap from "./routes/heatMap/+page.svelte";
  import RentalData from "./routes/rentalData/+page.svelte";

  //nav link objects to pass to the header
  let loginLinks = [{ href: "/", linkText: "Go Back" }];
  let heatMapLinks = [
    { href: "/rentalData", linkText: "View Rental Data" },
    { href: "/", linkText: "Log Out" },
  ];
  let rentalDataLinks = [
    { href: "/register", linkText: "Register User Account" },
    { href: "/heatMap", linkText: "View Heat Map" },
    { href: "/", linkText: "Log Out" },
  ];
  let landingPageLinks = [{ href: "/login", linkText: "Log In" }];
  let registerLinks = [{ href: "/rentalData", linkText: "Go Back to Rental Data page"}];

  let liveServerURL = "https://mesn-backend.onrender.com";
  let localServerURL = "http://localhost:5001";

  //change which is commented dependant on where youre working
  let currentURL = liveServerURL;
  //let currentURL = localServerURL;



</script>

<Router {url}>
  <Route path="/">
    <Header navList={landingPageLinks} />
    <LandingPage />
  </Route>
  <Route path="login">
    <Header title={"login"} navList={loginLinks} />
    <Login bind:currentURL />
  </Route>
  <Route path="register">
    <Header title={"register"} navList={registerLinks} />
    <Register bind:currentURL/>
  </Route>
  <Route path="heatMap">
    <Header title={"heatMap"} navList={heatMapLinks} />
    <HeatMap bind:currentURL />
  </Route>
  <Route path="rentalData">
    <Header title={"rentalData"} navList={rentalDataLinks} />
    <RentalData  bind:currentURL/>
  </Route>
  
  <Footer />
</Router>

<style>

</style>
