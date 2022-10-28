== TODO: Categories legend and highlight ==
TODO: so make this interactive

TODO: add a legend for
* Chemicals & processes
* Power system
* Aviation & shipping
* Land transportation
* Heating
that when rolled over fills in the appropriate rects
??? Where to fit this in?

So give each rounded-rectangle instance a class
chemicals-processes (I don't think '+' is legal in CSS class)
power_system
aviation-shipping
land_transportation
heating

And on rollover of each one,
 * add style category-highlighted to everything with the same class, e.g. chemicals-processes

I don't think I can use :hover CSS pseudoselector to change everything that shares the class,
it only affects what you're hovering over.

Then have CSS saying for style category-highlighted
* In category_legend, style the text of the item with that class bold
* In each row, style the fill color of every item with that class to match the row.
  - TODO: this would be easiest if they were within a group with class .rowA_items
  - for now I have an explicit "rowA", "rowB", etc. clss on several of the items.
  - TODO: it's actually the path within the item with the class, i.e. .rowA > .path
  - this is sort-of wrong since there are two paths in each rounded rect item.
  - TODO: this is probably easier if every item in the row is within a group with ID "row-A", "row-B", etc.
- TODO: rename "row" -> something less geometric like...??? "level" "suitability", or "rating"

TODO: decide whether to leap to Inkscape version
	* adds id for everything
	* > in style block becomes &gt;
	* nearly every attribute indented 2 spaces
    * all colors change from rgb to hex, e.g.  stroke="rgb(118,84,163)" ->   stroke="#7654a3"
  - TODO: find an XML differ that can handle or reformat its attribute whitespace
    git diff --ignore-space-change is pretty good
  - maybe have one commit where I edit in Inkscape and save but no other changes
    - then ungroup and remove mask
    - then organize each rows items into a groupchange

TODO: the original SVG has two paths for each rounded rect, one setting the fill and one setting the stroke. Why not just one path that sets both?
TODO: check if Impress exports a rounded rect with separate fill and stroke paths.
BUG: is this a PPTX import bug or a bug in how Impress exports a rounded rect with a fill and stroke?

TODO: instead of a function adding an onmouseenter handler, actually add one to each item.
TODO: see if Inkscape leaves this alone or even presents it as an object property.


==== Category/arrow colors for each row of the ladder ====
When highlighting items in a category like "chemicals & processes", the items take the same fill color as the arrow for that row.

The CSS colors for each row/rating https://www.w3schools.com/colors/colors_converter.asp to convert these colors to rgb()
A: #1fa550
B: #54b149 rgb(84, 177, 73)
C: #bcd033
D: #f5e925
E: #f9b61f
F: #ef7127
G: #e61a26

=== TODO: set cursor on hover items (?) ===
could add cursor="pointer" to them.


== TODO: Competing Technologies legend and highlight ==
TODO: Copy from Slide #9 (hydrogen_ladder_competing_technologies.svg) the grouping:
"Key:
* No real alternative
* Electricity/batteries
* Biomass/biogas
* Other
with grouping "competing_legend"
Probably change "Key" to "Competing Technologies"
And each g inside here has a class
* alternative-none, alternative-elec_battery, alternative-biomass_biogas, alternative_other and alternative-ammonia
Add these classes to every g id

upon rollover of the competing_legend group (anywhere), change items with these classes to add style "competing-highlight", which is a nested selector to make some items green border, etc.
and 
=== TODO: get rounded rect stroke and fill colors for these from slide #9
=== TODO: asterisk reveal in competition ? ===
Also the trick of within "Biomass/biogas", the items 'Shipping", Long-haul aviation, Vintage vehicles, and "Medium-haul aviation" all get an asterisk and the slide shows the footnote.
     * Most likely via ammonia or e-fuel rather than H2 gas or liquid.

== TODO: Arial font ==
TODO: need to embed Arial (? or rely on fc-match). Supposedly https://vecta.io/nano will do this, according to their own https://vecta.io/blog/how-to-use-fonts-in-svg . Or could try to do it ourselves , see https://lvngd.com/blog/how-embed-google-font-svg/


== TODO: Terms and conditions ==
TODO: note Terms & Conditions on last slide #11.
	>>>>
	The Clean Hydrogen Ladder is the copyright of Michael Liebreich/Liebreich Associates Limited. We are releasing these charts (but not any accompanying article or presentation) under the terms of a Creative Commons Attribution 3.0 Unported License (CC-BY 3.0), which means that you are free to reproduce, use or modify these charts. If you make modifications, you must indicate which part or parts you have changed, not pass off the resulting ladder as the work of Michael Liebreich/Liebreich Associates Limited. Please include a credit on each page or image in the following format (including the links):
		Source: Michael Liebreich/Liebreich Associates, Clean Hydrogen Ladder, Version 4.1, 2021.
Concept credit: Adrian Hiel, Energy Cities. As modified by skierpage. CC-BY 3.0
	<<<<

TODO: I could add a (c) symbol that pops this up.

TODO: need to add a LICENSE with CC-BY 3.0 to project (different because it's not my copyright?)
TODO: should I change T&C text in SVG to add "as modified by skierpage."

== Bugs ==
TODO: BUG: If I import the SVG back into LibreOffice (Impress opens), the underlined text in the T&C doesn't appear (check with the original export)
TODO: BUG: If I insert the SVG into a LibreOffice Draw document, only the master slide graphics appear, not the stuff on the slide (check with the original export)

TODO: BUG: LibreOffice SVG export fails validation
hydrogen_uses_ladder.svg is valid XML, but 
https://validator.w3.org/check complains

*  Error Line 21, Column 133: end tag for "font-face" which is not finished 
   <font-face font-family="Arial embedded" units-per-em="2048" font-weight="normal" font-style="normal" ascent="1852" descent="423"/>
This suggests it wants to have some child element.

== Cleanup ==
The main content is nestead g1234 > g1232 > container-id1 > id1 (which has a clip path) > g1228. Could remove most or all of these.

Remove all the ooo: attributes

Remove the <defs> section that names slide elements and is out-of-date and probably useless.

== DONE: Summary so far ==
"The Clean Hydrogen Ladder (now up to v4.1)" could be a single interactive SVG.
I mentioned this in a reply to https://www.linkedin.com/pulse/clean-hydrogen-ladder-v40-michael-liebreich/
and Michael Liebrich provided a link to the presentation https://docs.google.com/presentation/d/1zDt5TxqacweNLh_tY1KwHXT4VW-CNnSL/edit#slide=id.p3

From the slide master this is "Clean Hydrogen Use Case Ladder – Version 4.1a" of 9 September 2021 by @mliebreich

BUG: fonts look weird in Google Docs, and doesn't render right.

Download the pptx, open in LibreOffice Impress. Looks good.

Copy C:\Windows\Fonts\Arial, put the main arial.ttf file in ~/.fonts

Slide 3 is the key.
So Export as SVG. No option to choose a slide (!!?),

TODO: In a browser with JS disabled (easiest to do in Konqueror), the items in the ladder layer of the edited SVG don't appear. I could go through and remove all the 'visibility: "hidden"' attributes, or set them to 'visibility: "visible"'. But maybe if I reverted to an earlier version, fixed the visibility of class="SlideGroup", then ungrouped in Inkscape, I would fix it once and for all. 
^^^^ did I do this?

== Cleanup ==
Removed overall group
Removed dummy-master-page group for class Master_Slide and its Background and BackgroundObjects
Removed bg-id2 class Background (filled with white, but it seems white anyway).
Kept bo-id ("BackgroundObjects" group

Saved this iteration of hydrogen_uses_ladder.svg

Next in Inkscape only: remove g1232 group (ungroup?), remove (ungroup) container-id1, then release object id1 from its clip_path (in the file as #presenataion_clip_path).
The clip_path became black rect3002 (not present before) which I deleted.

Now I'm down to g id1 class "Slide", a group of 1. ungroup that to give g id "g1228" class "Page", ooo:name "Clean_Hydrogen_Ladder"
Ungroup that and I have all the items on the slide.

Select the top row of rects, group them, give the group the ID "g_rowA".

later removed the dummy-slide and dummy-master-page groups

=== Fixed the LibreOffice export ===
To get the Liebrich badge and footer text to appear I had to edit the SVG to comment out the opening and closing defs tag around the Slide Master components, and then deleted the `<script>` tag.
I filed Inkscape bug https://gitlab.com/inkscape/inbox/-/issues/6566

