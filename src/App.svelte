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
	console.log(themeValue);	
}

const number = (x) => {
	if (operator) {
		value=x;
	} else {
		if (dotClicked) {	
			value= Number(value) + x*(Math.pow(10, -(counter)));
			counter++;
		}else{
			value = (value*10)+ x ;
		}		
	}	
	operator = false;
	firstTime = true;
}
const add = () =>{
	if (storage[0]==0) {
		storage[0]=value;
		
	} else if (operatorWhich!="add") {
		switch (operatorWhich) {
			case "multiply": multiply(); break;		
			case "divide": divide(); break;
			case "substract": substract(); break;
		}
	} else if (firstTime) {
		value=storage[0]+value;	
		storage[0]=value;
		firstTime = false;
	}
	operator=true;
	operatorWhich ="add"
	dotClicked=false;
	counter=1;

}
const multiply = () =>{
	if (storage[0]==0) {
		storage[0]=value;
		
	} else if (operatorWhich!="multiply") {
		switch (operatorWhich) {
			case "add": add(); break;		
			case "divide": divide(); break;
			case "substract": substract(); break;
		}		
 	} else if (firstTime){
		value=storage[0]*value;	
		storage[0]=value;
		firstTime = false;
	}		
	operator=true;
	operatorWhich ="multiply"
	dotClicked =false;
	counter=1;
}

const divide = () =>{
	if (storage[0]==0) {
		storage[0]=value;
		
	} else if (operatorWhich!="divide") {
		switch (operatorWhich) {
			case "add": add(); break;		
			case "multiply": multiply(); break;
			case "substract": substract(); break;
		}		
 	} else if (firstTime){
		value=(storage[0])/value;	
		storage[0]=value;
		firstTime = false;
	}		
	operator=true;
	operatorWhich ="divide"
	dotClicked= false;
	counter=1;
}
const substract = () =>{
	if (storage[0]==0) {
		storage[0]=value;		
	} else if (operatorWhich!="substract") {
		switch (operatorWhich) {
			case "add": add(); break;		
			case "multiply": multiply(); break;
			case "divide": divide(); break;
		}		
 	} else if (firstTime){
		value=(storage[0])-(value);	
		storage[0]=value;
		firstTime = false;
	}		
	operator=true;
	operatorWhich ="substract"
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
		storage[0] = value;
		console.log(value);
		dotClicked = true;
	}
	
}
/* 
	onMount(()=> {
		let slider = document.getElementById("myRange");

		slider.addEventListener("change", (a) => {
			themeValue = a.target.value;
			console.log(themeValue);
		})
	}); */
	

</script>

<main>
	<div class="main">
		<div class="header">
			<div class={ `title title${themeValue}`}>calc</div>
			<div class="theme">
				<div class="theme-text">THEME</div>
				<div class="theme-change">
					<div class="value-text">
						<div>1</div>
						<div>2</div>
						<div>3</div>
					</div>					
					<div class="slidecontainer">
						<input type="range" on:change={updateTheme} min="1" max="3" value="1" class="slider" id="myRange">						
					</div>
				</div>
			</div>
		</div>
		<div class="display">
			<div class="display-box">				
				{value}
			</div>
		</div>
		<div class="inputs style">
			<div class="grid-container">
				<button on:click={()=>number(7)} class="standart-button">7</button>
				<button on:click={()=>number(8)} class="standart-button" id="sayı">8</button>
				<button on:click={()=>number(9)} class="standart-button" id="sayı">9</button>
				<button class="del">Del</button>
				<button on:click={()=>number(4)} class="standart-button" id="sayı">4</button>
				<button on:click={()=>number(5)} class="standart-button" id="sayı">5</button>
				<button on:click={()=>number(6)} class="standart-button" id="sayı">6</button>
				<button on:click={()=>add()} class="standart-button" id="buttonAdd">+</button>
				<button on:click={()=>number(1)} class="standart-button" id="sayı">1</button>
				<button on:click={()=>number(2)} class="standart-button" id="sayı">2</button>
				<button on:click={()=>number(3)} class="standart-button" id="sayı">3</button>
				<button on:click={()=>substract()} class="standart-button" id="buttonSubstract">-</button>
				<button on:click={()=>dot()} class="standart-button" id="buttonDot">.</button>
				<button on:click={()=>number(0)} class="standart-button" id="sayı">0</button>
				<button on:click={()=>divide()} class="standart-button" id="buttonDivide">/</button>
				<button on:click={()=>multiply()} class="standart-button" id="buttonTime">x</button>
				<button on:click={()=>reset()} class="reset" id="buttonReset">Reset</button>
				<button class="equal" id="buttonEqual">=</button>

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
	.inputs {
		background: #242D44;
		margin-top: 24px;
		border-radius: 10px;
		width: 540px;
		height: 480px;
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
		border-radius: 10px;
		border:none;
	}
	.del:hover {
		background: #A2B2E1;
	}

	.reset {
		grid-column-start: 1;
		grid-column-end: 3;
		background: #647198;
		color: #FFFFFF;
		border-radius: 10px;
		border:none;		
	}
	.reset:hover {
		background: #A2B2E1;
	}
	.equal {
		grid-column-start: 3;
		grid-column-end: 5;
		border-radius: 10px;
		border:none;
		background: #D03F2F;
		color: #FFFFFF;		
	}
	.equal:hover {
		background: #F96B5B;
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
	}
	.standart-button:hover {
		background: #FFFFFE;
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

		
	.slider::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 16px;
		height: 16px;
		border-radius: 50%;
		background: #D03F2F;
		cursor: pointer;
	}

	
	.slider::-webkit-slider-thumb:hover {
		opacity: 1;
		background: #F96B5B;
	}








</style>