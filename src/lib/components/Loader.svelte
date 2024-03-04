
<div class='container'>
  <img alt='logo' src='images/logo.svg' />
  <div class="loader"></div>

</div>

<style>
  .container{
    display: flex;
      flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  img{
    width: 150px;
    height: 150px;
  }
  .loader {
    width: 60%;
    height: 4.8px;
    display: inline-block;
    position: relative;
    background: rgba(255, 255, 255, 0.15);
    overflow: hidden;
  }
  .loader::after {
    content: '';
    box-sizing: border-box;
    width: 0;
    height: 4.8px;
    background: #1577F5;
    position: absolute;
    top: 0;
    left: 0;
    animation: animFw 10s linear infinite;
  }

  @keyframes animFw {
    0% {
      width: 0;
    }
    100% {
      width: 100%;
    }
  }

</style>