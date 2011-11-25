#Headings.less

######STYLING YOUR CAPTIONS WITH RHYTHM

##Description

The **Fibonacci sequence** is used _conveniently_ to calculate the heading tags sizes. This sets the `font-size` CSS property and it´s powered by the amazing [Less CSS](http://lesscss.org/).

The sequence 1, 1, 2, 3, 5, 8, 13... it´s used like percentages, ignoring the first "1" and assuming the base size is the next "1" or a 100%.

##The Mixins

Headings.less provide you four different creative ways to use the fibbonacci sequence. Two are what I call **successions** and the other two are what I call **base** sequences, both have an ASCending and DESCending version.

The `.successionDESC` and `.successionASC` mixins are calculated as follows:

###.successionDESC

.successionDESC() takes the @headings-max-size variable or the passed value and apply it to the h1 tag. Then, the next sizes are calculated substracting the percentage in the sequence from the preceding heading size (20%, 30%, 50%, 80%, 13%). This is achieved dividing e.g.:

    h1 = ( @headings-max-size / 1 )
    h2 = ( h1 / 1.2 )
    h3 = ( h2 / 1.3 )
    .
    .
    .
    h6 = ( h5 / 1.13 )


###.successionDESC
.successionASC() is pretty the same, but go from h6 to h1 and the @headings-min-size or passed value it´s applied to h6, instead of substracting, now we add. This is achieved multiplying e.g.:

    h6 = ( @headings-min-size * 1 )
    h5 = ( h1 * 1.2 )
    h4 = ( h2 * 1.3 )
    .
    .
    .
    h1 = ( h5 * 2.3 )

<small>**Notice** that the last operation for h1 has a 2.3 multiplier, this is because if we multiply h2 by 1.13 we will have a pretty similar result, therefore, this is not good in terms of design and visual perception, we must look for a good contrast. The logic behind that 2.3 is that if we got a "13" in the sequence, deliberately I take it as 1.3 or as 130% and then I add an extra 100% for the contrast we want, so, this results in 230% or 2.3 ( I know this looks like a magic trick out of the sleeve, but take this as optical adjustments ;)</small>

---

The `.baseDESC` and `.baseASC` works in the same way but the operations are all applied to the base font size, e.g.:

###.baseDESC

For descending order:

    h1 = ( @headings-max-size / 1 )
    h2 = ( @headings-max-size / 1.2 )
    h3 = ( @headings-max-size / 1.3 )
    .
    .
    .


###.baseASC

For ascending order

    h6 = ( @headings-min-size * 1 )
    h5 = ( @headings-min-size * 1.2 )
    h4 = ( @headings-min-size * 1.3 )
    .
    .
    .

---

##Configuration

At the top of the headings.less file you could setup the next things:

###Variables

`@headings-max-size` & `@headings-min-size`:

Default max & min size for headings (h1 & h6 respectively depending on the mixin used).
The unit lengths will be overwritten by the **@headings-units** var, so be careful.

**Defaults:** 48 & 12 respectively (for px units).

---

`@headings-decimals`:

The desired decimal digits, set to 0 to get integers. Must be greater or equal to zero.

**Default:** 3.

---

`@headings-units`:

The unit lenghts used: (px, em, ex, pt, pc, in, cm, mm, %). This must have a value.
In case you choose `%`, set the value like this: `~'%'`.

Be aware that you are using the units and the max/min values correctly. This is because it´s not the same using pixels or picas or whatever. More insight at http://www.w3.org/TR/CSS2/syndata.html#length-units and http://pxtoem.com/

**Default:** px

---

###Configuration Bundle

The `#headings-config` bundle has some mixins to customize **global** heading styles and the **specific** ones. You just have to write the normal CSS code to be applied inside the mixins brackets.

This bundle looks like this and it's self explanatory:

    #headings-config {

    	//Write here the h1-h6 common styles,
        //leave blank if you don´t want that styling output
    	.common-styles() { }

    	//Write here the specific heading styles,
        //leave blank if you don't want additional styling
    	.h1() {  }
    	.h2() {  }
    	.h3() {  }
    	.h4() {  }
    	.h5() {  }
    	.h6() {  }
    }

---

##Usage

To use this in your projects you have to follow 3 simple steps after downloading or forking headings.less.

###1. Configure

Open the **headings.less** file and edit your custom preferences. e.g.:

	@headings-max-size: 72;
	@headings-min-size: 10;
	@headings-decimals: 2;
	@headings-units: px

	#headings-config {

		//Write here the h1-h6 common styles,
		//leave blank if you don´t want that styling output
		.common-styles() { 
                    font-weight: normal;
                    margin: .5em 0;
                    color: #3b3b3b;
                }

		//Write here the specific heading styles,
		//leave blank if you don't want additional styling
		.h1() {
                    //Let´s add some color for this tag
                    color: #c90000;
                }
		.h2() {  }
		.h3() {  }
		.h4() {  }
		.h5() {  }
		.h6() {
                    //We add special styles for h6,
                    //normally this tag ends with a small font-size
                    font-weight: bold;
                    letter-spacing: .618em;
                    word-spacing: .038em;
                    text-transform: uppercase;
                }
	}


###2. Import

Just import the file within your main less file. e.g.:

In your **main.less**

`@import "headings.less"`

By default the headings.less doesn't output nothing but a CSS comment block with a legal disclaimer. See the LICENCE file for more info.

###3.Run the mixins

You could do this just writing the next Less CSS code (see http://lesscss.org for more info if you are new to Less):

    #headings > .init();
    #headings > .successionDESC();

Or you could wrap the h1-h6 tags in a parent CSS selector like this:

    article {
       #headings > .init();
       #headings > .successionDESC();
    }

Have fun!
