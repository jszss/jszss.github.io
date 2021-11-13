---
title: '弹出式环形菜单'
date: 2019-10-09 12:08:32
tags: [css 特效,CSS3]
published: true
hideInList: false
feature: 
---
# 弹出式环形菜单(https://codepen.io/HelKyle/pen/qygvJz)
```html
<div class="popping-menu">
<input class="checkbox" id="checkbox" type="checkbox" />
<button>
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve" fill="white">
<g>
	<g>
		<g>
			<path d="M384,0H128c-14.138,0-25.6,11.461-25.6,25.6v460.8c0,14.138,11.461,25.6,25.6,25.6h256c14.138,0,25.6-11.461,25.6-25.6     V25.6C409.6,11.461,398.138,0,384,0z M392.533,68.267H196.267c-4.713,0-8.533,3.82-8.533,8.533s3.82,8.533,8.533,8.533h196.267     v332.8h-25.6c-4.713,0-8.533,3.82-8.533,8.533s3.82,8.533,8.533,8.533h25.6v51.2c0,4.713-3.82,8.533-8.533,8.533H128     c-4.713,0-8.533-3.82-8.533-8.533v-51.2h196.267c4.713,0,8.533-3.82,8.533-8.533s-3.82-8.533-8.533-8.533H119.467v-332.8h25.6     c4.713,0,8.533-3.82,8.533-8.533s-3.82-8.533-8.533-8.533h-25.6V25.6c0-4.713,3.82-8.533,8.533-8.533h256     c4.713,0,8.533,3.82,8.533,8.533V68.267z"></path>
			<path d="M264.533,460.8h-17.067c-4.713,0-8.533,3.82-8.533,8.533s3.82,8.533,8.533,8.533h17.067c4.713,0,8.533-3.82,8.533-8.533     S269.246,460.8,264.533,460.8z"></path>
		</g>
	</g>
</g>
</svg>
</button>
<button><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512.001 512.001" style="enable-background:new 0 0 512.001 512.001;" xml:space="preserve" fill="white">
<g>
	<g>
		<path d="M356,145.993c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10c5.52,0,10-4.48,10-10S361.52,145.993,356,145.993z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M156,345.993c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10s10-4.48,10-10C166,350.473,161.52,345.993,156,345.993z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M508.532,214.332c-0.811-4.815-4.98-8.34-9.862-8.34h-38.684c-5.079-20.77-13.275-40.497-24.447-58.838l29.082-29.081    c3.453-3.454,3.907-8.897,1.073-12.875c-16.262-22.821-36.079-42.638-58.9-58.9c-3.977-2.833-9.419-2.381-12.875,1.073    l-29.081,29.082C346.497,65.282,326.77,57.084,306,52.006V13.323c0-4.882-3.525-9.051-8.34-9.861    c-27.347-4.604-55.973-4.604-83.319,0C209.525,4.272,206,8.441,206,13.323v38.683c-20.778,5.08-40.508,13.278-58.839,24.446    l-29.08-29.081c-3.454-3.454-8.897-3.908-12.875-1.073c-22.821,16.262-42.638,36.079-58.9,58.9    c-2.834,3.978-2.38,9.42,1.073,12.875l29.082,29.081c-11.172,18.341-19.368,38.068-24.447,58.838H13.33    c-4.882,0-9.051,3.525-9.861,8.34C1.167,228.007,0,242.022,0,255.993c0,13.97,1.167,27.986,3.469,41.66    c0.811,4.815,4.979,8.34,9.861,8.34h38.683c5.08,20.778,13.278,40.508,24.446,58.839l-29.081,29.08    c-3.453,3.454-3.907,8.897-1.073,12.875c16.262,22.821,36.079,42.638,58.9,58.9c3.977,2.834,9.42,2.381,12.875-1.073    l29.081-29.082C165.503,446.704,185.23,454.9,206,459.978v38.684c0,4.882,3.525,9.051,8.34,9.861    c13.671,2.302,27.688,3.469,41.66,3.469s27.989-1.167,41.66-3.469c4.814-0.811,8.34-4.979,8.34-9.861V459.98    c20.778-5.08,40.508-13.278,58.839-24.446l29.08,29.081c3.454,3.453,8.896,3.906,12.875,1.073    c22.821-16.262,42.638-36.079,58.9-58.9c2.834-3.978,2.38-9.42-1.073-12.875L435.54,364.83    c11.172-18.341,19.368-38.068,24.447-58.838h38.684c4.882,0,9.051-3.525,9.861-8.34c2.302-13.673,3.469-27.69,3.469-41.66    C512.001,242.022,510.834,228.007,508.532,214.332z M490.054,285.993H451.98c-4.754,0-8.851,3.347-9.799,8.006    c-4.855,23.854-14.18,46.298-27.715,66.708c-2.629,3.965-2.101,9.234,1.263,12.598l28.658,28.658    c-12.254,15.943-26.475,30.163-42.417,42.417l-28.658-28.658c-3.364-3.365-8.634-3.893-12.6-1.261    c-20.395,13.532-42.837,22.856-66.706,27.714c-4.659,0.948-8.006,5.045-8.006,9.799v38.074c-19.816,2.586-40.184,2.586-60,0    v-38.074c0-4.754-3.347-8.851-8.006-9.799c-23.854-4.855-46.298-14.18-66.708-27.715c-3.966-2.63-9.234-2.102-12.598,1.263    l-28.658,28.658c-15.943-12.254-30.163-26.475-42.417-42.417l28.658-28.658c3.365-3.364,3.892-8.634,1.261-12.6    C84,340.311,74.676,317.868,69.818,294c-0.948-4.659-5.045-8.006-9.799-8.006H21.946c-1.293-9.911-1.946-19.967-1.946-30    c0-10.033,0.653-20.089,1.946-30H60.02c4.754,0,8.851-3.347,9.799-8.006c4.855-23.854,14.18-46.298,27.715-66.708    c2.629-3.965,2.101-9.234-1.263-12.598l-28.658-28.658c12.255-15.943,26.475-30.163,42.418-42.417l28.658,28.658    c3.364,3.364,8.634,3.893,12.6,1.261c20.395-13.532,42.837-22.856,66.706-27.714c4.659-0.948,8.006-5.045,8.006-9.799V21.939    c19.821-2.586,40.179-2.586,60,0v38.074c0,4.754,3.347,8.851,8.006,9.799c23.854,4.855,46.298,14.18,66.708,27.715    c3.964,2.629,9.233,2.101,12.598-1.263l28.658-28.658c15.943,12.254,30.163,26.475,42.417,42.417l-28.658,28.658    c-3.364,3.364-3.892,8.633-1.263,12.598c13.535,20.41,22.86,42.853,27.715,66.708c0.948,4.659,5.045,8.006,9.799,8.006h38.074    c1.293,9.911,1.946,19.967,1.946,30C492.001,266.025,491.347,276.082,490.054,285.993z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M327.972,124.405c-21.947-12.047-46.835-18.414-71.972-18.414c-82.71,0-150,67.29-150,150    c0,25.137,6.367,50.024,18.414,71.972c2.665,4.857,8.751,6.604,13.578,3.955c4.842-2.657,6.612-8.736,3.955-13.578    C131.514,299.335,126,277.775,126,255.993c0-71.682,58.318-130,130-130c21.782,0,43.342,5.514,62.349,15.946    c4.84,2.657,10.921,0.888,13.578-3.955C334.585,133.142,332.814,127.064,327.972,124.405z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M387.586,184.022c-2.657-4.843-8.736-6.613-13.578-3.955c-4.842,2.657-6.612,8.736-3.955,13.578    C380.486,212.65,386,234.211,386,255.993c0,71.682-58.318,130-130,130c-21.782,0-43.342-5.514-62.349-15.946    c-4.839-2.656-10.92-0.887-13.578,3.955c-2.658,4.841-0.887,10.92,3.955,13.578c21.947,12.047,46.835,18.414,71.972,18.414    c82.71,0,150-67.29,150-150C406,230.856,399.633,205.97,387.586,184.022z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M256,145.993c-60.654,0-110,49.346-110,110s49.346,110,110,110s110-49.346,110-110S316.654,145.993,256,145.993z     M256,345.993c-49.626,0-90-40.374-90-90c0-49.626,40.374-90,90-90c49.626,0,90,40.374,90,90    C346,305.618,305.626,345.993,256,345.993z"></path>
	</g>
</g>
</svg></button>
<button><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve" fill="white">
<g>
	<g>
		<path d="M416,426c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10c5.52,0,10-4.48,10-10C426,430.48,421.52,426,416,426z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M446,47.432V30c0-16.542-13.458-30-30-30H96C79.458,0,66,13.458,66,30v17.432C0.773,167.896,0.003,164.319,0,169.989    c0,0.004,0,0.007,0,0.011v20c0,17.333,10.022,33.453,26,42.62V502c0,5.522,4.478,10,10,10h440c5.522,0,10-4.478,10-10V232.62    c15.817-9.159,26-25.469,26-42.62v-20c0-0.004,0-0.007,0-0.011C511.997,164.258,510.591,166.721,446,47.432z M485.088,160h-61.88    L389.875,60h40.213L485.088,160z M346,180h60v10c0,16.542-13.458,30-30,30s-30-13.458-30-30V180z M344.471,160L327.805,60h40.987    l33.333,100H344.471z M86,30c0-5.514,4.486-10,10-10h320c5.514,0,10,4.486,10,10v10c-9.522,0-330.404,0-340,0V30z M326,180v10    c0,16.542-13.458,30-30,30s-30-13.458-30-30v-10H326z M266,160V60h41.529l16.667,100H266z M187.805,160l16.667-100H246v100    H187.805z M246,180v10c0,16.542-13.458,30-30,30s-30-13.458-30-30v-10H246z M109.874,160l33.333-100h40.988l-16.667,100H109.874z     M166,180v10c0,16.542-13.458,30-30,30s-30-13.458-30-30v-10H166z M81.912,60h40.213L88.792,160h-61.88L81.912,60z M20,190v-10h66    v10c0,15.701-15.729,30-33,30c-4.354,0-8.866-0.945-13.066-2.742C28.011,212.187,20,201.232,20,190z M206,492H106v-86h100V492z     M206,386H106v-86h100V386z M466,492H226V290c0-5.522-4.478-10-10-10H96c-5.522,0-10,4.478-10,10v202H46V239.511    c2.318,0.315,4.653,0.489,7,0.489c13.161,0,26.465-5.214,36.498-14.306c2.219-2.01,4.217-4.16,6.01-6.413    C104.602,231.822,119.36,240,136,240c16.339,0,30.87-7.878,40-20.035C185.13,232.122,199.661,240,216,240s30.87-7.878,40-20.035    C265.13,232.122,279.661,240,296,240s30.87-7.878,40-20.035C345.13,232.122,359.661,240,376,240    c16.64,0,31.398-8.178,40.492-20.719c1.793,2.253,3.791,4.402,6.01,6.413C432.535,234.786,445.839,240,459,240    c2.342,0,4.677-0.168,7-0.485V492z M492,190c0,11.548-8.309,22.629-20.674,27.575c-4.044,1.61-8.19,2.425-12.326,2.425    c-17.271,0-33-14.299-33-30v-10h66V190z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M436,386h-10v-96c0-5.522-4.478-10-10-10H296c-5.522,0-10,4.478-10,10v96h-10c-5.522,0-10,4.478-10,10    c0,5.522,4.478,10,10,10h160c5.522,0,10-4.478,10-10C446,390.478,441.522,386,436,386z M406,386H306v-86h100V386z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M376,426h-80c-5.522,0-10,4.478-10,10c0,5.522,4.478,10,10,10h80c5.522,0,10-4.478,10-10C386,430.478,381.522,426,376,426    z"></path>
	</g>
</g>
</svg></button>
<button><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve" fill="white">
<g>
	<g>
		<path d="M299.359,266.002c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10c5.52,0,10-4.48,10-10    C309.359,270.482,304.878,266.002,299.359,266.002z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M239.359,123.002c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10c5.52,0,10-4.48,10-10    C249.359,127.482,244.878,123.002,239.359,123.002z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M411.646,178.251c-15.378-46.131-46.09-86.391-86.495-113.402c-9.031-29.961-31.399-53.916-59.541-63.301l-3.08-1.03    c-3.843-1.286-8.073-0.126-10.724,2.93c-2.652,3.057-3.201,7.411-1.39,11.03c3.857,7.706,6.463,16.506,7.643,25.681l-5.772,5.772    c-11.008,11.008-25.643,17.071-41.209,17.071h-11.72c-3.609,0-7.111,1.999-8.878,5.409c-0.021,0.04-0.046,0.076-0.066,0.116    l-7.062,14.114c-6.275,12.559-18.896,20.36-32.936,20.36c-4.406,0-8.801,0.511-13.056,1.517    c-8.673,2.046-13.957,5.405-16.584,6.598c-19.381,9.684-31.42,29.159-31.42,50.825c0,15.685,5.791,25.013,12.143,37.695    c6.706,13.215,20.078,21.425,34.897,21.425c6.105,0,11.983-1.392,17.477-4.138c15.345-7.682,34.263-8.317,50.859-0.054    l0.034,0.018c0.076,0.04,0.151,0.08,0.229,0.118c5.408,2.704,11.27,4.506,17.265,5.379c-11.195,7.753-22.887,13.305-34.44,16.195    c-50.817,12.705-83.713,66.415-64.521,123.862l6.57,19.72c1.36,4.084,5.183,6.839,9.487,6.839h10v23h-10    c-16.575,0-30,13.424-30,30c0,6.169,1.874,11.908,5.079,16.681C99.461,467.328,89.356,483.5,89.356,502c0,5.523,4.478,10,10,10    h280c5.522,0,10-4.477,10-10c0-18.401-9.914-34.583-25.049-43.333c3.284-4.893,5.049-10.645,5.049-16.667    c0-16.542-13.458-30-30-30h-10v-23h10.003v0.002c4.304,0,8.126-2.754,9.486-6.837l4.191-12.57    c2.502-7.507,4.764-15.412,6.757-23.592h39.565c4.767,0,8.87-3.364,9.806-8.038l9.341-46.683    C425.844,254.545,423.344,213.346,411.646,178.251z M367.656,492.002H111.073c4.127-11.641,15.249-20,28.286-20h200    C352.648,472.002,363.628,480.587,367.656,492.002z M339.359,432.002c5.513,0,10,4.485,10,10c0,5.521-4.478,10-10,10h-200    c-5.514,0-10-4.486-10-10c0-5.521,4.478-10,10-10H339.359z M169.359,412.002v-23c24.939,0,107.161,0,140,0v23H169.359z     M342.672,330.961c-1.074,1.835-1.542,3.939-1.317,6.09c-4.031,17.633-8.06,28.284-9.203,31.949h-12.793h-47.013    c15.475-10.639,28.137-29.405,33.95-50.424c1.473-5.323-1.649-10.832-6.972-12.304c-5.326-1.472-10.833,1.649-12.304,6.972    c-4.593,16.603-14.744,31.788-26.488,39.625L236.332,369c-13.237,0-78.514,0-89.764,0l-4.295-12.887    c-15.364-45.99,10.526-88.161,50.402-98.13c24.835-6.213,49.858-22.344,70.578-45.465c7.593-5.371,13.807-12.567,17.989-20.931    l7.06-14.11c2.471-4.939,0.471-10.946-4.469-13.417c-4.939-2.471-10.946-0.47-13.418,4.468l-7.061,14.112    c-9.04,18.076-31.053,25.582-49.306,16.532l-0.03-0.016c-0.074-0.04-0.149-0.078-0.224-0.116    c-22.078-11.051-47.68-10.609-68.868-0.002c-2.687,1.343-5.556,2.024-8.528,2.024c-7.246,0-13.784-4.014-17.039-10.429    l-0.182-0.363l23.343-7.781c5.239-1.747,8.071-7.41,6.325-12.649c-1.747-5.24-7.408-8.072-12.649-6.325l-25.432,8.477    c-4.745-16.717,2.718-34.872,18.972-42.994c2.86-1.319,6.306-3.619,12.224-5.015c2.754-0.651,5.6-0.981,8.458-0.981    c21.666,0,41.142-12.04,50.824-31.416l4.295-8.584h5.541c16.834,0,32.853-5.287,46.175-15.062    c-1.383,7.297-3.68,14.274-6.838,20.587c-2.471,4.939-0.471,10.946,4.469,13.417c4.939,2.471,10.946,0.471,13.418-4.468    c9.995-19.978,13.117-44.913,8.174-68.286c15.031,10.463,26.267,26.969,30.81,46.203c1.376,5.845,2.073,11.769,2.073,17.608    c0,1.075,0.173,2.143,0.514,3.163l24.189,72.569c9.864,29.593,15.297,64.137,15.297,97.268    C349.359,286.905,347.2,308.912,342.672,330.961z M398.893,287.359l-7.731,38.642h-27.179c0.45-2.531,0.883-5.068,1.278-7.609    c2.72-17.549,4.099-35.176,4.099-52.391c0-35.224-5.797-72.014-16.323-103.592l-23.01-69.032    c28.84,23.81,50.771,55.578,62.645,91.197C403.303,216.468,405.57,253.933,398.893,287.359z"></path>
	</g>
</g>
</svg></button>
<button><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve" fill="white">
<g>
	<g>
		<path d="M416,352c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10c5.52,0,10-4.48,10-10C426,356.48,421.52,352,416,352z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M256,352c-5.52,0-10,4.48-10,10c0,5.52,4.48,10,10,10s10-4.48,10-10C266,356.48,261.52,352,256,352z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M76,106c-5.52,0-10,4.48-10,10s4.48,10,10,10s10-4.48,10-10S81.52,106,76,106z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M454.743,301.362c-16.373-27.55-36.631-49.257-58.584-63.149c0.357-0.325,0.708-0.658,1.052-1.001    C402.879,231.543,406,224.01,406,216c0-3.904-0.758-7.633-2.121-11.057C416.61,201.473,426,189.815,426,176    c0-7.457-2.708-14.499-7.655-20.009C423.101,150.68,426,143.673,426,136c0-7.453-2.705-14.491-7.647-20    c4.942-5.509,7.647-12.547,7.647-20c0-16.542-13.458-30-30-30h-22.473l12.224-53.784c0.675-2.966-0.038-6.078-1.936-8.455    C381.918,1.384,379.042,0,376,0h-80c-3.042,0-5.918,1.385-7.815,3.762c-1.898,2.377-2.61,5.489-1.936,8.456l3.567,15.694    l-23.467,11.734c-10.798,5.399-20.602,12.465-29.139,21.003c-13.968,13.966-31.873,22.549-51.21,24.76V76c0-5.523-4.477-10-10-10    H36c-5.523,0-10,4.477-10,10v160c0,5.523,4.477,10,10,10h140c5.523,0,10-4.477,10-10v-10h3.68c16.385,0,32.578,2.627,48.125,7.806    c10.552,3.521,21.323,6.287,32.234,8.29c-19.715,13.911-37.862,34.161-52.781,59.266C197.685,334.296,186,371.918,186,402    c0,33.631,14.455,61.732,41.802,81.267C254.117,502.064,291.531,512,336,512s81.883-9.936,108.197-28.733    C471.545,463.732,486,435.631,486,402C486,371.917,474.315,334.296,454.743,301.362z M166,106h-50c-5.523,0-10,4.477-10,10    s4.477,10,10,10h50v100H46V86h120V106z M363.473,20l-10.455,46h-34.035l-10.454-46H363.473z M244.131,214.833    C226.537,208.972,208.217,206,189.68,206H186V105.534c24.69-2.282,47.601-12.993,65.352-30.743    c7.015-7.015,15.069-12.821,23.94-17.257l19.087-9.543L298.472,66H296c-5.522,0-10,4.477-10,10s4.478,10,10,10    c21.954,0,78.309,0,100,0c5.514,0,10,4.486,10,10c0,2.668-1.041,5.179-2.931,7.068c-1.89,1.891-4.401,2.932-7.069,2.932h-40    c-5.522,0-10,4.477-10,10s4.478,10,10,10h40c5.521,0,10,4.479,10,10c0,5.514-4.486,10-10,10h-40c-5.522,0-10,4.477-10,10    s4.478,10,10,10h40c5.521,0,10,4.479,10,10c0,5.514-4.486,10-10,10c-13.99,0-26.01,0-40,0c-5.522,0-10,4.477-10,10s4.478,10,10,10    h20c5.514,0,10,4.486,10,10c0,5.522-4.479,10-10,10h-63.08c-3.141,0-6.402-0.074-9.697-0.22    C283.115,224.89,263.236,221.208,244.131,214.833z M432.572,466.993C409.67,483.353,376.275,492,336,492    c-40.275,0-73.67-8.647-96.573-25.007C217.559,451.372,206,428.898,206,402c0-26.642,10.636-60.443,28.45-90.42    c19.44-32.71,44.446-55.995,70.53-65.731c2.687,0.09,5.354,0.151,7.939,0.151h54.503c25.94,9.825,50.788,33.038,70.128,65.58    C455.364,341.556,466,375.358,466,402C466,428.898,454.441,451.372,432.572,466.993z"></path>
	</g>
</g>
<g>
	<g>
		<path d="M341.178,353.875c-14.907-7.879-24.678-13.609-24.678-21.165c0-11.028,8.972-20,20-20s20,8.972,20,20    c0,5.523,4.478,10,10,10c5.522,0,10-4.477,10-10c0-18.604-12.767-34.282-30-38.734V282.71c0-5.523-4.478-10-10-10    c-5.522,0-10,4.477-10,10v11.266c-17.233,4.452-30,20.13-30,38.734c0,20.171,18.771,30.093,35.331,38.847    c14.901,7.877,24.669,13.604,24.669,21.153c0,11.028-8.972,20-20,20s-20-8.972-20-20c0-5.523-4.478-10-10-10    c-5.522,0-10,4.477-10,10c0,18.604,12.767,34.282,30,38.734v11.266c0,5.523,4.478,10,10,10c5.522,0,10-4.477,10-10v-11.266    c17.233-4.452,30-20.13,30-38.734C376.5,372.546,357.734,362.627,341.178,353.875z"></path>
	</g>
</g>
</svg></button>
<label class="label" for="checkbox">Click Me</label>
</div>
```
```scss
// @import "compass";

$d: 9em;

*,
*::before,
*::aftre {
  padding: 0;
  margin: 0;
}
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.popping-menu {
  position: relative;
  width: 10em;
  height: 10em;
  display: flex;
  justify-content: center;
  align-items: center;
  button {
    position: absolute;
    display: block;
    width: 4em;
    height: 4em;
    padding: 0 1em;
    appearance: none;
    background: #FFB66F;
    border: none;
    transition: all 0.3s ease-in-out;
    transform: translate(0, 0) rotate(360deg);
    opacity: 0;
    border-radius: 50%;
    color: white;
  }  
}
.popping-menu {
  .checkbox {
    display: none;
  }
  .checkbox:checked {
    ~ button {
      @import "compass";

      $per: 180 / 4;
      @for $i from 1 through 6 {
        &:nth-of-type(#{$i}) {
          $angle: $per * ($i - 1) * 1deg + 180deg;
          $x: cos($angle) * $d;
          $y: sin($angle) * $d;
          opacity: 1;
          transition-delay: 0.1s * $i;
          transform: translate($x, $y) rotate(0deg) ;
        }
      }
    }
  }
}

.popping-menu {
  .label {
    z-index: 10;
    border-radius: 50%;
    background: #4791FF;
    width: 6em;
    height: 6em;
    line-height: 6em;
    text-align: center;
    display: block;
    color: white;
    cursor: pointer;
    user-select: none;
  }
}
```