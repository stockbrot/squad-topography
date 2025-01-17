# Squad Topographic Maps

This repository contains hand-drawn topographic recreations of maps inspired by the game Squad. These maps aim to enhance clarity and usability for the community by providing detailed terrain information, all created using standardized topographic mapping techniques. While accuracy and adherence to these techniques are important, equal care has been taken to ensure the maps are visually appealing, blending functionality with a touch of style befitting a videogame setting.

---

## Workflow

Here’s an overview of the process used to create these maps:

1. **Extracting Map Data**
   - Using the *Squad* SDK to gather essential data, including heightmaps, map resolution, scale, size, and features.
   - Using Blueprint functions to extract road, building, forests and other features, for later use as masks.
   - Analyzing in-game features such as roads, rivers, buildings, forests, and terrain types for accurate placement.

2. **Generating Base Layers in QGIS**
   - Importing heightmap data to create contour lines and hillshading.
   - Adjusting contour intervals and hillshade settings to ensure clarity and alignment with topographic mapping standards.

3. **Hand-Editing with Inkscape**
   - Using vector tools to manually place or draw roads, buildings, rivers, forests, and other critical features.
   - Ensuring accuracy by cross-referencing in-game visuals and real-world mapping principles.

4. **Polishing in Photoshop**
   - Enhancing the map’s visual appeal with color adjustments, layer blending, and custom effects.
   - Applying standardized symbols, labels, and color schemes for a professional and readable finish.

---

## Maps Included

As of now, the following maps are in progress (I plan to do all 23):

- **Yehorivka**
- **Al-Basrah**
- **Anvil**
- **Lashkar Valley**


---

## Usage

These maps are made available for **personal, non-commercial use only**. Please read the full license terms below for details.

### Key Notes:
- You may download and use these maps for personal reference or enjoyment.
- Commercial use, redistribution, or modification of these maps is strictly prohibited.
- If you wish to share these maps, please provide a link to this repository rather than redistributing them directly.

---

## Getting contour labels for fictional maps using QGIS

First, you need to create a .wld file with the same name as the heightmap used in QGIS.

For example, if you have Yehorivka-heightmap.png, you should create a Yehorivka-heightmap.wld file with the following content:

```
1
0
0
-1
0
0
```

This tells QGIS that the "world" coordinates are at 1, -1, which prevents the contours from flipping later. This is required for generated heightmaps that have no geospatial data. While you can attach a CRS, I had minimal success with this approach.

With the heightmap layer selected in QGIS, go to Raster -> Extraction -> Contour.

Default values are generally fine, but you should test which "Interval between contour lines" fits best for your landscape by setting the "Layer Style" of your heightmap to contour. For Yehorivka, I used an interval of 50.

You can follow this tutorial by "Geospatial School": [Tutorial](https://www.youtube.com/watch?v=0oyZ0gwLKXY)

For the context of Yehorivka, I used the following field calculations:

### Elevation
To get the correct elevation labels, I placed two actors in Yehorivka in the Squad SDK and used their values to determine the total elevation, which is 161 meters.

Since QGIS output the ELEV attribute ranging from 250 to 5850, you can remap these values to new elevation values by using:

UE4 Height Range / QGIS Height Range --> 160/5600 = 0.028

You can also use this value as the z-factor for the hillshading layer style, which looks nice!

The calculation for the new elevation variable is:

`floor("ELEV" * 0.028 + 60) - 1` 

The +60 is the Mean Sea Level (MSL). Since actual MSL values are not available, I used close approximations based on geographical similarities suggested by ChatGPT.

Continue following the tutorial with the new elevation variable instead of ELEV.

### Index
For Yehorivka, which is fairly flat, I used a 5-meter scale for each index line.

The calculation is:

`if("elevation"%5=0,1,NULL)`

---

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)** license. 
Just because I don't know any better, I want to protect the effort and time I’ve invested in this project. If you have suggestions for a better alternative, feel free to share them!

### Summary of Terms:
- **Attribution**: You must credit the creator (this repository) when using the maps.
- **Non-Commercial**: These maps may not be used for commercial purposes.
- **No Derivatives**: You may not modify, remix, or build upon these maps.

For the full legal terms, visit [Creative Commons CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode).

---

## Disclaimer

These maps are recreations based on *Squad*'s heightmap data, which remains the property of Offworld Industries (OWI). 

- This project is not affiliated with or endorsed by OWI.
- The original heightmaps are not included in this repository, as they were not created by the author.
- These maps are purely for personal and community use.
- I intend to 

---

## Feedback and Contributions

Feedback is welcome! If you spot an error or have suggestions for improvements, feel free to open an issue or reach out. However, since derivative works are not allowed under the license, contributions involving modifications to the maps themselves cannot be accepted.

Thank you for your interest and support!

