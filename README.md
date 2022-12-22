The infamous "Clean Hydrogen Ladder (now up to v4.1)" figure by Michael Liebreich/Liebreich Associates
that shows up in response to any overhyped article about The Hydrogen Economy™
comes from a slide deck that goes on to categorize uses of hydrogen from Unavoidable to Uncompetitive.
I turned these slides into a single interactive SVG, a resizable vector image whose text they can search and copy.

image links like these aren't interactive, and clicking on them goes to "camo.githubusercontent.com"
![Test GitHub Pages link here](https://skierpage.github.io/hydrogen_ladder_svg/hydrogen_uses_ladder.svg)
![Test raw here](https://raw.githubusercontent.com/skierpage/hydrogen_ladder_svg/main/hydrogen_uses_ladder.svg)

*Note:* GitHub, and other sites, strip the `<script>` tag contents when it presents the SVG, for security reasons.
You can interact with the SVG [here](https://skierpage.github.io/hydrogen_ladder_svg/hydrogen_uses_ladder.svg).

## History
I mentioned this idea in a reply to https://www.linkedin.com/pulse/clean-hydrogen-ladder-v40-michael-liebreich/
and Michael Liebrich provided a link to his presentation.

From the slide master this is "Clean Hydrogen Use Case Ladder – Version 4.1a" of 9 September 2021 by @mliebreich

BUG: font looks weird in Google Docs, and dosn't render right, maybe because I didn't have Arial?

Download the pptx, open in LibreOffice Impress. Looks good.

Copy C:\Windows\Fonts\Arial, put the main arial.ttf file in ~/.fonts

Slide 3 is the key, so Export as SVG. No option in LibreOffice to choose a slide (!!?),

Then start editing the svg text, cleaning it up and adding interactivity.

## Interactivity

(see the `<script>` block in the SVG).

Give each rounded-rectangle instance a class, and on rollover of each one
* add CSS class `highlighted` to everything with the same class, e.g. chemicals-processes
  - I don't think I can use :hover CSS pseudoselector to change everything that shares the class,
it only affects what you're hovering over.

Then have CSS saying for style category-highlighted
* Set CSS `category_set .highlight` fill color to blue.
* Set CSS for `.rowX.highlight path` fill color to the row's arrow color.
  - this is sort-of wrong since there are two paths in each rounded rect item.
  - TODO: this is probably easier if every item in the row is within a group with ID "row-A", "row-B", etc.
- TODO: rename "row" -> something less geometric like...??? "level" "suitability", or "rating"


## TODOs
(TODO: move these to Issues :wink: )

- set cursor on hover items (?)
  - could add cursor="pointer" to them.

- why doesn't mouseenter/mouseleave work? Unclear if it ever fires. Maybe it will if I remove the main content nesting in **Cleanup**.
- instead of a function adding `onclick` and `onmouseenter` handlers, actually add one to each item in the SVG.
  - see if Inkscape leaves this alone or even presents it as an object property.

- decide whether to leap to Inkscape version
	* adds id for everything
	* > in style block becomes &gt;
	* nearly every attribute indented 2 spaces
    * all colors change from rgb to hex, e.g.  stroke="rgb(118,84,163)" ->   stroke="#7654a3"
  - TODO: find an XML differ that can handle or reformat its attribute whitespace
    git diff --ignore-space-change is pretty good
  - maybe have one commit where I edit in Inkscape and save but no other changes
    - then ungroup and remove mask
    - then organize each rows items into a groupchange

### TODO: Competing Technologies legend and highlight
Copy from Slide #9 (hydrogen_ladder_competing_technologies.svg) - grouping:
"Key:
* No real alternative
* Electricity/batteries
* Biomass/biogas
* Other
with grouping "competing_legend"
Probably change "Key" to "Competing Technologies"
And each g inside here has a class
* alternative-none, alternative-elec_battery, alternative-biomass_biogas, alternative_other and alternative-ammonia
* Add these classes to every g id
* upon click/rollover of the competing_legend group (anywhere),
 * call unHilight, then change items with these classes to add style "competing-highlight", which is a nested selector to make some items green border, etc.
* rename unHilightCat to unHighlight, update it to also remove this competing-highlight

- TODO: get rounded rect stroke and fill colors for these from slide #9

### TODO: asterisk reveal in competition ?
Also the trick of within "Biomass/biogas", the items 'Shipping", Long-haul aviation, Vintage vehicles, and "Medium-haul aviation" all get an asterisk and the slide shows the footnote.
     * Most likely via ammonia or e-fuel rather than H2 gas or liquid.

### TODO: Arial font
- Does the `<defs>` that includes font id=EmbeddedFont_1 that defines "Arial embedded" work?
- need to embed Arial (? or rely on fc-match). Supposedly https://vecta.io/nano will do this, according to their own https://vecta.io/blog/how-to-use-fonts-in-svg . Or could try to do it ourselves , see https://lvngd.com/blog/how-embed-google-font-svg/


### TODO: Terms and conditions
TODO: note Terms & Conditions on last slide #11.
	>>>>
	The Clean Hydrogen Ladder is the copyright of Michael Liebreich/Liebreich Associates Limited. We are releasing these charts (but not any accompanying article or presentation) under the terms of a Creative Commons Attribution 3.0 Unported License (CC-BY 3.0), which means that you are free to reproduce, use or modify these charts. If you make modifications, you must indicate which part or parts you have changed, not pass off the resulting ladder as the work of Michael Liebreich/Liebreich Associates Limited. Please include a credit on each page or image in the following format (including the links):
		Source: Michael Liebreich/Liebreich Associates, Clean Hydrogen Ladder, Version 4.1, 2021.
Concept credit: Adrian Hiel, Energy Cities. As modified by skierpage. CC-BY 3.0
	<<<<

TODO: I could add a (c) symbol that pops this up.

TODO: should I change T&C text in SVG to add "as modified by skierpage."

## Bugs
TODO: BUG: If I import the SVG back into LibreOffice (Impress opens), the underlined text in the T&C doesn't appear (check with the original export)
TODO: BUG: If I insert the SVG into a LibreOffice Draw document, only the master slide graphics appear, not the stuff on the slide (check with the original export)

TODO: BUG: LibreOffice SVG export fails validation
hydrogen_uses_ladder.svg is valid XML, but 
https://validator.w3.org/check complains

*  Error Line 21, Column 133: end tag for "font-face" which is not finished 
   <font-face font-family="Arial embedded" units-per-em="2048" font-weight="normal" font-style="normal" ascent="1852" descent="423"/>
This suggests it wants to have some child element.

TODO: In a browser with JS disabled (easiest to do in Konqueror), the items in the ladder layer of the edited SVG don't appear. I could go through and remove all the 'visibility: "hidden"' attributes, or set them to 'visibility: "visible"'. But maybe if I reverted to an earlier version, fixed the visibility of class="SlideGroup", then ungrouped in Inkscape, I would fix it once and for all. 
^^^^ did I do this?

### TODO: Cleanup
Remove all the ooo: attributes

Remove the `<defs>` section that names slide elements and is out-of-date and probably useless.


The main content is nested g1234 > g1232 > container-id1 > id1 (which has a clip path) > g1228. Could remove most or all of these...
To do this in Inkscape:
* remove g1232 group (ungroup?)
* remove (ungroup) container-id1
* then release object id1 from its clip_path (in the file as #presentataion_clip_path).
* The clip_path became black rect3002 (not present before) which I deleted.

Now I'm down to g id1 class "Slide", a group of 1. ungroup that to give g id "g1228" class "Page", ooo:name "Clean_Hydrogen_Ladder"
Ungroup that and I have all the items on the slide.

In hydrogen_uses_ladder_INKSCAPE_UNGROUPED_ROW_A.svg, I selected the top row of rects, grouped them, gave the group the ID "g_rowA".


The original SVG has two paths for each rounded rect, one setting the fill and one setting the stroke. Why not just one path that sets both?
- TODO: Check if Impress exports a rounded rect with separate fill and stroke paths.
- BUG: is this a PPTX import bug or a bug in how Impress exports a rounded rect with a fill and stroke?


## Cleanup done (??)
Removed overall group
Removed dummy-master-page group for class Master_Slide and its Background and BackgroundObjects
Removed bg-id2 class Background (filled with white, but it seems white anyway).
Removed the dummy-slide and dummy-master-page groups (still have ooo: groups mentioning them)
Kept bo-id ("BackgroundObjects" group


### Fixed the LibreOffice export
To get the Liebrich badge and footer text to appear I had to edit the SVG to comment out the opening and closing `<defs>` tag around the Slide Master components, and then deleted the `<script>` tag.
I filed Inkscape bug https://gitlab.com/inkscape/inbox/-/issues/6566

[![CC BY 3.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 3.0 Unported License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/3.0/
[cc-by-image]: https://i.creativecommons.org/l/by/3.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%203.0-lightgrey.svg
