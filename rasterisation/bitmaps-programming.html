<!DOCTYPE html>
<html>
	<head>
		<link rel="stylesheet" type="text/css" href="../styles/style.css"/>
		<link rel="icon" type="image/png" href="../favicon.png"/>
		<title>Programming Bitmaps</title>
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
				<h1>Programming Bitmaps</h1>
				<div class="note">
					<p>I planned to initally create a programming section in every article, but I have decided that it could impede learning and more effort could be put into making the articles better. Here is the only programming article, maybe it will help you :)</p>
				</div>
				<div class="warning">
					<p>The content on this page is incomplete and has not been proofread for accuracy. Please report any issues you notice on the <a href="https://github.com/knot126/Knowledgebase/issues">GitHub issues page</a>.</p>
				</div>
				<p>Let us start programming now! You can probably stop reading here and do it yourself, but I will provide a description of what I would do in a C-like (mid-level) language.</p>
				<h2>Programming!</h2>
				<p>First, I would create a record to represent our pixels and hold our bitmap data:</p>
				<pre><b>record</b> <span class="blue">pixel_t</span> {
	<span class="blue">uint8_t</span> r, g, b, a;
}

<b>record</b> <span class="blue">bitmap_t</span> {
	<span class="blue">int32_t</span> width, height;
	<span class="blue">pixel_t</span> *data;
}</pre>
				<p>You could just use plain <code>uint8_t</code>s or <code>uint32_t</code> with bitwise ops for the pixels, but I find its easier to manage when its in a structure. Plus, it should not add any overhead.</p>
				<p>Now, I will lay out the defitions of the functions that we will use — there are not that many for a basic bitmap object:</p>
				<pre>
<span class="blue">errorcode_t</span> <span class="purple">bitmap_init</span>(<span class="blue">bitmap_t</span> *<b>this</b>, <span class="blue">uint32_t</span> width, <span class="blue">uint32_t</span> height);
<span class="blue">void</span> <span class="purple">bitmap_free</span>(<span class="blue">bitmap_t</span> *<b>this</b>);
<span class="blue">pixel_t</span> <span class="purple">bitmap_get_pixel</span>(<span class="blue">bitmap_t</span> *<b>this</b>, <span class="blue">uint32_t</span> x, <span class="blue">uint32_t</span> y);
<span class="blue">void</span> <span class="purple">bitmap_set_pixel</span>(<span class="blue">bitmap_t</span> *<b>this</b>, <span class="blue">uint32_t</span> x, <span class="blue">uint32_t</span> y, <span class="blue">pixel_t</span> colour);</pre>
				<p>We can almost immidately implement them, but first we will want to figure out how to get from the \(x\) and \(y\) coordinate to an index in the array.</p>
				<p>Most of the time, we will have \(x\) going left to right and \(y\) from top to bottom, storing the image y-major and x-minor. That is what we will do here.</p>
				<p class="image">
					<img src="vectors/drawing-6.svg" width="200" height="200"/>
				</p>
				<p>To access a pixel in any row, we can just say that it is located at \(\text{OffsetToRow} + x\), where \(x\) is the x-coordinate.</p>
				<p class="image">
					<img src="vectors/drawing-7.svg" width="200" height="200"/>
				</p>
				<p>To get the start of the \((y + 1)\)th row, and therefore \(\text{OffsetToRow}\), we can find \(y \cdot \text{Width}\), the start of row \(y\).</p>
				<p class="image">
					<img src="vectors/drawing-8.svg" width="200" height="200"/>
				</p>
				<p>Finally, we can plug this back together to find that the offset for any pixel is \(y \cdot \text{Width} + x\). We can then just implement this directly:</p>
				<pre><b>let</b> <span class="pink">bitmap_pixel_index</span>(x, y, width) = y * width + x;</pre>
				<p>Now we can start to implement <code>bitmap_init</code>, which is mostly language-specific:</p>
				<pre><span class="blue">errorcode_t</span> <span class="purple">bitmap_init</span>(<span class="blue">bitmap_t</span> *<b>this</b>, <span class="blue">uint32_t</span> width, <span class="blue">uint32_t</span> height) {
	<span class="purple">fill_zero</span>(<b>this</b>, sizeof *this);
	
	<b>this</b>->width = width;
	<b>this</b>->height = height;
	<b>this</b>->data = <span class="purple">allocate</span>(<b>sizeof</b> *<b>this</b>->data * width * height);
	
	<b>if</b> (<b>this</b>->data == <span class="blue"><b>null</b></span>) {
		return <span class="green">errorcode.failure</span>;
	}
	
	<b>return</b> <span class="green">errorcode.success</span>;
}</pre>
				<p>As well as <code>bitmap_free</code>:</p>
				<pre><span class="blue">void</span> <span class="purple">bitmap_init</span>(<span class="blue">bitmap_t</span> *<b>this</b>) {
	<span class="purple">free</span>(<b>this</b>->data);
}</pre>
				<p>Then we can implement getting a pixel, which we will do by calculating the index then returning the pixel value:</p>
				<pre><span class="blue">pixel_t</span> <span class="purple">bitmap_get_pixel</span>(<span class="blue">bitmap_t</span> *<b>this</b>, <span class="blue">uint32_t</span> x, <span class="blue">uint32_t</span> y) {
	<b>return</b> this->data[<span class="pink">bitmap_pixel_index</span>(x, y, <b>this</b>->width)];
}</pre>
				<p>It might seem like we would implement getting a pixel similarly, but we do need to remember there is an alpha channel:</p>
				<!-- FINISH THIS!!! -->
			</div>
			<div class="topbar"><p>The contents of this website are licensed under the <a rel="license" href="http://creativecommons.org/publicdomain/zero/1.0/">Cerative Commons Zero</a> (public domain) licence unless otherwise noted.</p></div>
		</div>
	</body>
</html>
