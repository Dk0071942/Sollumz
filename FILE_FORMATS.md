# Sollumz File Format Reference

## Overview

This document details the GTA V file formats supported by Sollumz. All formats are handled through CodeWalker's XML representation, which Sollumz imports and exports.

## Supported Formats

### YDR - Drawable
**Purpose**: Static 3D models (buildings, props, vehicles)  
**Extension**: `.ydr.xml`

#### Structure
```xml
<Drawable>
  <Name>model_name</Name>
  <Bounds>
    <Min x="0" y="0" z="0"/>
    <Max x="1" y="1" z="1"/>
  </Bounds>
  <LodGroup>
    <High><!-- LOD 0 mesh data --></High>
    <Med><!-- LOD 1 mesh data --></Med>
    <Low><!-- LOD 2 mesh data --></Low>
  </LodGroup>
  <Shaders><!-- Shader definitions --></Shaders>
  <DrawableModels><!-- Mesh geometry --></DrawableModels>
</Drawable>
```

#### Key Components
- **LOD Levels**: High, Medium, Low, Very Low
- **Shaders**: Material definitions with parameters
- **Skeleton**: Bone hierarchy (optional)
- **Lights**: Light entities (optional)

#### Sollumz Properties
- Drawable type (normal, weapon, vehicle, etc.)
- LOD distances
- Render flags
- Bounds configuration

### YFT - Fragment
**Purpose**: Dynamic/breakable objects with physics  
**Extension**: `.yft.xml`

#### Structure
```xml
<Fragment>
  <Name>fragment_name</Name>
  <Bounds><!-- Bounding info --></Bounds>
  <Drawable><!-- Visual model --></Drawable>
  <Physics>
    <LOD1><!-- Physics data --></LOD1>
    <LOD2><!-- Simplified physics --></LOD2>
    <LOD3><!-- Most simplified --></LOD3>
  </Physics>
  <VehicleGlassWindows><!-- Glass definitions --></VehicleGlassWindows>
</Fragment>
```

#### Key Components
- **Drawable**: Visual representation
- **Physics**: Collision and mass properties
- **Children**: Breakable parts
- **Glass Windows**: Vehicle glass definitions

#### Physics Properties
- Mass
- Inertia tensor
- Damage threshold
- Fragment health

### YDD - Drawable Dictionary
**Purpose**: Collection of related drawables  
**Extension**: `.ydd.xml`

#### Structure
```xml
<DrawableDictionary>
  <Drawables>
    <Item><!-- First drawable --></Item>
    <Item><!-- Second drawable --></Item>
    <!-- More drawables -->
  </Drawables>
</DrawableDictionary>
```

#### Use Cases
- Weapon components
- Vehicle modifications
- Ped variations
- Prop collections

### YBN - Bounds/Collision
**Purpose**: Collision meshes and physics bounds  
**Extension**: `.ybn.xml`

#### Structure
```xml
<Bounds>
  <Type>Composite</Type>
  <BoundingBoxMin><!-- Min coords --></BoundingBoxMin>
  <BoundingBoxMax><!-- Max coords --></BoundingBoxMax>
  <Children>
    <Item>
      <Type>Box|Sphere|Capsule|Mesh|etc</Type>
      <!-- Shape-specific data -->
    </Item>
  </Children>
</Bounds>
```

#### Collision Types
- **Box**: Simple box collision
- **Sphere**: Spherical bounds
- **Capsule**: Cylinder with rounded ends
- **Mesh**: Complex triangle mesh
- **Composite**: Multiple shapes

#### Material Properties
- Material type (concrete, metal, wood, etc.)
- Flags (stairs, no climb, etc.)
- Procedural ID
- Room ID (for interiors)

### YCD - Clip Dictionary
**Purpose**: Animation data  
**Extension**: `.ycd.xml`

#### Structure
```xml
<ClipDictionary>
  <Name>anim_dict_name</Name>
  <Clips>
    <Item>
      <Name>clip_name</Name>
      <Duration>1.0</Duration>
      <Animation><!-- Keyframe data --></Animation>
    </Item>
  </Clips>
</ClipDictionary>
```

#### Animation Data
- Bone animations
- UV animations
- Expression animations
- Root motion

### YTYP - Archetype Definitions
**Purpose**: Object templates and MLO interiors  
**Extension**: `.ytyp.xml`

#### Structure
```xml
<CMapTypes>
  <name>ytyp_name</name>
  <archetypes>
    <Item type="CBaseArchetypeDef">
      <name>archetype_name</name>
      <assetName>model_name</assetName>
      <flags>32</flags>
      <lodDist>100.0</lodDist>
      <!-- More properties -->
    </Item>
  </archetypes>
  <extensions><!-- MLO data if applicable --></extensions>
</CMapTypes>
```

#### Archetype Types
- **Base**: Standard objects
- **Time**: Time-based visibility
- **MLO**: Map Loader Object (interiors)
- **Composite**: Multi-part objects

#### MLO Components
- Rooms
- Portals
- Entity sets
- Timecycle modifiers

### YMAP - Map Files
**Purpose**: World entity placement  
**Extension**: `.ymap.xml`

#### Structure
```xml
<CMapData>
  <name>map_name</name>
  <entities>
    <Item>
      <archetypeName>prop_name</archetypeName>
      <position x="0" y="0" z="0"/>
      <rotation x="0" y="0" z="0" w="1"/>
      <!-- Entity properties -->
    </Item>
  </entities>
  <contentFlags>1</contentFlags>
</CMapData>
```

#### Entity Properties
- Position and rotation
- LOD level
- Parent index
- Flags (ambient occlusion, etc.)

### YNV - Navigation Mesh
**Purpose**: AI pathfinding data  
**Extension**: `.ynv.xml`  
**Support**: Import only

#### Structure
- Navigation polygons
- Connectivity data
- Flags (water, interior, etc.)

## Common Elements

### Vertex Formats
Sollumz supports various vertex layouts:
- **PNCT**: Position, Normal, Color, Texcoord
- **PNCTT**: Above + Tangent
- **PNCTX**: Multiple texture coordinates
- **PBBNCT**: Blendshapes/morphs

### Shader Parameters
Common shader parameters:
- `DiffuseSampler`: Main texture
- `BumpSampler`: Normal map
- `SpecSampler`: Specular map
- `DetailSampler`: Detail texture
- `TintPaletteSelector`: Vehicle colors

### Flags and Enums
Most formats use bit flags for properties:
- Render flags
- Physics flags
- Entity flags
- Material flags

## Working with Formats

### Import Workflow
1. Use CodeWalker to convert binary to XML
2. Import XML in Sollumz
3. Edit in Blender
4. Export back to XML
5. Convert XML to binary in CodeWalker

### Best Practices
- Keep LODs consistent
- Respect game limits (vertices, materials)
- Use appropriate collision materials
- Test in-game frequently

### Common Issues
- **Missing textures**: Ensure texture paths are correct
- **Wrong scale**: Check import/export scale settings
- **Broken physics**: Validate collision materials
- **Performance**: Optimize LODs properly

## Format Limits

### YDR/YFT
- Max vertices per model: ~65k
- Max materials: 255
- Max bones: 255
- Texture size: Power of 2

### YMAP
- Entities per file: ~2000
- Streaming distance: Consider game limits

### YTYP
- Archetypes per file: No hard limit
- MLO rooms: ~32 recommended

## Version Compatibility

Sollumz targets the latest GTA V version. Older versions may have different:
- Shader parameters
- Vertex formats
- Flag values
- Structure layouts

Always use matching CodeWalker version for conversions.