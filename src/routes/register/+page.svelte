<script>
  import Register from "../../components/global/register.svelte";
  export let currentURL = localServerURL;


  $: userData = {
    username: "",
    password: "",
  };

  let registerUser = async () => {
    console.log("registering user...");
    const response = await fetch(`${currentURL}/register`, {
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

  async function comparePasswords() {
    let pw1 = document.getElementById("password").value;
    let pw2 = document.getElementById("confirm").value;
    let pwMsg = document.getElementById("pwMsg");

    if (pw1 != pw2) {
      pwMsg.innerText = "Passwords do not match";
    } else {
      let response = await registerUser();
      console.log(response.message);
      if (response._id != undefined) {
        // redirect user to login page
        pwMsg.innerText = "You have been registered, Redirecting back to Rental Data page";
        setTimeout(() => {
          history.back();
        }, "5000");
      } else {
        pwMsg.innerText = `${response.message}`;
        pwMsg.className = "registerError";
      }
    }
  }
</script>

<Register on:click={comparePasswords} bind:userNameValue={userData.username} bind:passwordValue={userData.password} registerUserId={"username"} labelClassUser={"userName"} registerLabelUserId={"Username: "} registertTypeUserId={"text"} registerPwd={"password"} labelClassPwd={"password"} registerLabelPwd={"Password: "} registerTypePwd={"text"} registerConfirmPwd={"confirm"} registerLabelComfirmPwd={"Confirm Password:"} registerTypeConfirmPwd={"text"} registerFunction={"Register"} registerHeading={"Register User Account"} registerTextButton={"Register Account"} registerClass={"registerClass"} pwdClass={"pwdClass"} registerMsg={"pwMsg"} />

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
