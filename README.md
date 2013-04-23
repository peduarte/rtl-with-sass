#Simple RTL Stylesheet with CSS
###A simple and powerful way to generate RTL Stysheet with SASS.

Once I had to convert a already built e-Commerce (Magento) site to Arabic. It took me 3 months modifying just the stylesheet, and it was probably the most annoying thing I've ever had to do.<br><br>
Recently I worked on a different website, but I got to do it from scratch, so I decided to use SASS, which I now do for pretty much every project, and this site also needed an Arabic version. That's when I decided to use the power of SASS to make my life easier, and this is the solution I used:

###all.scss
	@import '_utils';
	@import '_global';

###rtl.scss
	// This overrides our default value of $dir
	$dir: right;
	
	// This overrides our default value of $opDir
	$opDir: left;
	
	@import 'all';
	
	body {
		direction: rtl;
	}

###_utils.scss
	// This sets our default direction
	$dir: left !default;
	
	// This sets our opposite default direction
	$opDir: right !default;
	
	
	@function invertValues($top, $right, $bottom, $left: $right) {
	    @if $left == true {
	        @if $dir == right {
	            @return $top $left $bottom $right;
	        }
	    }
	    @else {
	        @return $top $right $bottom $left;
	    }
	}

###_global.scss
	// Sample usage example
	body {
		text-align: $dir;
	}
	
	// If you need to use the variable in the property...
	header {
		position: absolute;
		#{$dir}: 100px; // equivalent of 'left: 100px;' or 'right: 100px;'
	}
	
	// Another example
	.offset {
		margin-#{$opDir}: -100px;
	}
	
####I also built a [demo](http://pedroduarte.me/rtl-with-sass) page where you can see it in action.

Feel free to change this as it suits you best, there might well be a better solution out there.