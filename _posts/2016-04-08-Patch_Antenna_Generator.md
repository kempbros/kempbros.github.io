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
					<input type="number" class="form-control" id="inputGhz" placeholder="5.795" value="5.795">
				</div>

				<label for="inputDC" class="col-lg-2 control-label">Dialectric Constant</label>
				<div class="col-lg-10">
					<input type="number" class="form-control" id="inputDC" placeholder="4.5" value="4.5">
					<div class="well" style="display:none;">
						The dielectric constant of FR4 (which is circuit board material) is typically 4.5
					</div>
				</div>

				<label for="inputH" class="col-lg-2 control-label">Dielectric Height in mm</label>
				<div class="col-lg-10">
					<input type="number" class="form-control" id="inputH" placeholder="1.5" value="1.5">
				</div>
			</div>
				<p>
					<a href="#" id="generateAntenna" class="btn btn-primary">Generate</a>
				</p>
		</fieldset>
	</form>
</div>

<script>
	var c = 299792458;

	function drawAntenna() {
		var ghz = parseFloat( $( '#inputGhz' ).val() );
		var dc = parseFloat( $( '#inputDC' ).val() );
		var inputH = parseFloat( $( '#inputH' ).val() );

		var antenna = {};
		
		antenna.f_zero = ghz * 1000000000;

		antenna.sum_R = dc;

		antenna.h = inputH / 1000;


		antenna.width = (c/((2*antenna.f_zero)*Math.sqrt((antenna.sum_R+1)/2)));

		antenna.sum_eff = ((antenna.sum_R+1)/2)+((antenna.sum_R-1)/2)* Math.pow( (1+12*(antenna.h/antenna.width)), (-1/2) );

		antenna.L_eff = c/(2*antenna.f_zero*Math.sqrt(antenna.sum_eff ));

		antenna.delta_L = (0.412*antenna.h)*(((antenna.sum_eff+0.3)*((antenna.width/antenna.h)+0.264))/((antenna.sum_eff-0.258)*((antenna.width/antenna.h)+0.8)));

		antenna.width = ( c/((2*antenna.f_zero)*Math.sqrt((antenna.sum_R+1)/2)));

		antenna.length = antenna.L_eff-2*(antenna.delta_L);

		antenna.Q0 = (c*Math.sqrt(antenna.sum_R))/(4*antenna.f_zero*antenna.h);

		antenna.delta_ss = 1/(2*antenna.Q0);

		antenna.corner_a = antenna.length*Math.sqrt(antenna.delta_ss);

		antenna.feed_y = antenna.length/(2*Math.sqrt(antenna.sum_R ) );

		antenna.feed_x = antenna.width/2;

		antenna.groundplane = {};

		antenna.groundplane.width = antenna.width +( antenna.h*4);

		antenna.groundplane.length = antenna.length+( antenna.h * 4);

		antenna.coordinates = {
			'feed': { 'X0': (antenna.groundplane.width * 1000 )/2,
						'Y0': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.feed_y * 1000 )
					},
			'groundplane': { 'X0': 0,
						'Y0': 0,
						'X1': (antenna.groundplane.width * 1000 ),
						'Y1': 0,
						'X2': (antenna.groundplane.width * 1000 ),
						'Y2': (antenna.groundplane.length * 1000 ),
						'X3': 0,
						'Y3': (antenna.groundplane.length * 1000 )
					},
			'lp_patch': { 'X0': ((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2,
						'Y0': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X1': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y1': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X2': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y2': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ),
						'X3': ((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2,
						'Y3': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 )
					},
			'rhp_patch': { 'X0': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.corner_a * 1000 ),
						'Y0': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X1': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y1': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X2': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y2': ((((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ))-(antenna.corner_a * 1000 ),
						'X3': ((((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ))-(antenna.corner_a * 1000 ),
						'Y3': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ),
						'X4': ((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2,
						'Y4': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ),
						'X5': ((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2,
						'Y5': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.corner_a * 1000 )
					},
			'lhp_patch': { 'X0': ((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2,
						'Y0': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X1': ((((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ))-(antenna.corner_a * 1000 ),
						'Y1': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'X2': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y2': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.corner_a * 1000 ),
						'X3': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.width * 1000 ),
						'Y3': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ),
						'X4': (((antenna.groundplane.width * 1000 )-(antenna.width * 1000 ))/2)+(antenna.corner_a * 1000 ),
						'Y4': (((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ),
						'X5': ((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2,
						'Y5': ((((antenna.groundplane.length * 1000 )-(antenna.length * 1000 ))/2)+(antenna.length * 1000 ))-(antenna.corner_a * 1000 )
					}
		};



		console.log( antenna );
		
	}

	$( '#generateAntenna' ).click( drawAntenna() );
</script>

