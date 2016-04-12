---
layout: post
title: Patch Antenna Generator
description: "JavaScript patch antenna generator"
modified: 2016-04-08
tags: [patch anntenna rf electromagnetic radiation spectrum]
categories: [antennas]
---

<style>
	table {
		border-collapse: collapse;
	}

	tr.border_bottom th {
		border-bottom: 1px solid black;
	}

	tr.border_bottom td {
		border-bottom: 1px solid black;
	}

	.border_right {
		border-right: 1px solid black;
	}

	.section {
		padding-top: 1em;
	}

</style>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.16/d3.min.js"></script>

<div id="content">
	<div class="row">
		<div class="column" style="width: 40%; display: inline-block;">
			<form class="form-horizontal">
				<fieldset>
					<legend>Input</legend>
					<div class="form-group">
						<label for="inputGhz" class="col-lg-2 control-label">Ghz</label>
						<div class="col-lg-10" style="padding-bottom: 1em;">
							<input type="number" class="form-control" id="inputGhz" placeholder="5.795" value="5.795">
						</div>

						<label for="inputDC" class="col-lg-2 control-label">Dialectric Constant</label>
						<div class="col-lg-10" style="padding-bottom: 1em;">
							<input type="number" class="form-control" id="inputDC" placeholder="4.5" value="4.5">
							<div class="well" style="display:none;">
								The dielectric constant of FR4 (which is circuit board material) is typically 4.5
							</div>
						</div>

						<label for="inputH" class="col-lg-2 control-label">Dielectric Height in mm</label>
						<div class="col-lg-10" style="padding-bottom: 1em;">
							<input type="number" class="form-control" id="inputH" placeholder="1.5" value="1.5">
						</div>

						<label for="eagle_type">Antenna Type</label>
						<select id="eagle_type">
							<option value="rhp_patch">RHP Patch</option>
							<option value="lhp_patch">LHP Patch</option>
							<option value="lp_patch">Linear Patch</option>
						</select>
					</div>
						<p>
							<button id="generateAntenna" class="btn btn-primary">Generate</button>
						</p>
				</fieldset>
			</form>
		</div>
		<div id="antenna_container" style="display: inline-block; margin: auto; vertical-align: top; padding-left: 25%; padding-top: 25%;">
			<svg id="antenna_svg">
				<g id="antenna_patch_group" transform="scale( 3.543307 )"></g>				
			</svg>
		</div>
	</div>

	<br />

	<div class="row">
		<div class="col-lg-12">
			<fieldset>
				<legend>Eagle Script</legend>
				<textarea id="eagle" style="width: 100%;" rows="14"></textarea>
				<p>
					<button id="saveEagle" class="btn btn-primary">Save</button>
				</p>
			</fieldset>
		</div>
	</div>

	<br />

	<div class="row">
		<div class="col-lg-12" class="section">
			<table>
				<thead>
					<tr class="border_bottom">
						<th class="border_right">Coordinates</th>
						<th class="border_right">X0</th>
						<th class="border_right">Y0</th>
						<th class="border_right">X1</th>
						<th class="border_right">Y1</th>
						<th class="border_right">X2</th>
						<th class="border_right">Y2</th>
						<th class="border_right">X3</th>
						<th class="border_right">Y3</th>
						<th class="border_right">X4</th>
						<th class="border_right">Y4</th>
						<th class="border_right">X5</th>
						<th>Y5</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border_bottom">
						<td class="border_right">Feed</td>
						<td id="feed_X0" class="border_right"></td>
						<td id="feed_Y0" class="border_right"></td>
						<td id="feed_X1" class="border_right"></td>
						<td id="feed_Y1" class="border_right"></td>
						<td id="feed_X2" class="border_right"></td>
						<td id="feed_Y2" class="border_right"></td>
						<td id="feed_X3" class="border_right"></td>
						<td id="feed_Y3" class="border_right"></td>
						<td id="feed_X4" class="border_right"></td>
						<td id="feed_Y4" class="border_right"></td>
						<td id="feed_X5" class="border_right"></td>
						<td id="feed_Y5"></td>
					</tr>
					<tr class="border_bottom">
						<td class="border_right">Groundplane</td>
						<td id="groundplane_X0" class="border_right"></td>
						<td id="groundplane_Y0" class="border_right"></td>
						<td id="groundplane_X1" class="border_right"></td>
						<td id="groundplane_Y1" class="border_right"></td>
						<td id="groundplane_X2" class="border_right"></td>
						<td id="groundplane_Y2" class="border_right"></td>
						<td id="groundplane_X3" class="border_right"></td>
						<td id="groundplane_Y3" class="border_right"></td>
						<td id="groundplane_X4" class="border_right"></td>
						<td id="groundplane_Y4" class="border_right"></td>
						<td id="groundplane_X5" class="border_right"></td>
						<td id="groundplane_Y5"></td>
					</tr>
					<tr class="border_bottom">
						<td class="border_right">LP Patch</td>
						<td id="lp_patch_X0" class="border_right"></td>
						<td id="lp_patch_Y0" class="border_right"></td>
						<td id="lp_patch_X1" class="border_right"></td>
						<td id="lp_patch_Y1" class="border_right"></td>
						<td id="lp_patch_X2" class="border_right"></td>
						<td id="lp_patch_Y2" class="border_right"></td>
						<td id="lp_patch_X3" class="border_right"></td>
						<td id="lp_patch_Y3" class="border_right"></td>
						<td id="lp_patch_X4" class="border_right"></td>
						<td id="lp_patch_Y4" class="border_right"></td>
						<td id="lp_patch_X5" class="border_right"></td>
						<td id="lp_patch_Y5"></td>
					</tr>
					<tr class="border_bottom">
						<td class="border_right">RHP Patch</td>
						<td id="rhp_patch_X0" class="border_right"></td>
						<td id="rhp_patch_Y0" class="border_right"></td>
						<td id="rhp_patch_X1" class="border_right"></td>
						<td id="rhp_patch_Y1" class="border_right"></td>
						<td id="rhp_patch_X2" class="border_right"></td>
						<td id="rhp_patch_Y2" class="border_right"></td>
						<td id="rhp_patch_X3" class="border_right"></td>
						<td id="rhp_patch_Y3" class="border_right"></td>
						<td id="rhp_patch_X4" class="border_right"></td>
						<td id="rhp_patch_Y4" class="border_right"></td>
						<td id="rhp_patch_X5" class="border_right"></td>
						<td id="rhp_patch_Y5"></td>
					</tr>
					<tr>
						<td class="border_right">LHP Patch</td>
						<td id="lhp_patch_X0" class="border_right"></td>
						<td id="lhp_patch_Y0" class="border_right"></td>
						<td id="lhp_patch_X1" class="border_right"></td>
						<td id="lhp_patch_Y1" class="border_right"></td>
						<td id="lhp_patch_X2" class="border_right"></td>
						<td id="lhp_patch_Y2" class="border_right"></td>
						<td id="lhp_patch_X3" class="border_right"></td>
						<td id="lhp_patch_Y3" class="border_right"></td>
						<td id="lhp_patch_X4" class="border_right"></td>
						<td id="lhp_patch_Y4" class="border_right"></td>
						<td id="lhp_patch_X5" class="border_right"></td>
						<td id="lhp_patch_Y5"></td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</div>

<script>
	var antenna = {};

	function drawAntenna() {
		var ghz = parseFloat( $( '#inputGhz' ).val() );
		var dc = parseFloat( $( '#inputDC' ).val() );
		var inputH = parseFloat( $( '#inputH' ).val() );
		var c = 299792458;

		antenna = {};

		antenna.ghz = ghz;
		antenna.dc = dc;
		antenna.inputH = inputH;
		
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

		for ( var coord_type in antenna.coordinates ) {
			
			[0,1,2,3,4,5].forEach( function( step ) {
				x = '';
				y = '';
				if ( antenna.coordinates[ coord_type ].hasOwnProperty( 'X' + step ) ) {
					x = antenna.coordinates[ coord_type ][ 'X' + step ].toFixed( 2 );
					antenna.coordinates[ coord_type ][ 'X' + step ] = parseFloat( x );
					y = antenna.coordinates[ coord_type ][ 'Y' + step ].toFixed( 2 );
					antenna.coordinates[ coord_type ][ 'Y' + step ] = parseFloat( y );
				}

				$( '#' + coord_type + '_X' + step ).html( x );
				$( '#' + coord_type + '_Y' + step ).html( y );

				
			});
		}

		create_eagle( antenna );
		create_svg( antenna );

		return antenna;

	}

	function create_eagle( antenna ) {
		type = $( '#eagle_type' ).val();

		c = antenna.coordinates;
		eagle_scr = "BRD:" + '\r';
		eagle_scr += "GRID MM" + '\r';
		eagle_scr += "CHANGE ISOLATE 0" + '\r';
		eagle_scr += "SET WIRE_BEND 2" + '\r';
		eagle_scr += "LAYER Dimension" + '\r';
		eagle_scr += "WIRE 0.0 (" + c.groundplane.X0 + ' ' + c.groundplane.Y0 + ') ';
			eagle_scr += '(' + c.groundplane.X1 + ' ' + c.groundplane.Y1 + ') ';
			eagle_scr += '(' + c.groundplane.X2 + ' ' + c.groundplane.Y2 + ') ';
			eagle_scr += '(' + c.groundplane.X3 + ' ' + c.groundplane.Y3 + ') ';
			eagle_scr += '(0 0)' + '\r';
		eagle_scr += "LAYER Bottom" + '\r';
		eagle_scr += "POLYGON 'GND' 0.0 (" + c.groundplane.X0 + ' ' + c.groundplane.Y0 + ') ';
			eagle_scr += '(' + c.groundplane.X1 + ' ' + c.groundplane.Y1 + ') ';
			eagle_scr += '(' + c.groundplane.X2 + ' ' + c.groundplane.Y2 + ') ';
			eagle_scr += '(' + c.groundplane.X3 + ' ' + c.groundplane.Y3 + ') ';
			eagle_scr += '(0 0)' + '\r';
		eagle_scr += "LAYER Top" + '\r';
		eagle_scr += "POLYGON 'PATCH' 0.0 ("+ c[ type ].X0 + ' ' + c[ type ].Y0 + ') ';
			eagle_scr += '(' + c[ type ].X1 + ' ' + c[ type ].Y1 + ') ';
			eagle_scr += '(' + c[ type ].X2 + ' ' + c[ type ].Y2 + ') ';
			eagle_scr += '(' + c[ type ].X3 + ' ' + c[ type ].Y3 + ') ';

			if ( type != 'lp_patch' ) {
				eagle_scr += '(' + c[ type ].X4 + ' ' + c[ type ].Y4 + ') ';
				eagle_scr += '(' + c[ type ].X5 + ' ' + c[ type ].Y5 + ') ';

				if( type == 'lhp_patch' ) {
					eagle_scr += '(' + c[ type ].X5 + ' ' + c[ type ].Y5 + ')';
				} else {
					eagle_scr += '(' + c[ type ].Y5 + ' ' + c[ type ].X5 + ')';
				}			
			}

		eagle_scr += '\r';
			
		eagle_scr += "CHANGE DRILL 1" + '\r';
		eagle_scr += "VIA 'PATCH' auto round" + ' (' + c.feed.X0 + ' ' + c.feed.Y0 + ')' + '\r';
		eagle_scr += "RATSNEST";

		$( '#eagle' ).html( '' );
		$( '#eagle' ).html( eagle_scr );

	}


	function create_svg( antenna ) {
		// Clear out the old patch
		$( '#antenna_patch_group' ).html( '' );
		type = $( '#eagle_type' ).val();
		svg = d3.select( '#antenna_svg' );
		antenna_patch_group = d3.select( '#antenna_patch_group' );

		c = antenna.coordinates;

		svg.attr( "width", c.groundplane.X1 + 'mm' );
		svg.attr( "height", c.groundplane.Y2 + 'mm' );


		patch_polygon = [];


		[0,1,2,3,4,5].forEach( function( step ) {
			if ( c[ type ].hasOwnProperty( 'X' + step ) ) {
				patch_polygon.push( c[ type ][ 'X' + step ].toFixed( 2 ) + ',' + c[ type ][ 'Y' + step ].toFixed( 2 ) );
			}

		})

		antenna_patch_group.selectAll( 'polygon' )
			.data( [ patch_polygon ] )
			.enter()
			.append( 'polygon' )
			.attr( 'points', patch_polygon.join( ' ' ) )
			.attr( 'stroke','black' )
			.attr( 'stroke-width',2 );
	}


	$( '#generateAntenna' ).click( function( e ) {
		e.preventDefault();
		antenna = drawAntenna();
	});

	$( '#saveEagle' ).click( function( e ) {
		e.preventDefault();
		save_eagle( $( '#eagle' ).html() );
	});

	$( '#eagle_type' ).change( function() {
		antenna = drawAntenna();
		create_eagle( antenna );
		create_svg( antenna );
	});

	function save_eagle( scr ) {
		type = $( '#eagle_type' ).val();

		var tempElement = document.createElement( 'a' );
		tempElement.href = 'data:attachment/text,' + encodeURI( scr );
		tempElement.target = '_blank';
		tempElement.download = 'KempBros_Patch_Antenna_' + type + '.txt';
		tempElement.click();
	}
</script>

