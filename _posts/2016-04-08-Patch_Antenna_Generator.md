---
layout: post
title: Patch Antenna Generator
description: "JavaScript patch antenna generator"
modified: 2016-04-08
tags: [patch anntenna]
categories: [stuff]
---

<div id="content">
	<form class="form-horizontal">
		<fieldset>
			<legend>Input</legend>
			<div class="form-group">
				<label for="inputGhz" class="col-lg-2 control-label">Ghz</label>
				<div class="col-lg-10">
					<input type="number" class="form-control" id="inputGhz" placeholder="5.795">
				</div>

				<label for="inputFoo" class="col-lg-2 control-label">Foo</label>
				<div class="col-lg-10">
					<input type="number" class="form-control" id="inputFoo" placeholder="4.5">
				</div>

				<label for="inputBar" class="col-lg-2 control-label">Bar</label>
				<div class="col-lg-10">
					<input type="number" class="form-control" id="inputBar" placeholder="1.5">
				</div>
			</div>
				<a href="#" id="generateAntenna" class="btn btn-primary">Generate</a>
		</fieldset>
	</form>
</div>

<script>
	var c = 299792458;

	function drawAntenna() {
		var ghz = $( '#inputGhz' ).val();
		var foo = $( '#inputFoo' ).val();
		var bar = $( '#inputBar' ).val();
		
    var antenna = {};

		antenna.f_zero = ghz * 1000000000;

    antenna.sum_R = foo;

    antenna.h = bar / 1000;


    antenna.width = (c/((2*antenna.f_zero)*Math.pow((antenna.sum_R+1)/2, 0.5 ) ));

    antenna.sum_eff = Math.pow( ((antenna.sum_R+1)/2)+((antenna.sum_R-1)/2)*(1+12*(antenna.h/antenna.width)), (-1/2) );

    antenna.L_eff = c/(2*antenna.f_zero*Math.pow(antenna.sum_eff, 0.5));

    antenna.delta_L = (0.412*antenna.h)*(((antenna.sum_eff+0.3)*((antenna.width/antenna.h)+0.264))/((antenna.sum_eff-0.258)*((antenna.width/antenna.h)+0.8)));

    antenna.height = antenna.L_Eff-2*(antenna.delta_L);

    antenna.length = antenna.L_eff-2*(antenna.delta_L);

    console.log( antenna );
		
	}

	$( '#generateAntenna' ).click( drawAntenna() );
</script>

