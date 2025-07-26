# Sollumz Quick Navigation Index

## 🚀 Getting Started
- [README.md](README.md) - Main project overview and setup
- [Installation Guide](https://docs.sollumz.org/getting-started/installation) - Official installation instructions
- [Wiki](https://docs.sollumz.org/) - Comprehensive documentation
- [Discord Server](https://discord.sollumz.org/) - Community support

## 📂 Core Structure

### Main Entry Points
- [`__init__.py`](__init__.py) - Blender addon initialization and metadata
- [`auto_load.py`](auto_load.py) - Module auto-loading system
- [`blender_manifest.toml`](blender_manifest.toml) - Blender addon manifest

### Core UI & Operations
- [`sollumz_ui.py`](sollumz_ui.py) - Main UI panels and interfaces
- [`sollumz_operators.py`](sollumz_operators.py) - Core Blender operators
- [`sollumz_properties.py`](sollumz_properties.py) - Custom properties and data structures
- [`sollumz_preferences.py`](sollumz_preferences.py) - Addon preferences and settings
- [`sollumz_pie.py`](sollumz_pie.py) - Pie menu interfaces
- [`tabbed_panels.py`](tabbed_panels.py) - Tabbed panel UI system

### Helper Systems
- [`sollumz_helper.py`](sollumz_helper.py) - General helper functions
- [`sollumz_tool.py`](sollumz_tool.py) - Tool-specific utilities
- [`sollumz_debug.py`](sollumz_debug.py) - Debug utilities and tools
- [`icons.py`](icons.py) - Icon management system

## 🗂️ File Format Modules

### YDR (Drawable Models)
**Location:** [`ydr/`](ydr/)
- **Import/Export:** [`ydr/ydrimport.py`](ydr/ydrimport.py), [`ydr/ydrexport.py`](ydr/ydrexport.py)
- **Core Features:**
  - Model data management ([`model_data.py`](ydr/model_data.py))
  - Shader materials ([`shader_materials.py`](ydr/shader_materials.py), [`shader_materials_v2.py`](ydr/shader_materials_v2.py))
  - Lights system ([`lights.py`](ydr/lights.py))
  - Cable system ([`cable.py`](ydr/cable.py), [`cable_mesh_builder.py`](ydr/cable_mesh_builder.py))
  - Cloth physics ([`cloth.py`](ydr/cloth.py), [`cloth_char.py`](ydr/cloth_char.py), [`cloth_env.py`](ydr/cloth_env.py))
  - Mesh building ([`mesh_builder.py`](ydr/mesh_builder.py), [`vertex_buffer_builder.py`](ydr/vertex_buffer_builder.py))

### YFT (Fragment Models)
**Location:** [`yft/`](yft/)
- **Import/Export:** [`yft/yftimport.py`](yft/yftimport.py), [`yft/yftexport.py`](yft/yftexport.py)
- **Core Features:**
  - Fragment merging ([`fragment_merger.py`](yft/fragment_merger.py))
  - Fragment properties and UI

### YDD (Drawable Dictionary)
**Location:** [`ydd/`](ydd/)
- **Import/Export:** [`ydd/yddimport.py`](ydd/yddimport.py), [`ydd/yddexport.py`](ydd/yddexport.py)
- Multiple drawable management

### YBN (Collision/Bounds)
**Location:** [`ybn/`](ybn/)
- **Import/Export:** [`ybn/ybnimport.py`](ybn/ybnimport.py), [`ybn/ybnexport.py`](ybn/ybnexport.py)
- **Core Features:**
  - Collision materials ([`collision_materials.py`](ybn/collision_materials.py))
  - Flag presets ([`flag_presets.xml`](ybn/flag_presets.xml))

### YCD (Clip Dictionary/Animations)
**Location:** [`ycd/`](ycd/)
- **Import/Export:** [`ycd/ycdimport.py`](ycd/ycdimport.py), [`ycd/ycdexport.py`](ycd/ycdexport.py)
- Animation clip management

### YTYP (Type Definitions)
**Location:** [`ytyp/`](ytyp/)
- **Import/Export:** [`ytyp/ytypimport.py`](ytyp/ytypimport.py), [`ytyp/ytypexport.py`](ytyp/ytypexport.py)
- **Core Features:**
  - Archetype definitions ([`ui/archetype.py`](ytyp/ui/archetype.py))
  - MLO (Map Loader Object) support ([`properties/mlo.py`](ytyp/properties/mlo.py), [`ui/mlo.py`](ytyp/ui/mlo.py))
  - Entity management ([`operators/entity.py`](ytyp/operators/entity.py), [`ui/entities.py`](ytyp/ui/entities.py))
  - Extensions system ([`operators/extensions.py`](ytyp/operators/extensions.py), [`properties/extensions.py`](ytyp/properties/extensions.py))
  - Gizmos for visual helpers ([`gizmos/`](ytyp/gizmos/))

### YMAP (Map Files)
**Location:** [`ymap/`](ymap/)
- **Import/Export:** [`ymap/ymapimport.py`](ymap/ymapimport.py), [`ymap/ymapexport.py`](ymap/ymapexport.py)
- Map entity placement and management

### YNV (Navigation Mesh)
**Location:** [`ynv/`](ynv/)
- **Import:** [`ynv/ynvimport.py`](ynv/ynvimport.py)
- Navigation mesh data

## 🛠️ Core Systems

### CWXML (CodeWalker XML)
**Location:** [`cwxml/`](cwxml/)
- XML parsing and generation for all file formats
- Key files:
  - [`element.py`](cwxml/element.py) - Base XML element handling
  - [`drawable.py`](cwxml/drawable.py) - Drawable XML structures
  - [`fragment.py`](cwxml/fragment.py) - Fragment XML structures
  - [`bound.py`](cwxml/bound.py) - Collision/bounds XML
  - [`shader.py`](cwxml/shader.py) - Shader definitions
  - [`ymap.py`](cwxml/ymap.py), [`ytyp.py`](cwxml/ytyp.py) - Map format XML

### Tools & Helpers
**Location:** [`tools/`](tools/)
- [`blenderhelper.py`](tools/blenderhelper.py) - Blender-specific utilities
- [`drawablehelper.py`](tools/drawablehelper.py) - Drawable manipulation
- [`boundhelper.py`](tools/boundhelper.py) - Bounds/collision helpers
- [`jenkhash.py`](tools/jenkhash.py) - Jenkins hash implementation
- [`meshhelper.py`](tools/meshhelper.py) - Mesh manipulation utilities
- [`animationhelper.py`](tools/animationhelper.py) - Animation utilities

### Shared Utilities
**Location:** [`shared/`](shared/)
- [`geometry.py`](shared/geometry.py) - Geometric calculations
- [`math.py`](shared/math.py) - Mathematical utilities
- [`shader_nodes.py`](shared/shader_nodes.py) - Shader node management
- [`shader_expr/`](shared/shader_expr/) - Shader expression compiler

### Versioning System
**Location:** [`versioning/`](versioning/)
- Version migration scripts for different Sollumz versions
- [`versioning_230.py`](versioning/versioning_230.py), [`versioning_240.py`](versioning/versioning_240.py), etc.

## 🧪 Testing
**Location:** [`tests/`](tests/)
- Unit tests for various components
- Test assets in [`tests/assets/`](tests/assets/)
- Run tests with [`tests/run.py`](tests/run.py)

## 📋 Quick Reference

### Common Operations
1. **Import a model**: File → Import → Select format (YDR/YFT/YDD/etc)
2. **Export a model**: File → Export → Select format
3. **Access Sollumz tools**: 3D Viewport → N-panel → Sollumz tab
4. **Preferences**: Edit → Preferences → Add-ons → Sollumz

### Key Data Types
- **Drawable**: Basic 3D model (`.ydr`)
- **Fragment**: Breakable/physics model (`.yft`)
- **Drawable Dictionary**: Collection of drawables (`.ydd`)
- **Bounds**: Collision data (`.ybn`)
- **Archetype**: Object definitions (`.ytyp`)
- **Map**: World placement data (`.ymap`)
- **Animation**: Animation clips (`.ycd`)

### Important Presets
- [`ydr/shader_presets.xml`](ydr/shader_presets.xml) - Shader configurations
- [`ydr/light_presets.xml`](ydr/light_presets.xml) - Light settings
- [`ybn/flag_presets.xml`](ybn/flag_presets.xml) - Collision flags
- [`cwxml/Shaders.xml`](cwxml/Shaders.xml) - Shader definitions

## 🔍 Need More Info?
- Check the [official wiki](https://docs.sollumz.org/)
- Join the [Discord server](https://discord.sollumz.org/)
- Report issues on [GitHub](https://github.com/Sollumz/Sollumz/issues)