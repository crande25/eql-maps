# eql-maps

In-game EverQuest Legends maps for new or altered zones.

These are standard EverQuest map files — plain text line data the client draws on
the in-game map window. They are generated from each zone's own geometry, so they
reflect what the zone actually contains rather than a hand-traced approximation.

## Installing

**Don't drop these loose into the client's `maps` folder.** EverQuest rewrites around
a hundred default zone maps every time it starts, and the patcher re-downloads its own
map files on top of that. Anything custom sitting directly in `maps\` eventually gets
overwritten, and labels frequently end up duplicated.

Put them in a map pack subfolder instead — the same way the community distributes
[Brewall's](https://www.eqmaps.info/eq-map-files/) and
[Good's](https://github.com/RedGuides/goodurden-maps) packs. Subfolders are left alone
by the patcher, and the client lets you switch between them in game.

1. Find your EverQuest `maps` folder. It's typically at
   `C:\Users\Public\Daybreak Game Company\Installed Games\EverQuest\maps\`
   (older installs use `C:\Users\Public\EverQuest\maps\`).

2. Copy `newsebexp.txt` into the subfolder of whichever pack you already use — for
   example `maps\Brewall\` or `maps\Good's Maps\`. If you don't run a pack, create your
   own subfolder such as `maps\eql\` and put it there.

3. In game, open the map window (`M` by default) and choose that folder from the
   dropdown in the upper-left corner of the window.

Keep the filename exactly as published. The client matches map files to zones by short
name, so renaming one stops it from loading.

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
