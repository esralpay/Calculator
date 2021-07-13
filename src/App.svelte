<script>
import { onMount } from "svelte";
let value =0;
let counter = 1;
let themeValue=1;
let storage =[0,0];
let operator= false;
let operatorWhich = "";
let firstTime = false;
let dotClicked = false;

const updateTheme = (a)=> {
	themeValue = a.target.value;	
}

const number = (x) => {
	
	if (operator) {
		value=x;
	}else if(value.toString().length==14) {
		return;
	}else{
			if (dotClicked) {
				console.log(value);
				let valueLength= value.length;
				value= Number(value) + x*(Math.pow(10, -(counter)));
				console.log(value);
				if (value < 1) {
					value = value.toPrecision(valueLength-1);
				}else{
					value = value.toPrecision(valueLength);
				}		
				counter++;
			}else{
				value = (value*10)+ x ;
			}		
		}	
		operator = false;
		firstTime = true;
	
	
}
const operation = (operand) =>{
	
	if (storage[0]==0) {
		storage[0]=value;
				
	} else if (operatorWhich!=operand) {
		console.log(operatorWhich,operand);
		console.log(firstTime);
		// 5 + 2 den sonra * basıldığında  * değil + çağırmak için
		return operation(operatorWhich);
	} else if (firstTime) {
		console.log("firsttime");
		switch(operand){
			case "add":{				
				value=Number(storage[0])+ Number(value);
				console.log(value);
				value = value.toFixed(10);
				console.log(value);
				value= value.toString().replace(/0+$/,"")	
				console.log(value);			
				break;
			}
			case "multiply":{
				value=storage[0]*value;
				console.log(value);
				value = value.toPrecision(10).replace(/0+$/,"");
				console.log(value);
				break;
			}
			case "substract":{				
			 	value=storage[0]-value;	 			
				value = value.toPrecision(storage[0].toString().length).replace(/0+$/,"");					
				break;
			}
			case "divide":{
				value=storage[0]/value;
				value = value.toPrecision(10).replace(/0+$/,"");
				break;
			}
			case "equal":{
				value=storage[0];
				break;
			}			
		}		
		storage[0]=value;
		firstTime = false;
	}
	console.log("erdem");
	operator=true; // bu ne?
	operatorWhich =operand
	dotClicked=false;
	counter=1;
}

const reset = () => {
	value =0;	
	storage[0] = 0;
	operator= false;
	operatorWhich = "";
	firstTime = false;
	dotClicked=false;
	counter=1;
}

const dot = ()=> {
	if (dotClicked) {
		return;
	}else{
		value= value+"." ;		
		dotClicked = true;
	}	
}	
const del = () => {	
	if (value.toString().length == 1) {
		value = 0;
	}else if (dotClicked) {
		value = value.toString().substring(0, value.toString().length - 1); 
		counter--;
	}else{
		value = value.toString().substring(0, value.toString().length - 1); 
	}	
}

/* kendime bilgi olarak kalsın istedim onMount önce yüklenmesini istediğimiz kodlar için kullanılır.
	onMount(()=> {
		let slider = document.getElementById("myRange");
		slider.addEventListener("change", (a) => {
			themeValue = a.target.value;
		})
	}); */
	

</script>

<main>
	<div class={ `main main${themeValue}`}>
		<div class="header">
			<div class={ `title title${themeValue}`}>calc</div>
			<div class="theme">
				<div class={ `theme-text theme-text${themeValue}`}>THEME</div>
				<div class="theme-change">
					<div class={ `value-text value-text${themeValue}`}>
						<div>1</div>
						<div>2</div>
						<div>3</div>
					</div>					
					<div class="slidecontainer">
						<input type="range" on:change={updateTheme} min="1" max="3" value="1" class={`slider slider${themeValue}`} id="myRange">						
					</div>
				</div>
			</div>
		</div>
		<div class={ `display display${themeValue}`}>
			<div data-display class={ `display-box display-box${themeValue}`}>				
				{value}
			</div>
		</div>
		<div class={ `inputs style inputs${themeValue} style${themeValue}`}>
			<div class="grid-container">
				<button on:click={()=>number(7)} class={`standart-button standart-button${themeValue}`}>7</button>
				<button on:click={()=>number(8)} class={`standart-button standart-button${themeValue}`} id="sayı">8</button>
				<button on:click={()=>number(9)} class={`standart-button standart-button${themeValue}`} id="sayı">9</button>
				<button on:click={()=>del()} class={`del del${themeValue}`}>DEL</button>
				<button on:click={()=>number(4)} class={`standart-button standart-button${themeValue}`} id="sayı">4</button>
				<button on:click={()=>number(5)} class={`standart-button standart-button${themeValue}`} id="sayı">5</button>
				<button on:click={()=>number(6)} class={`standart-button standart-button${themeValue}`} id="sayı">6</button>
				<button on:click={()=>operation("add")} class={`standart-button standart-button${themeValue}`} id="buttonAdd">+</button>
				<button on:click={()=>number(1)} class={`standart-button standart-button${themeValue}`} id="sayı">1</button>
				<button on:click={()=>number(2)} class={`standart-button standart-button${themeValue}`} id="sayı">2</button>
				<button on:click={()=>number(3)} class={`standart-button standart-button${themeValue}`} id="sayı">3</button>
				<button on:click={()=>operation("substract")} class={`standart-button standart-button${themeValue}`} id="buttonSubstract">-</button>
				<button on:click={()=>dot()} class={`standart-button standart-button${themeValue}`} id="buttonDot">.</button>
				<button on:click={()=>number(0)} class={`standart-button standart-button${themeValue}`} id="sayı">0</button>
				<button on:click={()=>operation("divide")} class={`standart-button standart-button${themeValue}`} id="buttonDivide">/</button>
				<button on:click={()=>operation("multiply")} class={`standart-button standart-button${themeValue}`} id="buttonTime">x</button>
				<button on:click={()=>reset()} class={`reset reset${themeValue}`} id="buttonReset">RESET</button>
				<button on:click={()=>operation("equal")} class={`equal equal${themeValue}`} id="buttonEqual">=</button>
			</div>			
		</div>
	</div>	
</main>

<style>
	.main {
		display: flex;
		flex-direction: column;		
		align-items: center;
		width: 1440px;
		height: 900px;	
		background:#3A4663;
	}
	.main2{
		background: #F2F2F2;
	}
	.main3{
		background: #17062A
	}
	.header {		
		margin-top: 96px;
		width: 540px;
		height:44px;
		display: flex;
		justify-content: space-between;		
	}
	.title{
		display:flex;
		flex-direction: column;
		justify-content: flex-end;
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 32px;
		line-height: 36px;
		text-align: center;
		letter-spacing: -0.533333px;		
	}
	.title1 {		
		color: #FFFFFF;
	}
	.title2 {		
		color: #36362C;
	}
	.title3 {
		color:#e9e910;
	}
	.theme {
		display: flex;		
	}
	.theme-text {
		display: flex;
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 12px;
		line-height: 13px;
		text-align: center;
		letter-spacing: 1px;
		color: #FFFFFF;
		margin-top: 27px;
		margin-right:21px;
	}
	.theme-text2{
		color: #36362C;
	}
	.theme-text3{
		color: #FFE53D;
	}
	.theme-change {
		display:flex;
		flex-direction: column;
		width: 71px;
	}
	.value-text {
		display:flex;
		justify-content: space-around;
		padding-left: 4px;
		padding-right: 4px;
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 12px;
		line-height: 13px;
		text-align: center;
		color: #FFFFFF;
		margin-bottom: 5px;
	}
	.value-text2{
		color:#36362C;
	}
	.value-text3{
		color:#FFE53D;
	}
	.display {
		background: #181F33;
		margin-top: 32px;
		border-radius: 10px;
		width: 540px;
		height: 128px;
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}
	.display2{
		background:#EEEEEE;
	}
	.display3{
		background:#1E0936;
	}
	.display-box {
		height: 54px;
		width: 500px;
		margin-right: 32px;
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 48px;
		line-height: 54px;
		text-align: right;
		letter-spacing: -0.8px;
		color: #FFFFFF;
	}
	.display-box2{
		color: #36362C;
	}
	.display-box3{
		color:#FFE53D;
	}
	.inputs {
		background: #242D44;
		margin-top: 24px;
		border-radius: 10px;
		width: 540px;
		height: 480px;		
	}
	.inputs2{
		background:#D2CDCD;
	}
	.inputs3{
		background:#1E0936;
	}
	.grid-container {
		display: grid;
		grid-template-columns: repeat(4,100px);
		grid-template-rows: repeat(5,64px);
		gap: 25px;
		margin-top: 32px;
		justify-content: center;
		align-items: center;
	}
	.del {
		background: #647198;
		color: #FFFFFF;
		height:64px;
		box-sizing: border-box;
		border-radius: 10px;
		border:none;
		box-shadow: inset 0px -4px 0px #414E73;
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 20px;
		line-height: 22px;
		letter-spacing: -0.333333px;
	}
	.del2{
		background: #378187;
		box-shadow: inset 0px -4px 0px #A79E91;
	}
	.del3{
		background: #56077C;
		box-shadow: inset 0px -4px 0px #BE15F4;
	}
	.del:hover {
		background: #A2B2E1;
	}
	.del2:hover {
		background:#62B5BC;;
	}
	.del3:hover {
		background: #8631AF;
	}
	.reset {
		grid-column-start: 1;
		grid-column-end: 3;
		height:64px;
		background: #647198;
		color: #FFFFFF;
		border-radius: 10px;
		border:none;	
		font-family: Spartan;
		box-shadow: inset 0px -4px 0px #414E73;		
		font-style: normal;
		font-weight: bold;
		font-size: 20px;
		line-height: 22px;
		letter-spacing: -0.333333px;
	}
	.reset2{
		background: #378187;
		box-shadow: inset 0px -4px 0px #1B6066;
	}
	.reset3{
		background: #56077C;
		box-shadow: inset 0px -4px 0px #BE15F4;
	}
	.reset:hover {
		background: #A2B2E1;
	}
	.reset2:hover {
		background: #62B5BC;;
	}
	.reset3:hover {
		background: #8631AF;;
	}
	.equal {
		grid-column-start: 3;
		grid-column-end: 5;
		border-radius: 10px;
		border:none;
		background: #D03F2F;
		color: #FFFFFF;	
		box-shadow: inset 0px -4px 0px #93261A;	
	}
	.equal2{
		background: #C85402;
		box-shadow: inset 0px -4px 0px #873901;
	}
	.equal3{
		background: #00DED0;
		box-shadow: inset 0px -4px 0px #6CF9F1;
	}
	.equal:hover {
		background: #F96B5B;
	}
	.equal2:hover {
		background:#FF8A38;;
	}
	.equal3:hover {
		background: #93FFF8;
	}
	.style {
		font-family: Spartan;
		font-style: normal;
		font-weight: bold;
		font-size: 32px;
		line-height: 36px;
		align-items: center;
		text-align: center;
		letter-spacing: -0.533333px;
		color: #434A59;
	}		
	.standart-button {
		border-radius: 10px;
		border:none;
		background: #EAE3DC;
		box-shadow: inset 0px -4px 0px #B3A497;
	}
	.standart-button2{
		background: #E5E4E1;
		color:#36362C;
		box-shadow: inset 0px -4px 0px #A79E91;
	}
	.standart-button3{
		background: #331C4D;
		color:#FFE53D;
		box-shadow: inset 0px -4px 0px #881C9E;
	}
	.standart-button:hover {
		background: #FFFFFE;
	}
	.standart-button2:hover {
		background: #FFFFFF;
	}
	.standart-button3:hover {
		background: #6C34AC;
	}
	.slider {
		-webkit-appearance: none;
		width: 100%;		
		height: 26px;
		border-radius: 12px;
		border: none;
		background: #242D44;
		outline: none;
		opacity: 1;
		-webkit-transition: .2s;
		transition: opacity .2s;
	}
	.slider2{
		background: #D2CDCD;
	}
	.slider3{
		background: #1E0936;
	}	
	.slider::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 16px;
		height: 16px;
		border-radius: 50%;
		background: #D03F2F;
		cursor: pointer;
	}
	.slider2::-webkit-slider-thumb {
		background:#C85402;		
	}
	.slider3::-webkit-slider-thumb {
		background: #00DED0;			
	}	
	.slider::-webkit-slider-thumb:hover {
		opacity: 1;
		background: #F96B5B;
	}
	.slider2::-webkit-slider-thumb:hover {
		opacity: 1;
		background: #FF8A38;
	}
	.slider3::-webkit-slider-thumb:hover {
		opacity: 1;
		background: #93FFF8;
	}

</style>