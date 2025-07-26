# Sollumz Module Reference

## Core Modules

### `__init__.py`
**Purpose**: Addon initialization and registration  
**Key Components**:
- `bl_info`: Addon metadata for Blender
- `register()` / `unregister()`: Addon lifecycle
- Module reloading system for development

### `auto_load.py`
**Purpose**: Automatic module discovery and loading  
**Features**:
- Recursively finds all modules in package
- Handles registration order dependencies
- Development hot-reload support

### `sollumz_properties.py`
**Purpose**: Custom property definitions  
**Key Properties**:
- Scene properties for global settings
- Object properties for entity data
- Material properties for shaders
- Mesh properties for vertex attributes

### `sollumz_operators.py`
**Purpose**: Core Blender operators  
**Key Operators**:
- Import/Export operators
- Tool operators (apply modifiers, etc.)
- Utility operators (hash generation, etc.)

### `sollumz_ui.py`
**Purpose**: Main UI panels  
**Panels**:
- Sollumz Tools panel
- Object properties panel
- Material properties panel
- Debug panel

## File Format Modules

### YDR Module (`ydr/`)
**Purpose**: Drawable (static model) support

#### Core Files
- **`ydrimport.py`**: Import YDR files
  - Parses drawable XML structure
  - Creates meshes with proper materials
  - Sets up LODs and bounds
  
- **`ydrexport.py`**: Export YDR files
  - Validates mesh data
  - Optimizes geometry
  - Generates proper XML structure

#### Support Systems
- **`shader_materials.py`**: Material management
  - Shader parameter handling
  - Texture assignment
  - Render bucket configuration

- **`lights.py`**: Light entity support
  - Light creation and editing
  - Presets and templates
  - Game-specific properties

- **`vertex_buffer_builder.py`**: Vertex data optimization
  - Vertex format generation
  - Compression and packing
  - Platform-specific formats

### YFT Module (`yft/`)
**Purpose**: Fragment (physics/breakable) support

#### Core Files
- **`yftimport.py`**: Import YFT files
  - Fragment hierarchy parsing
  - Physics setup
  - Breakable part configuration

- **`yftexport.py`**: Export YFT files
  - Fragment structure generation
  - Physics data export
  - Child fragment handling

- **`fragment_merger.py`**: Fragment operations
  - Merge multiple fragments
  - LOD management
  - Physics optimization

### YDD Module (`ydd/`)
**Purpose**: Drawable Dictionary (model collection) support

- **`yddimport.py`**: Import multiple drawables
- **`yddexport.py`**: Export drawable collections
- Manages drawable relationships and shared resources

### YBN Module (`ybn/`)
**Purpose**: Collision/bounds support

#### Core Files
- **`ybnimport.py`**: Import collision meshes
  - Bound shape parsing
  - Material assignment
  - Flag configuration

- **`ybnexport.py`**: Export collision data
  - Bound generation
  - Optimization
  - Material mapping

- **`collision_materials.py`**: Collision material system
  - Material presets
  - Physics properties
  - Sound/particle effects

### YCD Module (`ycd/`)
**Purpose**: Animation clip support

- **`ycdimport.py`**: Import animations
  - Clip data parsing
  - Bone mapping
  - Curve interpolation

- **`ycdexport.py`**: Export animations
  - Animation baking
  - Compression
  - Clip metadata

### YTYP Module (`ytyp/`)
**Purpose**: Archetype definitions and MLO support

#### Core Systems
- **`properties/ytyp.py`**: Archetype properties
  - Base archetype data
  - LOD configuration
  - Physics properties

- **`properties/mlo.py`**: MLO (interior) properties
  - Room definitions
  - Portal configuration
  - Entity sets

- **`operators/entity.py`**: Entity management
  - Entity creation
  - Placement tools
  - Batch operations

#### Extensions
- **`properties/extensions.py`**: Game entity extensions
  - Lights
  - Particle effects
  - Audio emitters
  - Spawn points
  - Doors
  - And more...

### YMAP Module (`ymap/`)
**Purpose**: Map/world data support

- **`ymapimport.py`**: Import world entities
  - Entity placement
  - Streaming configuration
  - LOD setup

- **`ymapexport.py`**: Export map data
  - Entity instances
  - Content flags
  - Streaming metadata

## Support Systems

### CWXML Module (`cwxml/`)
**Purpose**: CodeWalker XML parsing/generation

#### Core Components
- **`element.py`**: Base XML element class
  - XML parsing
  - Attribute handling
  - Validation

#### Format-Specific
- **`drawable.py`**: Drawable XML structures
- **`fragment.py`**: Fragment XML structures
- **`bound.py`**: Bounds XML structures
- **`shader.py`**: Shader definitions
- **`ymap.py`** / **`ytyp.py`**: Map format structures

### Tools Module (`tools/`)
**Purpose**: Utility functions and helpers

- **`blenderhelper.py`**: Blender-specific utilities
  - Object creation
  - Material setup
  - Collection management

- **`meshhelper.py`**: Mesh manipulation
  - Vertex operations
  - Normal calculations
  - UV mapping

- **`jenkhash.py`**: Hash generation
  - String to hash conversion
  - Hash lookup
  - Collision detection

- **`utils.py`**: General utilities
  - File operations
  - Data conversion
  - Validation

### Shared Module (`shared/`)
**Purpose**: Shared utilities across modules

- **`geometry.py`**: Geometric calculations
  - Bounding box operations
  - Transformation matrices
  - Intersection tests

- **`shader_nodes.py`**: Shader node utilities
  - Node creation
  - Connection management
  - Parameter mapping

#### Shader Expression (`shader_expr/`)
- **`compiler.py`**: Expression compiler
- **`expr.py`**: Expression parser
- **`builtins.py`**: Built-in functions

## UI Systems

### Gizmos
**Purpose**: Visual helpers in 3D viewport

#### YDR Gizmos (`ydr/gizmos/`)
- **`lights.py`**: Light visualization
- **`light_manipulators/`**: Interactive light editing

#### YTYP Gizmos (`ytyp/gizmos/`)
- **`extensions.py`**: Extension entity visualization
- **`mlo.py`**: MLO room/portal visualization

### Panels
Organized by module:
- `ydr/ui.py`: Drawable panels
- `yft/ui.py`: Fragment panels
- `ytyp/ui/`: Multiple YTYP panels
- `ymap/ui.py`: Map panels

## Versioning System (`versioning/`)
**Purpose**: Handle project file migrations

- **`versioning_230.py`**: v2.3.0 migrations
- **`versioning_240.py`**: v2.4.0 migrations
- **`versioning_250.py`**: v2.5.0 migrations
- **`versioning_260.py`**: v2.6.0 migrations

Each handles specific schema changes and data migrations.

## Testing Framework (`tests/`)
**Purpose**: Automated testing

- **`conftest.py`**: Test configuration
- **`run.py`**: Test runner
- **`test_*.py`**: Individual test modules
- **`assets/`**: Test data files

## Module Dependencies

### Import Order
1. Core modules (init, properties)
2. CWXML system
3. Tools and shared utilities
4. File format modules
5. UI modules
6. Operators

### Key Relationships
- All format modules depend on CWXML
- UI modules depend on properties
- Operators depend on format modules
- Gizmos depend on properties and UI

## Best Practices

### When Adding New Modules
1. Follow existing naming conventions
2. Place in appropriate directory
3. Add to auto_load if needed
4. Include proper docstrings
5. Add unit tests

### Module Structure
```python
# Standard header with license
# Imports (Blender first, then Sollumz)
# Constants and configuration
# Main classes/functions
# Registration functions (if needed)
```