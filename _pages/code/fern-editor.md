---
layout: page
title: Fern Editor
permalink: /code/fern/
description: Pimp your glamour!
embedimage: /img/embeds/fern.png
---

<!-- HTML -->
<script src="/scripts/jscolor.js"></script>

<input type="button" onclick="render()" value="Generate Preview"> <- Click this if something goes wrong
<div class="row">
  <div class="imgColumn"><canvas id="canvas" width="435" height="320"></canvas><canvas id="expt_canvas" width="87" height="64"></canvas> <- Right click + save to import</div>
  <div class="buttonsColumn">
  	<div id="buttons-div">
  		Sleeve: <input type="text" id="color0" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Forearm: <input type="text" id="color1" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat (Light): <input type="text" id="color2" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat (Mid): <input type="text" id="color3" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat (Dark): <input type="text" id="color4" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat Text: <input type="text" id="color5" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat (Misc): <input type="text" id="color13" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat (Misc): <input type="text" id="color23" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Shoe (Light): <input type="text" id="color7" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Coat/Shoe (Dark): <input type="text" id="color22" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Backpack: <input type="text" id="color18" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Pants: <input type="text" id="color6" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Accessories: <input type="text" id="color11" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Shirt (Light): <input type="text" id="color9" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Shirt (Dark): <input type="text" id="color19" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Shirt (Hem): <input type="text" id="color21" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Skin (Light): <input type="text" id="color12" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Skin (Mid): <input type="text" id="color24" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Skin (Dark): <input type="text" id="color25" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Skin (Shade): <input type="text" id="color26" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Eye (Dark): <input type="text" id="color14" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Eye (Light): <input type="text" id="color15" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Pupil: <input type="text" id="color16" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Hair (Light): <input type="text" id="color10" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Hair (Dark): <input type="text" id="color27" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Overlay 1: <input type="text" id="color28" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Overlay 2: <input type="text" id="color29" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		<br/>
  		Unknown: <input type="text" id="color8" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Unknown: <input type="text" id="color17" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  		Unknown: <input type="text" id="color20" style="width: 60px;" data-jscolor="{}" onChange="render();"><br/>
  	</div>
  </div>
</div> 
<canvas id="buffer" class="debug" width="435" height="320"></canvas>
<canvas id="expt_buffer" class="debug" width="435" height="320"></canvas> 
<canvas id="palette" class="debug"></canvas>

<script>
	const MASKS = ["https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_00.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_01.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_02.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_03.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_04.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_05.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_06.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_07.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_08.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_09.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_10.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_11.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_12.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_13.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_14.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_15.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_16.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_17.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_18.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_19.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_20.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_21.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_22.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_23.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_24.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_25.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_26.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_27.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_28.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_29.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/fern_mask_30.png"];

	const MASKS_EXPORTABLE = ["https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_00.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_01.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_02.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_03.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_04.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_05.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_06.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_07.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_08.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_09.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_10.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_11.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_12.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_13.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_14.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_15.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_16.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_17.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_18.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_19.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_20.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_21.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_22.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_23.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_24.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_25.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_26.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_27.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_28.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_29.png",
				   "https://github.com/Blizihguh/blizihguh.github.io/raw/master/img/fern/small/fern_mask_30.png"];

	const COLORS = ["#3E8084", "#FF9F26", "#C47922", "#315259", "#8A541E", "#CFA06B", "#0E050F", "#302722", "#0E050F", "#20303D", 
					"#431F19", "#DD8B36", "#FCC477", "#3F2C1C", "#A18F7B", "#F2E6BD", "#1B1716", "#315259", "#182126", "#626D60", 
					"#20303D", "#C0BEA7", "#502E1B", "#191919", "#7D4C27", "#DF8D2F", "#885326", "#1D0E18", "#000000", "#000000", "#AAAAAA"];

	var canvas = null;
	var ctx = null;
	var buffer = null;
	var btx = null;

	var expt_canvas = null;
	var expt_ctx = null;
	var expt_buffer = null;
	var expt_btx = null;

	var foo = 0;

	function init() {
		// Initialize colors
		for (var i=0; i<30; i++) {
			let elm = document.getElementById("color" + i.toString());
			elm.value = COLORS[i]
		}

		// Initialize canvases
		canvas = document.getElementById("canvas");
		ctx = canvas.getContext("2d");

		buffer = document.getElementById("buffer");
		buffer.width = canvas.width;
		buffer.height = canvas.height;
		btx = buffer.getContext("2d");

		expt_canvas = document.getElementById("expt_canvas");
		expt_ctx = expt_canvas.getContext("2d");

		expt_buffer = document.getElementById("expt_buffer");
		expt_buffer.width = expt_canvas.width;
		expt_buffer.height = expt_canvas.height;
		expt_btx = expt_buffer.getContext("2d");

		render();
	}

	function render() {
		load_colors();
		clear_canvas();
		for (var i=0; i<31; i++) {
			get_layer_in_buffer(i);
			draw_layer_from_buffer();
		}
	}

	function load_colors() {
		for (var i=0; i<30; i++) {
			let elm = document.getElementById("color" + i.toString());
			COLORS[i] = elm.value;
		}
	}

	function get_layer_in_buffer(idx) {
		// Create new image from the mask
		const img = new Image();
		img.src = MASKS[idx];

		// Draw the color
		btx.globalCompositeOperation = "source-over";
		btx.fillStyle = COLORS[idx];
		btx.fillRect(0, 0, buffer.width, buffer.height);

		// Mask the color
		btx.globalCompositeOperation = "darken";
		btx.drawImage(img, 0, 0);


		// Do it again for the export-sized canvas
		const expt_img = new Image();
		expt_img.src = MASKS_EXPORTABLE[idx];

		expt_btx.globalCompositeOperation = "source-over";
		expt_btx.fillStyle = COLORS[idx];
		expt_btx.fillRect(0, 0, expt_buffer.width, expt_buffer.height);

		expt_btx.globalCompositeOperation = "darken";
		expt_btx.drawImage(expt_img, 0, 0);
	}

	function clear_canvas() {
		ctx.save();
		ctx.globalCompositeOperation = "source-over";
		ctx.fillStyle = "#000000";
		ctx.fillRect(0, 0, canvas.width, canvas.height);
		ctx.restore();

		expt_ctx.save();
		expt_ctx.globalCompositeOperation = "source-over";
		expt_ctx.fillStyle = "#000000";
		expt_ctx.fillRect(0, 0, expt_canvas.width, expt_canvas.height);
		expt_ctx.restore();
	}

	function draw_layer_from_buffer() {
		ctx.globalCompositeOperation = "lighten";
		ctx.drawImage(buffer, 0, 0);

		expt_ctx.globalCompositeOperation = "lighten";
		expt_ctx.drawImage(expt_buffer, 0, 0);
	}

</script>

<!-- Set default color values -->
<script>
	init();
</script>

<style>
	.imgColumn {
	  float: left;
	  width: 50%;
	}

	.buttonsColumn {
		float: left;
		width: 50%;
	}

	/* Clear floats after the columns */
	.row:after {
	  content: "";
	  display: table;
	  clear: both;
	}

	.debug {
		display: none;
	}
</style>