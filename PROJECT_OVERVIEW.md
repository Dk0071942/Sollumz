# Sollumz Project Overview

## 🎮 What is Sollumz?

Sollumz is a comprehensive Blender addon for creating, importing, and exporting Grand Theft Auto V (GTA V) assets. It provides a complete workflow for modders to work with GTA V's proprietary file formats using Blender's powerful 3D modeling environment.

### Key Features
- **Full Format Support**: Import/export YDR, YFT, YDD, YBN, YTYP, YCD, and YMAP files
- **Visual Editing**: Work with GTA V assets directly in Blender
- **Material System**: Advanced shader editing with GTA V's material system
- **Animation Support**: Import and export animations (YCD)
- **Collision Editing**: Create and modify collision meshes (YBN)
- **Map Editing**: Place and manage entities in the game world (YMAP/YTYP)

## 🏗️ Architecture Overview

### Core Components

#### 1. **File Format Handlers**
Each GTA V file format has its own module with dedicated import/export functionality:
- **YDR** (Drawable): Static 3D models
- **YFT** (Fragment): Dynamic/breakable objects with physics
- **YDD** (Drawable Dictionary): Collections of models
- **YBN** (Bounds): Collision data
- **YCD** (Clip Dictionary): Animations
- **YTYP** (Types): Object definitions and archetypes
- **YMAP** (Map): World entity placement

#### 2. **CWXML System**
The CodeWalker XML (CWXML) system handles conversion between GTA V's binary formats and human-readable XML:
```
Binary Format ↔ CWXML ↔ Blender Data
```

#### 3. **UI System**
- **Main Panel**: Central Sollumz panel in Blender's N-panel
- **Pie Menus**: Quick access to common operations
- **Property Groups**: Custom properties for GTA V-specific data
- **Gizmos**: Visual helpers for lights, extensions, and other game entities

#### 4. **Helper Systems**
- **Material/Shader System**: Manages GTA V's complex shader system
- **Mesh Builder**: Optimizes geometry for game engine
- **Animation System**: Handles bone animations and constraints
- **Hash System**: Jenkins hash for game asset names

## 📊 Data Flow

### Import Process
1. User selects GTA V file (XML format from CodeWalker)
2. CWXML parser reads and validates the file
3. Format-specific importer creates Blender objects
4. Materials, textures, and properties are set up
5. Helper systems optimize the scene

### Export Process
1. Validation checks on Blender scene
2. Format-specific exporter gathers data
3. Mesh optimization and processing
4. CWXML generation with proper structure
5. File written in CodeWalker XML format

## 🔧 Technical Stack

### Dependencies
- **Blender**: 4.0+ (Python API)
- **CodeWalker**: For binary ↔ XML conversion
- **Python Libraries**: Standard library only (no external deps in runtime)

### Key Technologies
- **Python 3.x**: Core implementation language
- **Blender Python API**: Integration with Blender
- **XML Processing**: For CodeWalker format handling
- **Custom Binary Formats**: Vertex buffers, shader parameters

## 🎯 Use Cases

### 1. **Vehicle Modding**
- Import vehicle models (YFT)
- Edit body, wheels, and parts
- Set up materials and liveries
- Export with proper hierarchy

### 2. **Map Modding**
- Create custom buildings (YDR)
- Design MLO interiors (YTYP)
- Place entities in world (YMAP)
- Set up collisions (YBN)

### 3. **Character/Ped Modding**
- Import character models
- Edit clothing and accessories
- Set up cloth physics
- Export with skeletons

### 4. **Animation Creation**
- Import existing animations
- Create new animations
- Export animation clips (YCD)

## 🚀 Getting Started

### Installation
1. Download latest release from GitHub
2. Install in Blender: Edit → Preferences → Add-ons → Install
3. Enable "Import-Export: Sollumz"

### Basic Workflow
1. **Import**: File → Import → Select format
2. **Edit**: Use Blender tools + Sollumz panels
3. **Configure**: Set properties in Sollumz panel
4. **Export**: File → Export → Select format

### Important Concepts
- **Drawable**: Basic renderable object
- **Fragment**: Physics-enabled object
- **Archetype**: Template for game objects
- **Bounds**: Collision geometry
- **Shader**: Material with game-specific properties

## 📁 Project Structure

### Main Systems
- **Core**: Initialization, properties, operators
- **UI**: Panels, menus, gizmos
- **Formats**: Import/export for each file type
- **Helpers**: Utilities and tools
- **CWXML**: XML parsing and generation

### Module Organization
```
Sollumz/
├── Core Files (init, properties, operators)
├── Format Modules (ydr/, yft/, etc.)
├── Support Systems (cwxml/, tools/, shared/)
├── UI Components (panels, gizmos)
└── Tests & Documentation
```

## 🔗 Integration Points

### With Blender
- Custom properties on objects
- Shader node integration
- Animation system usage
- Collection organization

### With GTA V
- Proper naming conventions
- Hash generation for assets
- Game-specific limits respected
- Performance optimization

## 📚 Further Reading
- [Module Reference](MODULE_REFERENCE.md) - Detailed module documentation
- [File Formats Guide](FILE_FORMATS.md) - Format specifications
- [Developer Guide](DEVELOPER_GUIDE.md) - Contributing and development
- [Quick Navigation](INDEX.md) - Fast access to any file