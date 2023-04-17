<script>
  // import LoginInfo from "../../components/global/loginInfo.svelte";
  // import LoginButton from "../../components/global/loginButton.svelte";
  // import PartialsLinks from "../../components/global/partialsLinks.svelte";
  import Login from "../../components/global/login.svelte";
</script>

<!--
<main>

<section class="container">
        <form>
            <LoginInfo inputId={'username'} labelText={'Username: '} InputType={'text'} labelClass={'userName'}/>    
             <label for="username">Username:</label>
            <input type="text" id="username" /> 
            <LoginInfo inputId={'password'} labelText={'Password:'} InputType={'text'} labelClass={'password'}/>
            <label for="password">password:</label>
            <input type="text" id="password" />
            <LoginButton linkName={'rentalData'} linksText={'Login'}/>
            <a href="rentalData">Log In</a> 
        </form>
        <PartialsLinks linkName={'forgotPassword'} linksText={'Forgot Password.'}/>
        <a href="forgotPassword">Forgot Password</a>
    </section> 
</main>  -->

<Login inputIdUser={"username"} labelClassUser={"userName"} labelTextUser={"Username: "} InputTypeUser={"text"} inputIdPwd={"password"} labelClassPwd={"password"} labelTextPwd={"Password: "} InputTypePwd={"text"} linkNameLog={"rentalData"} linksTextLog={"Login"} linkRegister={"register"} registerText={"Register"} linkNamePwd={"forgotPassword"} linksTextPwd={"Forgot Password."} loginText={"Login Information"} loginClass={"loginClass"} registerClass={"registerClass"} pwdClass={"pwdClass"} />

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
