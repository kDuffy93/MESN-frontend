<script>

  export let inputIdUser;
  export let labelClassUser;
  export let labelTextUser;
  export let InputTypeUser;
  export let inputIdPwd;
  export let labelClassPwd;
  export let labelTextPwd;
  export let InputTypePwd;
  export let linkNameLog;
  export let linksTextLog;
  export let linkNamePwd;
  export let linksTextPwd;
  export let loginText;
  export let pwdClass;
  export let loginClass;

</script>

<!-- html -->
<main>
  <section class="container">
    <form>

      <h1>{loginText}</h1>
      <label for={inputIdUser} class={labelClassUser}>{labelTextUser}</label>
      <input type={InputTypeUser} id={inputIdUser} />
      <label for={inputIdPwd} class={labelClassPwd}>{labelTextPwd}</label>
      <input type={InputTypePwd} id={inputIdPwd} />
      <a href={linkNameLog} class={loginClass}>{linksTextLog}<span /></a><br />
      <a href={linkNamePwd} class={pwdClass}>{linksTextPwd}<span /></a>

    </form>
  </section>
</main>

<!-- style -->
<style>

form{
  transform: scale(1.5);
}


  /* container */
  main {
    background: #362100 url("https://i.esdrop.com/d/f/00nJAaeIIr/ARxxEA1V2j.png");
    width: 100vw;
    height: 85vh;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    z-index: -1;
    position: absolute;
    transition: 0.3s;
    /* opacity: 0.5; */
  }
  /* .container {
  align-items: center;
  display: flex;
  justify-content: center;
  background: #362100 url('https://picsum.photos/id/413/1920/1080') center/cover;
  height: 70vh;
  position: relative;
} */
  .container {
    align-items: center;
    display: flex;
    justify-content: center;
    height: 70vh;
    position: relative;
  }
  form {
    backdrop-filter: blur(10px);
    /* background: rgba(254, 254, 254, 0.075); */
    background: rgba(254, 254, 254, 0.45);
    border: 1px solid rgba(254, 254, 254, 0.18);
    border-radius: 15px;
    box-shadow: 0 10px 35px 0 rgb(64, 81, 59);
    /* color: #F5F5F5; */
    max-width: 300px;
    max-height: 400px;
    overflow: hidden;
    padding: 20px 30px 50px 30px;
    position: relative;
    text-align: center;
    z-index: 1;
  }
  h1 {
    font-size: 23px;
    font-weight: 200;
    margin-bottom: 15px;
  }

  input {
    background: rgba(254, 254, 254, 0.075);
    border: 1px solid rgba(254, 254, 254, 0.3);
    border-radius: 20px;
    box-sizing: border-box;
    color: black;
    display: block;
    font-size: 1rem;
    letter-spacing: 0.15rem;
    padding: 10px;
    width: 100%;
  }
  input:focus,
  input:active {
    background: rgba(254, 254, 254, 0.08);
    border: 1px solid rgba(254, 254, 254, 0.75);
    outline: none;
  }

  /* login button */
  .loginClass {
    display: inline-block;
    background: #00539b;
    color: #f5f5f5;
    border: none;
    text-decoration: none;
    border-radius: 25px;
    margin: 10px auto 10px auto;
    padding: 8px 20px;
  }
  .loginClass:hover {
    background: #64a70b;
    /* color: black; */
    outline: none;
  }
  /* password link */
  .pwdClass {
    --color: #00539b;
    position: relative;
    text-decoration: none;
    color: var(--color);
    padding: 0.2rem 0;
    text-align: center;
  }
  .pwdClass::before {
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
  .pwdClass:hover::before {
    transform-origin: left;
    transform: scaleX(1);
  }
  .pwdClass:hover span {
    --deg: -45deg;
  }
  .pwdClass:hover span::before {
    transform: rotate(var(--deg));
  }
  .pwdClass:hover span::after {
    transform: translateX(-1px) rotate(var(--deg));
  }
  .pwdClass span {
    --line-arrow-width: 1px;
    --line-arrow-height: 6px;
    --line-arrow-easing: cubic-bezier(0.3, 1.5, 0.5, 1);
    --line-arrow-transition-duration: 200ms;
    --line-arrow-transition-delay: 240ms;
  }
  .pwdClass span::before,
  .pwdClass span::after {
    content: "";
    position: absolute;
    right: -18%;
    bottom: 0px;
    background: var(--color);
    transition: transform var(--line-arrow-transition-duration) var(--line-arrow-easing);
    transition-delay: var(--line-arrow-transition-delay);
    z-index: 2;
  }
  .pwdClass span::before {
    width: var(--line-arrow-width);
    height: var(--line-arrow-height);
    transform-origin: 0% 100%;
    transform: rotate(-90deg);
  }
  .pwdClass span::after {
    height: var(--line-arrow-width);
    width: var(--line-arrow-height);
    transform-origin: 100% 0%;
    transform: translateX(-1px) rotate(0deg);
  }
</style>
