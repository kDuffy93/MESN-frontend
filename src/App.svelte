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
    { href: "/heatMap", linkText: "View Heat Map" },
    { href: "/", linkText: "Log Out" },
  ];
  let landingPageLinks = [{ href: "/login", linkText: "Log In" }];
  let registerLinks = [{ href: "/", linkText: "Go Back"}];
</script>

<Router {url}>
  <Route path="/">
    <Header navList={landingPageLinks} />
    <LandingPage />
  </Route>
  <Route path="login">
    <Header title={"login"} navList={loginLinks} />
    <Login />
  </Route>
  <Route path="register">
    <Header title={"register"} navList={registerLinks} />
    <Register />
  </Route>
  <Route path="heatMap">
    <Header title={"heatMap"} navList={heatMapLinks} />
    <HeatMap />
  </Route>
  <Route path="rentalData">
    <Header title={"rentalData"} navList={rentalDataLinks} />
    <RentalData />
  </Route>
  <div class='bottomSpacer'></div>
  <Footer />
</Router>

<style>
.bottomSpacer{
  min-height:10vh;
}
</style>
