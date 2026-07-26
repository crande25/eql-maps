# eql-maps

In-game EverQuest Legends maps for new or altered zones.

These are standard EverQuest map files — plain text line data the client draws on
the in-game map window. They are generated from each zone's own geometry, so they
reflect what the zone actually contains rather than a hand-traced approximation.

## Installing

Copy the `.txt` files into your EverQuest client's `maps` folder, then bring up the
in-game map. The client picks up map files by zone short name, so the filename must
stay exactly as published.

## Available maps

| File | Zone | Lines |
|---|---|---|
| `newsebexp.txt` | New Sebilis | 1,166 |

## Reading the maps

Line colors indicate depth, following the usual community convention:

- **Black** — the zone's main level, where most of the walkable space is
- **Tan / gray** — areas above the main level
- **Purple / blue** — areas below the main level

Only wall and ledge boundaries are drawn. Flat floor interiors are intentionally
left blank so the map stays readable when several levels overlap.

## How these are made

Each map is extracted from the zone's own client geometry:

1. Unpack the zone's PFS archive and parse the `.wld` mesh fragments.
2. Classify every triangle as floor, wall, or ceiling by its surface normal.
3. Keep the edges where floors meet walls — the walkable boundary — plus open ledges.
4. Chain those edges into polylines, simplify them, and drop duplicate contours.
5. Convert world coordinates to map coordinates and color by depth band.

No client files are included in this repository. See `.gitignore` — game assets are
copyrighted and stay out of version control. Only the derived map text is published here.

## License

Released under [CC0 1.0 Universal](LICENSE) — public domain. Use them, host them,
modify them, no attribution required.
