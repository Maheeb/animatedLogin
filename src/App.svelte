<script>
	let name = '';
  let strength=0;
  let validations =[];
  let showPassword= false;
  let toggleView=''
  // const passwordField = document.querySelector('#password')
 
function showHidePwd() {
    let input = document.getElementById("password");
    if (input.type === "password") {
        input.type = "text";
        document.getElementById("toggle").innerHTML = "🙈";
    } else {
        input.type = "password";
        document.getElementById("toggle").innerHTML = "👁️";
    }
}

  function validatePassword(e) {
    const password = e.target.value;

    strength =
      +(password.length > 5) +
      +(password.search(/[A-Z]/) > -1) +
      +(password.search(/[0-9]/) > -1) +
      +(password.search(/[$&+,:;=?@#]/) > -1);
  }

</script>


<style> 
 main {
    display: flex;
    align-items: center;
	flex-direction: column;
	font-family: sofia-pro, sans-serif;
	
  }

  h1 {
    font-family: gothic-open-shaded, sans-serif;
    font-weight: 400;
    font-style: normal;
  } 
 .field {
    width: 100%;
    margin: 0 auto;
    position: relative;
    border-bottom: 2px dashed #afafaf;
    margin: 4rem auto 1rem;
    transition: 500ms;
  }

  .label {
    color: #afafaf;
    font-size: 1.2rem;
  }

  .input {
    outline: none;
    border: none;
    overflow: hidden;
    margin: 0;
    width: 100%;
    padding: 0.25rem 0;
    background: none;
    color: white;
    font-size: 1.2em;
    font-weight: bold;
    transition: border 500ms;
  }

  .input:valid {
    color: yellowgreen;
  }

  .input:invalid {
    color: orangered;
  }

  /* Border animation */

  .field::after {
    content: "";
    position: relative;
    display: block;
    height: 4px;
    width: 100%;
    background: #d16dff;
    transform: scaleX(0);
    transform-origin: 0%;
    opacity: 0;
    transition: all 500ms ease;
    top: 2px;
  }

  .field:focus-within {
    border-color: transparent;
  }

  .field:focus-within::after {
    transform: scaleX(1);
    opacity: 1;
  }

  /* Label animation */

  .label {
    z-index: -1;
    position: absolute;
    transform: translateY(-2rem);
    transform-origin: 0%;
    transition: transform 400ms;
  }

  .field:focus-within .label,
  .input:not(:placeholder-shown) + .label {
    transform: scale(0.8) translateY(-5rem);
    opacity: 1;
  }

  /* Strength Meter */

  .strength {
    display: flex;
    height: 20px;
	width: 100%;
  }
 .bar {
    margin-right: 5px;
    height: 100%;
    width: 25%;
    transition: box-shadow 500ms;
    box-shadow: inset 0px 20px #1f1f1f;
  }

  .bar-show {
    box-shadow: none;
  }

  .bar-1 {
    background: linear-gradient(to right, red, orangered);
  }

  .bar-2 {
    background: linear-gradient(to right, orangered, yellow);
  }

  .bar-3 {
    background: linear-gradient(to right, yellow, yellowgreen);
  }

  .bar-4 {
    background: linear-gradient(to right, yellowgreen, green);
  }

 .bar:last-child {
    margin-right: 0;
  }

  .strength-text {
    margin-top: 20px;
  }

 /* Buttons */

  button {
    margin-top: 2rem;
    padding: 10px 30px;
    font-weight: bold;
    border: 2px solid greenyellow;
    color: greenyellow;
    border-radius: 100px;
    background: transparent;
    transition: all 1000ms;
  }

  button:disabled {
    border-color: #b6b6b6;
    color: #b6b6b6;
  }

  .toggle-password {
    position: absolute;
    cursor: help;
    font-size: 0.8rem;
    right: 0.25rem;
    bottom: 0.5rem;
  }
  

</style> 

<main>  
<h1>Sign Up</h1>

	<form action=""> 
		 <div class="field">
      <input type="email" name="email" class="input" placeholder=" "/>
      <label for="email" class="label">Email</label>
    </div>

 <div class="field">
      <input type="password" id="password" class="input" placeholder=" "  on:input={validatePassword} class:valid={strength > 3}  bind:value={name}/>
      <label for="password" class="label">Password</label>

      <span
        class="toggle-password"
        id="toggle"
       
       on:click={showHidePwd}
      >👁️
      </span>
    </div>


	<div class="strength">
      <span class="bar bar-1" class:bar-show={strength > 0} />
      <span class="bar bar-2" class:bar-show={strength > 1} />
      <span class="bar bar-3" class:bar-show={strength > 2} />
      <span class="bar bar-4" class:bar-show={strength > 3} />
    </div>




<ul id="listStyle">
	<li>{  (name.length > 5)  ? '✅': '❌' }   must be at least 5 characters</li>
	<li>{(name.search(/[A-Z]/) > -1) ? '✅': '❌'}   must contain a capital letter</li>
	<li>{(name.search(/[0-9]/) > -1) ? '✅': '❌'}   must contain a number</li>
	<li>{(name.search(/[$&+,:;=?@#]/) > -1) ? '✅': '❌'}   must contain one of $&+,:;=?@#</li>
</ul>

<button disabled={strength < 4}>Sign Up</button>

	</form>

</main>