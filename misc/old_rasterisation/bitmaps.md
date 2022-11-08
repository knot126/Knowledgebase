<!DOCTYPE html>
<html>
	<head>
		<link rel="stylesheet" type="text/css" href="../styles/style.css"/>
		<link rel="icon" type="image/png" href="../favicon.png"/>
		<title>Bitmaps</title>
		<meta charset="utf-8"/>
		<meta name="keywords" content="bitmap, computer graphics, raster"/>
		<!-- KaTeX include -->
		<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/katex.min.css" integrity="sha384-KiWOvVjnN8qwAZbuQyWDIbfCLFhLXNETzBQjA/92pIowpC0d2O3nppDGQVgwd2nB" crossorigin="anonymous">
		<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/katex.min.js" integrity="sha384-0fdwu/T/EQMsQlrHCCHoH10pkPLlKA1jL5dFyUOvB3lfeT2540/2g6YgSi2BL14p" crossorigin="anonymous"></script>
		<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/contrib/auto-render.min.js" integrity="sha384-+XBljXPPiv+OzfbB3cVmLHf4hdUFHlWNZN5spNQ7rmHTXpd7WvJum6fIACpNNfIR" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
		<!-- KaTeX include -->
	</head>
	<body>
		<div id="main" class="main">
			<div class="topbar"><a href="../index.html">Knot126's Knowlegebase</a></div>
			<div id="main-content" class="content">
				<h1>Bitmaps</h1>
				<div class="warning">
					<p>The content on this page is incomplete and has not been proofread for accuracy. Please report any issues you notice on the <a href="https://github.com/knot126/Knowledgebase/issues">GitHub issues page</a>.</p>
				</div>
				<p>Bitmaps — or more generally raster graphics — store an image as a grid of colours. This can then be sent directly to the screen, which is a grid of lights, called pixels, that change colour based on the values in the bitmap.</p>
				<p>In other words, we are mapping the bits in the image to the pixels on the screen.</p>
				<p>Let us start simple. Take this grid of numbers, where \(1\) means the cell is lit (white) and \(0\) means the cell is off (black): $$\begin{bmatrix} 0 & 1 & 0 & 0 \\ 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 1 & 1 & 1 \end{bmatrix}$$</p>
				<p>Which makes this image:</p>
				<p class="image">
					<img src="vectors/drawing-1.svg" width="200" height="200"/>
				</p>
				<p>What if we want to add more than one colour? There are a few ways to do this. The most obvious method is to add new numbers and assign them directly to colours. Let's make the following mapping: $$\text{Off} = 0 \\ \text{Red} = 1 \\ \text{Green} = 2 \\ \text{Blue} = 3 \\ \text{Yellow} = 4 \\ \text{Purple} = 5 \\ \text{Grey} = 6 \\ \text{Full on} = 7$$</p>
				<p>... find an example ... $$\begin{bmatrix} 0 & 1 & 0 & 0 \\ 0 & 2 & 2 & 2 \\ 0 & 4 & 0 & 4 \\ 0 & 5 & 5 & 5 \end{bmatrix}$$</p>
				<p>... and visualise!</p>
				<p class="image">
					<img src="vectors/drawing-2.svg" width="200" height="200"/>
				</p>
				<p>But now, an issue: your screen can display <i>16 million</i> colours. And no one is crazy enough to assign 16 million colours in a way that is sane. So, what should we do?</p>
				<p>We can use the properties of light to help. Roughly speaking, in light, you only need red, green and blue lights and a way to control their intensitity in order to make any other colour of light.</p>
				<p class="image">
					<img src="vectors/drawing-3.svg" width="400" height="400"/>
				</p>
				<p>So, we just need to store the intensity of red, green and blue per pixel.</p>
				<p>A good way to store this is by using integers in the range \([0, 255]\), where \(0\) is fully off and \(255\) is completely on, since these are the extreme values of an unsigned byte.</p>
				<p>We can use three unsigned bytes for each pixel to store the red, green and blue channels; let's denote them using \((r, g, b)\) and create an example of this: $$ \begin{bmatrix} (0, 127, 255) & (0, 127, 255) & (0, 127, 255) & (0, 127, 255) \\ (255, 128, 0) & (255, 128, 0) & (255, 128, 0) & (255, 128, 0) \\ (63, 127, 127) & (63, 127, 127) & (63, 127, 127) & (63, 127, 127) \\ (255, 0, 0) & (0, 255, 0) & (0, 0, 255) & (255, 255, 255) \end{bmatrix} $$</p>
				<p>That gives us this bitmap:</p>
				<p class="image">
					<img src="vectors/drawing-4.svg" width="200" height="200"/>
				</p>
				<div class="note">
					<p><b>Note</b>: The following section about alpha channels needs more info about alpha blending.</p>
				</div>
				<p>There is one last thing we might want to add: some way to store the transluscentcy (see-through-ness) of a pixel so that we can see other things thorugh our image if we put it on top of another.</p>
				<p>Usually, we add another channel (number) for each pixel that denotes its transluscentcy.</p>
				<p>And conventionally, that channel is called "alpha" (for the greek letter \(\alpha\)) where \(255\) is usually opaque and \(0\) is transparent.</p>
				<p>When we begin to combine pixels with alpha channels, we will fade (or interpolate) between the two pixel values using the alpha channel.</p>
				<p>There are many ways to do alpha blending, some being more realistic than others. (EDITOR NOTE write more about this...)</p>
				<p>Let's see an examaple where we have \((r, g, b, \alpha)\)! $$ \begin{bmatrix} (0, 127, 255, 255) & (0, 127, 255, 170) & (0, 127, 255, 85) & (0, 127, 255, 0) \\ (255, 128, 0, 255) & (255, 128, 0, 170) & (255, 128, 0, 85) & (255, 128, 0, 0) \\ (63, 127, 127, 255) & (63, 127, 127, 170) & (63, 127, 127, 85) & (63, 127, 127, 0) \\ (255, 0, 0, 255) & (0, 255, 0, 255) & (0, 0, 255, 255) & (255, 255, 255, 0) \end{bmatrix} $$</p>
				<p>The final image:</p>
				<p class="image">
					<img src="vectors/drawing-5.svg" width="200" height="200" style="background: #fff;"/>
				</p>
				<p>Now see that if we change the background, the total colour changes with any pixel that isn't opqaue and transluscent pixels blend together with the background.</p>
				<p class="image">
					<img src="vectors/drawing-5.svg" width="200" height="200" style="background: #000;"/>
					<img src="vectors/drawing-5.svg" width="200" height="200" style="background: #8d7;"/>
					<img src="vectors/drawing-5.svg" width="200" height="200" style="background: #a89;"/>
				</p>
			</div>
			<div class="topbar"><p>The contents of this website are licensed under the <a rel="license" href="http://creativecommons.org/publicdomain/zero/1.0/">Cerative Commons Zero</a> (public domain) licence unless otherwise noted.</p></div>
		</div>
	</body>
</html>
