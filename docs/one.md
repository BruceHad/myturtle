## Turtles

Like a lot of 80s kids, my first introduction to programming was a toy called [Big Trak](https://en.wikipedia.org/wiki/Big_Trak). It was a truck with a keypad on it's back, and it could be programmed to follow a route...3 forward, turn right, reverse 5 and so on. 

AKA a [Turtle](https://en.wikipedia.org/wiki/Turtle_graphics)), to program one it just needs to know two bit of information: where it is and what direction it's facing. On top of that, it needs to know how to perform a couple of actions: move forward and rotate.

	function Turtle(){
	  var location = [0.5,0.5]; // Half pixel offset
	  var angle = 0; // Radians
	  var pen = new Pen();
	  var canvas = new Canvas();
	  this.rotate = function(anglePercent) {
	    // to simplify the maths anglePercent is a percentage of
	    // a full circle. e.g to rotate turtle by 90 degrees == rotate(0.25).
	    angle += anglePercent * Math.PI *2;
	  };
	  this.forward = function(dist) {
	    pos2 = [location[0]+ Math.cos(angle) * dist, location[1]+ Math.sin(angle) * dist];
	    if(pen.draw) canvas.draw(location, pos2, pen);
	    location = [pos2[0], pos2[1]];
	  };
	}
	
And that's pretty much all the code that's needed for a turtle. Though in order two implement this in HTML/Javascript we need a pen and a [canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) with some line drawing capability. Something like this.

	function Pen() {
		var colour = '#000000';
		var width = 1;
		this.draw = true;
		this.pop = function() {
			draw = !draw
		};
	};

	function Canvas(canvasId) {
		var canvas = document.getElementById(canvasId);
		var ctx = canvas.getContext('2d');
		var intId = null;
		var steps = 10;
		ctx.clearRect(0, 0, canvas.width, canvas.height);
		var count = 0;
		this.draw = function(start, end, pen) {
			ctx.strokeStyle = pen.colour;
			ctx.lineWidth = pen.width;
			ctx.beginPath();
			ctx.moveTo(start[0], start[1]);
			ctx.lineTo(end[0], end[1]);
			ctx.stroke();
		};
	}

And I have added a few basic controls and animated the line drawing just for kicks.