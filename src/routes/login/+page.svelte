<script>
  // import LoginInfo from "../../components/global/loginInfo.svelte";
  // import LoginButton from "../../components/global/loginButton.svelte";
  // import PartialsLinks from "../../components/global/partialsLinks.svelte";
  import Login from "../../components/global/login.svelte";

  //page level varibles
  let liveServerURL = "https://mesn-backend.onrender.com";
  let localServerURL = "http://localhost:5001";

  //change which is commented dependant on where youre working
  //let currentURL = liveServerURL;
  let currentURL = localServerURL;

  $: userData = {
    username: "",
    password: "",
  };

  let handleLogin = async () => {
    console.log("trying to login user...");
    const response = await fetch(`${currentURL}/login`, {
      method: "post",
      mode: "cors",
      body: JSON.stringify(userData),
      headers: {
        "Content-Type": "application/json",
        // 'Content-Type': 'application/x-www-form-urlencoded',
      },
    });
    return response.json();
  };

    


  let logUserIn = async () => {
    let response = await handleLogin();

    if (response._id != undefined) {
      // redirect user to login page
      window.location.href = window.location.href.replace("login", "rentalData");
    } else {
      loginMsg = `${response.message}`;
    }


  }



  let loginMsg = "";
</script>

<Login on:click={logUserIn} bind:loginMsg bind:userNameValue={userData.username} bind:passwordValue={userData.password} inputIdUser={"username"} labelClassUser={"userName"} labelTextUser={"Username: "} InputTypeUser={"text"} inputIdPwd={"password"} labelClassPwd={"password"} labelTextPwd={"Password: "} InputTypePwd={"text"} linkNameLog={"rentalData"} linksTextLog={"Login"} linkRegister={"register"} registerText={"Register"} linkNamePwd={"forgotPassword"} linksTextPwd={"Forgot Password."} loginText={"Login Information"} loginClass={"loginClass"} registerClass={"registerClass"} pwdClass={"pwdClass"} />

<style>
  main > section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 76vh;
  }
  main > section > a {
    width: 25%;
    text-align: right;
  }
  form {
    padding: 2.5%;
    border-radius: 20px;
    background-color: grey;
    width: 30%;
    height: 30%;
    min-height: 120px;
    display: grid;
    grid-template-columns: 40% 60%;
    grid-template-areas:
      "unLabel unInput"
      "pwLabel pwInput"
      ". submit";
  }

  form > label:first-of-type {
    grid-area: unLabel;
    margin: 0;
    text-align: center;
    padding-top: 5%;
  }

  form > input:first-of-type {
    grid-area: unInput;
    border-radius: 10px;
    height: 100%;
  }

  form > label:last-of-type {
    grid-area: pwLabel;
    margin: 0;
    text-align: center;
    padding-top: 5%;
  }

  form > input:nth-of-type(2) {
    grid-area: pwInput;
    border-radius: 10px;
    height: 100%;
  }
  form > a {
    margin-top: 5%;
    grid-area: submit;
    margin-left: 25%;
    width: 50%;
    text-align: center;
    background-color: #f3f3f3;
    border-radius: 25px;
  }
</style>
