# Sollumz Developer Guide

## Getting Started

### Development Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Sollumz/Sollumz.git
   cd Sollumz
   ```

2. **Install in Blender (Development Mode)**
   - Create symbolic link from Blender addons folder to your dev folder
   - Or use Blender's "Install from file" and select the folder
   - Enable "Developer Extras" in Blender preferences

3. **Enable Debug Mode**
   - In Blender: Edit → Preferences → Add-ons → Sollumz
   - Check "Enable debug mode"
   - This enables additional logging and debug tools

### Project Structure

```
Sollumz/
├── __init__.py           # Entry point, addon registration
├── auto_load.py          # Module auto-discovery
├── sollumz_*.py          # Core modules
├── cwxml/                # XML parsing/generation
├── shared/               # Shared utilities
├── tools/                # Helper functions
├── ydr/, yft/, etc.      # Format-specific modules
└── tests/                # Unit tests
```

## Architecture Principles

### 1. **Separation of Concerns**
- Each file format has its own module
- UI code separate from logic
- Import/export in dedicated files

### 2. **Blender Integration**
- Use Blender's property system
- Follow Blender's operator patterns
- Respect Blender's data model

### 3. **CodeWalker Compatibility**
- Maintain XML schema compatibility
- Preserve all data during round-trips
- Handle version differences gracefully

## Core Concepts

### Property Groups

Properties are defined using Blender's property system:

```python
class MyProperties(bpy.types.PropertyGroup):
    my_int: bpy.props.IntProperty(
        name="My Integer",
        description="An integer value",
        default=0,
        min=0,
        max=100
    )
    
    my_enum: bpy.props.EnumProperty(
        name="My Enum",
        items=[
            ("OPT1", "Option 1", "First option"),
            ("OPT2", "Option 2", "Second option"),
        ]
    )
```

### Operators

Operators perform actions:

```python
class SOLLUMZ_OT_my_operator(bpy.types.Operator):
    bl_idname = "sollumz.my_operator"
    bl_label = "My Operator"
    bl_description = "Does something"
    
    def execute(self, context):
        # Operator logic here
        return {'FINISHED'}
```

### UI Panels

Panels provide UI:

```python
class SOLLUMZ_PT_my_panel(bpy.types.Panel):
    bl_label = "My Panel"
    bl_idname = "SOLLUMZ_PT_my_panel"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_category = "Sollumz"
    
    def draw(self, context):
        layout = self.layout
        layout.operator("sollumz.my_operator")
```

## Adding New Features

### 1. Adding a New Property

1. Define in appropriate property group
2. Add UI in relevant panel
3. Handle in import/export code
4. Add versioning if changing existing data

### 2. Adding a New File Format

1. Create new module directory
2. Add `__init__.py` with registration
3. Create import/export files
4. Add CWXML structures
5. Create operators and UI
6. Add tests

### 3. Adding a New Tool

1. Create operator class
2. Add to appropriate menu/panel
3. Document usage
4. Add icon if needed

## Code Style Guidelines

### Python Style
- Follow PEP 8
- Use type hints where helpful
- Document complex functions
- Keep functions focused

### Naming Conventions
- **Classes**: `SOLLUMZ_OT_operator_name` (operators)
- **Properties**: `snake_case`
- **Constants**: `UPPER_CASE`
- **UI Labels**: "Title Case"

### Blender Conventions
- Operators: `bl_idname = "sollumz.operator_name"`
- Panels: `bl_idname = "SOLLUMZ_PT_panel_name"`
- Property Groups: Suffix with `Properties`

## Testing

### Running Tests
```bash
# From Sollumz directory
python -m pytest tests/
```

### Writing Tests
```python
def test_my_feature(sollumz_game_assets):
    # Arrange
    obj = create_test_object()
    
    # Act
    result = my_function(obj)
    
    # Assert
    assert result.expected_value == 42
```

### Test Assets
- Place in `tests/assets/`
- Use minimal examples
- Document expected behavior

## Debugging

### Enable Debug Logging
```python
from .logger import logger
logger.debug("Debug message")
logger.info("Info message")
logger.warning("Warning message")
```

### Debug Tools
- Sollumz Debug panel
- Blender's Python console
- VS Code with Blender extension

### Common Issues
1. **Registration Errors**: Check class naming
2. **Import Failures**: Validate XML structure
3. **Property Updates**: Use update callbacks
4. **Performance**: Profile with cProfile

## CWXML System

### Adding XML Support
```python
class MyElement(Element):
    tag_name = "MyElement"
    
    def __init__(self):
        super().__init__()
        self.my_attr = AttributeProperty("myAttr", default=0)
        self.child = ElementProperty("Child", ChildElement)
```

### Parsing XML
```python
with open(filepath) as f:
    root = MyElement.from_xml_file(f)
```

### Generating XML
```python
element = MyElement()
xml_string = element.to_xml_string()
```

## Best Practices

### 1. **Error Handling**
```python
try:
    risky_operation()
except SpecificError as e:
    logger.error(f"Operation failed: {e}")
    self.report({'ERROR'}, str(e))
    return {'CANCELLED'}
```

### 2. **User Feedback**
```python
self.report({'INFO'}, "Operation completed successfully")
self.report({'WARNING'}, "Check the result")
self.report({'ERROR'}, "Operation failed")
```

### 3. **Performance**
- Cache expensive calculations
- Use Blender's update system
- Batch operations when possible
- Profile before optimizing

### 4. **Compatibility**
- Check Blender version
- Handle missing features gracefully
- Provide migration paths
- Document breaking changes

## Contributing

### Before Submitting
1. Run all tests
2. Check code style
3. Update documentation
4. Test in Blender

### Pull Request Process
1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit PR with description
5. Address review feedback

### Commit Messages
```
feat: Add new feature
fix: Fix specific bug
docs: Update documentation
refactor: Restructure code
test: Add/update tests
```

## Resources

### Documentation
- [Blender Python API](https://docs.blender.org/api/current/)
- [CodeWalker Formats](https://github.com/dexyfex/CodeWalker)
- [GTA V Research](https://gtamods.com/wiki/Main_Page)

### Tools
- [Blender Development](https://developer.blender.org/)
- [VS Code Blender Extension](https://marketplace.visualstudio.com/items?itemName=JacquesLucke.blender-development)
- [Blender Addon Tester](https://github.com/nangtani/blender-addon-tester)

### Community
- [Sollumz Discord](https://discord.sollumz.org/)
- [GitHub Issues](https://github.com/Sollumz/Sollumz/issues)
- [Wiki](https://docs.sollumz.org/)