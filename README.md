"The Clean Hydrogen Ladder (now up to v4.1)" could be a single interactive SVG.
I mentioned this in a reply to https://www.linkedin.com/pulse/clean-hydrogen-ladder-v40-michael-liebreich/

and Michael Liebrich provided a link to the presentation https://docs.google.com/presentation/d/1zDt5TxqacweNLh_tY1KwHXT4VW-CNnSL/edit#slide=id.p3

From the slide master this is "Clean Hydrogen Use Case Ladder – Version 4.1a" of 9 September 2021 by @mliebreich

BUG: fonts look weird in Google Docs, and doesn't render right.

Download the pptx, open in LibreOffice Impress. Looks good.

Copy C:\Windows\Fonts\Arial, put the main arial.ttf file in ~/.fonts

Slide 3 is the key.
So Export as SVG. No option to choose a slide (!!?),

To get the Liebrich badge and footer text to appear I had to edit the SVG to comment out the opening and closing defs tag around the Slide Master components, and then deleted the `<script>` tag.
I filed Inkscape bug https://gitlab.com/inkscape/inbox/-/issues/6566

TODO: In a browser with JS disabled (easiest to do in Konqueror), the items in the ladder layer of the edited SVG don't appear. I could go through and remove all the 'visibility: "hidden"' attributes, or set them to 'visibility: "visible"'. But maybe if I reverted to an earlier version, fixed the visibility of class="SlideGroup", then ungrouped in Inkscape, I would fix it once and for all. 

TODO: so make this interactive, add a legend for
* Chemicals & processes
* Aviation & shipping
* etc.
that when rolled over fills in the appropriate rects

TODO: note Terms & Conditions on last slide #11.
	>>>>
	The Clean Hydrogen Ladder is the copyright of Michael Liebreich/Liebreich Associates Limited. We are releasing these charts (but not any accompanying article or presentation) under the terms of a Creative Commons Attribution 3.0 Unported License (CC-BY 3.0), which means that you are free to reproduce, use or modify these charts. If you make modifications, you must indicate which part or parts you have changed, not pass off the resulting ladder as the work of Michael Liebreich/Liebreich Associates Limited. Please include a credit on each page or image in the following format (including the links):
		Source: Michael Liebreich/Liebreich Associates, Clean Hydrogen Ladder, Version 4.1, 2021.
Concept credit: Adrian Hiel, Energy Cities. As modified by skierpage. CC-BY 3.0
	<<<<

TODO: need to add a LICENSE with CC-BY 3.0 (different because it's not my copyright?)
TODO: Need to change T&C text in SVG to add "as modified by skierpage."

TODO: need to embed Arial (? or rely on fc-match). Supposedly https://vecta.io/nano will do this, according to their own https://vecta.io/blog/how-to-use-fonts-in-svg . Or could try to do it ourselves , see https://lvngd.com/blog/how-embed-google-font-svg/
