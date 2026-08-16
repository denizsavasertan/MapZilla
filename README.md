MapZilla
Turn any city into a clean, plotter-ready line drawing. Search a location, frame the area against a real paper size, adjust the map layers, and export an SVG sized in millimeters — ready for a pen plotter.
Inspired by prettymaps (layered map styling) and city-roads (fast interactive road-network export), built specifically around a plotter workflow: real paper dimensions, per-layer stroke control, and a clean vector export.
Status
v0.1 — MVP prototype. Fully client-side, no backend yet.
	•	✅ Search a city/address (Nominatim)
	•	✅ Pan/zoom map with a paper-ratio frame overlay
	•	✅ Paper size + orientation + margin (A5–A2, US Letter, Square)
	•	✅ Layer toggles: roads, buildings, water, green space, railway — each with its own color and stroke width
	•	✅ Live SVG preview
	•	✅ SVG export (millimeter-accurate viewBox, one <g> per layer)
Not yet implemented (planned):
	•	G-code export
	•	Path optimization (merge / simplify / travel-distance minimization)
	•	Hatch fill for buildings/water
	•	Multi-pen layer export
	•	Backend caching layer for Overpass queries (needed for heavier use — see note below)
Running it
This is a single static HTML file — no build step, no install.
	•	Locally: just open index.html in a browser.
	•	Hosted: enable GitHub Pages on this repo (Settings → Pages → deploy from main / root) and it’ll be live at https://<your-username>.github.io/MapZilla/.
How it works
	1.	You position a paper-shaped frame over the map.
	2.	On “Draw This Area,” the app queries the public Overpass API directly from the browser for roads, buildings, water, green space, and railways inside that frame.
	3.	Coordinates are projected from lat/lon to a local planar system (meters), then scaled to fit the chosen paper size and margins.
	4.	Each OSM feature becomes an SVG <path>, grouped by layer, styled with the color/width you set in the sidebar.
	5.	Export downloads the SVG with a millimeter-based viewBox, so it opens true-to-scale in Inkscape or your plotter software.
Known limitations
	•	Large areas can hit Overpass’s public rate limits or time out — keep the frame reasonably small (under a few km) for now.
	•	No backend means every user query hits the public Overpass API directly. Fine for personal/light use; a caching proxy is planned before this goes further.
	•	Water/green areas from OSM relation (multipolygon) geometries aren’t parsed yet — only simple way geometries. Some large water bodies or parks may be missing or incomplete.
Tech
Vanilla HTML/CSS/JS, Leaflet for the map, OpenStreetMap tiles, Overpass API for data, Nominatim for geocoding. No frameworks, no build tools.
