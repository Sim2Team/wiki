---
layout: sidebar
sidebar: research
content-text: Game List
title: Research Index
description: Research Index page
permalink: /research
---

**Click on one of the images below or on the sidebar to be redirected to the research page of the specific game.**

<div class="card card-main mb-3">
	<div class="card-body card-clr">
		<div class="container">
			<div class="row mb-3">
				<div class="col-sm-4 mb-3">
					<!-- The Sims Bustin' Out (GBA). !-->
					<div class="card sub-card-transparent" id="bustin-gba-card">
						<div class="card-header card-title-bar">
							<h4 class="card-title">The Sims Bustin' Out (Game Boy Advance)</h4>
						</div>
						<div class="card-body card-clr">
							<a href="{{ "/research/bustinout" | absolute_url }}">
								<img src="https://github.com/Sim2Team/Sim2Team.github.io/raw/main/assets/images/bustinOutGBACover.png" alt="The Sims Bustin' Out Game Boy Advance cover image" class="card-img-top">
							</a>
						</div>
					</div>
				</div>
				<div class="col-sm-4 mb-3">
					<!-- The Urbz - Sims in the City (GBA). !-->
					<div class="card sub-card-transparent" id="urbz-gba-card">
						<div class="card-header card-title-bar">
							<h4 class="card-title">The Urbz - Sims in the City (Game Boy Advance)</h4>
						</div>
						<div class="card-body card-clr">
							<a href="{{ "/research/urbzgba" | absolute_url }}">
								<img src="https://github.com/Sim2Team/Sim2Team.github.io/raw/main/assets/images/urbzGBACover.png" alt="The Urbz - Sims in the City Game Boy Advance cover image" class="card-img-top">
							</a>
						</div>
					</div>
				</div>
				<div class="col-sm-4">
					<!-- The Urbz - Sims in the City (NDS). !-->
					<div class="card sub-card-transparent" id="urbz-nds-card">
						<div class="card-header card-title-bar">
							<h4 class="card-title">The Urbz - Sims in the City (Nintendo DS)</h4>
						</div>
						<div class="card-body card-clr">
							<a href="{{ "/research/urbznds" | absolute_url }}">
								<img src="https://github.com/Sim2Team/Sim2Team.github.io/raw/main/assets/images/urbzNDSCover.png" alt="The Urbz - Sims in the City Nintendo DS cover image" class="card-img-top">
							</a>
						</div>
					</div>
				</div>
			</div>
			<div class="row">
				<div class="col-sm-4 mb-3">
					<!-- The Sims 2 (GBA). !-->
					<div class="card sub-card-transparent" id="sims2-gba-card">
						<div class="card-header card-title-bar">
							<h4 class="card-title">The Sims 2 (Game Boy Advance)</h4>
						</div>
						<div class="card-body card-clr">
							<a href="{{ "/research/sims2gba" | absolute_url }}">
								<img src="https://github.com/Sim2Team/Sim2Team.github.io/raw/main/assets/images/sims2GBACover.png" alt="The Sims 2 Game Boy Advance cover image" class="card-img-top">
							</a>
						</div>
					</div>
				</div>
				<div class="col-sm-4">
					<!-- The Sims 2 (NDS). !-->
					<div class="card sub-card-transparent" id="sims2-nds-card">
						<div class="card-header card-title-bar">
							<h4 class="card-title">The Sims 2 (Nintendo DS)</h4>
						</div>
						<div class="card-body card-clr">
							<a href="{{ "/research/sims2nds" | absolute_url }}">
								<img src="https://github.com/Sim2Team/Sim2Team.github.io/raw/main/assets/images/sims2NDSCover.png" alt="The Sims 2 Nintendo DS cover image" class="card-img-top">
							</a>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
<hr>


## Contributing Rules
The best before contributing is to discuss it on the <a href="{{ "/server" | absolute_url }}">Sim2Team's discord server - Sim2Server</a>.

That way, we can talk about how to contribute it the best and review things before.

Other than that... here are some of the rules for contributing.

### Styling rules
The styling rules are sort of a thing to discuss, personally me (SuperSaiyajinStackZ) do it as the following:

- The files for the pages should be `.md` (markdown).
- You can also use HTML if necessary, for example to properly link some things from other pages with the `<a>` tag like: `<a href="{ { "/research" | absolute_url } }">Research Index</a>`.
    - Because GitHub Pages doesn't have the sub sites before the main site name, the `<a>` tag way with jekyll is actually required to link to something with `| absolute_url`, otherwise it may link to `https://sim2team.github.io/` instead of this site.
- Use `<hr>` and then add 2 free lines (if another one follows) after a Section ends.
- Probably more to discuss about the actual style at a later point.


### Creating Pages
Here a basic guide how to add / create pages.

- Go into the `_data/structure/` folder and find the JSON file for the game you want to add a research page.
- Extend the object for the page you want to add, here a short explanation about each of the things:
    - `title`: The title of the page, it will be shown on the sidebar and on the actual page on the top.
	- `type`: The type of the page, such as `General` for things related to the Savefile AND Internal, `Internal` for internal things, and `Savefile` for Savefile related things.
	- `url`: The link to the page, without extension, such as `/research/sims2gba/savefile/episode`.

Now that the `_data/structure` part is done, it's time to get on the actual page.

- Go into the `pages/research/` folder and find the proper place with the game and the type.
- Create a `.md` file inside the folder. The name should all be lowercase.
- Add the following Header to the created file:

```
---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Episode
description: The Sims 2 Game Boy Advance | Savefile Episode Research
permalink: /research/sims2gba/savefile/episode
---

**Researched by [YourName](LINK), Version: X.X.X.**
<hr>
```

- `layout` should stay the same as is. There is nothing to edit on that one.
- Replace `researchcategory` with the type, like on the JSON.
- Replace `structure` with the name of the JSON, but without the `.json`.
- Replace `title` with the title of the page. It should be exactly like the title in the JSON, so it would make the current page from the sidebar bold.
- Replace `description` with the description for the page. Generally on an actual research page it should look like this: `The Sims 2 Game Boy Advance | Savefile Episode Research`.
- Replace `permalink` with the URL like in the JSON.
- Replace `YourName` with the name you want to be shown as on the page, and `LINK` with an optional URL that could link to your GitHub for example. If you don't want to be there, just replace `LINK` with a `#` to it.
- Replace `Version: X.X.X.` with the version for the page. A good option would be `0.1.0` for the start.

***If you are editing an existing page and your name is not on there, just add a `, [YourName](LINK)` or so on there if you want to be credited for the contribution.***

Is that done, then just add 1 new line and then start with `## Your Section`. Below then you can just add your content and finish that with a `<hr>` tag. Optional if you think a new category / type is required, feel free to ask on the Sim2Server and we'll see if that's a good idea.

***As of now, me (SuperSaiyajinStackZ) is the actual only contributor to the research pages.***
<hr>