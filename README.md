<style>

body {
margin: 0;
padding: 0;
}

</style>

<canvas id=game></canvas>

<script>

function randomCharacter() {
	return String.fromCharCode(65 + Math.floor(Math.random() * 25));
}

class Note {
	constructor(char) {
    	this.char = char;
    	this.age = 0;
    }
    
    update() {
    	this.age++;
    }
    
    render(x, y) {
    	context.fillStyle = "green";
        if (this.age >= 20) context.fillStyle = "orange";
        if (this.age >= 40) context.fillStyle = "red";
    	context.font = "50px Arial";
		context.fillText(this.char, x, y); 
    }
    
    shouldDie() {
    	return this.age >= 60;
    }
    
}

const characterSpace = 50;

const canvas = document.getElementById("game");
const context = canvas.getContext("2d");

const width = window.innerWidth;
const height = window.innerHeight;
canvas.width = width;
canvas.height = height;

context.textAlign = "center"; 

function clear() {
context.fillStyle = "gray";
context.fillRect(0, 0, width, height);
}

let notes = [];
notes.push(new Note("A"));

function render() {
clear();
for (let i = (notes.length - 1); i >= 0; i--) {
notes[i].update();
notes[i].render(width / 2, height / 2);
if (notes[i].shouldDie()) notes.splice(i, 1);
}
requestAnimationFrame(render);
}

render();

</script>
