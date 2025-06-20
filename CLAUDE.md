# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a PCL (Point Cloud Library) Python bindings generation project using nanobind for high-performance C++ to Python bindings. The project focuses on geometry fitting capabilities (planes, circles, cylinders) as the MVP scope.

## Development Environment

**Required Environment**: miniconda env `fovea` with Python 3.13

```bash
# Activate development environment
conda activate fovea

# Install core dependencies when implementing
pip install cxxheaderparser nanobind numpy pyyaml inflection pytest
```

## Technology Stack Architecture

### Code Generation Pipeline
- **Header Parser**: cxxheaderparser for parsing PCL C++ headers
- **Binding Generator**: nanobind (chosen over pybind11 for performance)
- **Template Management**: YAML-driven template instantiation system
- **Target PCL Version**: 1.15.0

### Key PCL Path Configuration (WSL2)
- Windows PCL: `/mnt/c/Program Files/PCL 1.15.0`
- Include headers: `/mnt/c/Program Files/PCL 1.15.0/include/pcl-1.15`
- Libraries: `/mnt/c/Program Files/PCL 1.15.0/lib`

## Planned Directory Structure

```
generators/                    # Code generation system
├── config.py                 # Generation configuration
├── point_types.yml           # Point type definitions  
├── modules.yml               # PCL module configuration
├── parser.py                 # Header parsing logic
└── generator.py              # Binding code generation

src/
├── pclbind/                  # Generated binding code
└── nanobind_extensions/      # Custom nanobind utilities

tests/
├── unit/                     # Unit tests
├── integration/              # Integration tests
└── fixtures/                 # Test data

scripts/
├── generate_bindings.py      # Main generation script
├── build_windows.py          # Windows build automation
└── validate_installation.py  # Installation verification
```

## MVP Target Functionality

### Core PCL Modules for Bindings
- `pcl_common` - Core data structures (PointCloud<T>, point types)
- `pcl_sample_consensus` - RANSAC-based model fitting
- `pcl_io` - Point cloud I/O operations  
- `pcl_search` - Spatial search operations

### Essential Classes to Bind
- `PointCloud<T>` with NumPy integration (zero-copy)
- `SACSegmentation<T>` - Main segmentation class
- `RandomSampleConsensus<T>` - RANSAC algorithm
- `ModelCoefficients` and `PointIndices` - Output structures

### Point Types for Template Instantiation
- `PointXYZ`, `PointXYZI`, `PointXYZRGB`, `PointNormal`

## Development Commands

```bash
# Environment setup
conda activate fovea

# Code generation (when implemented)
python scripts/generate_bindings.py

# Build system (when implemented)
mkdir build && cd build
cmake ..
make

# Testing (when implemented)
pytest tests/unit/
pytest tests/integration/
python scripts/validate_installation.py
```

## Cross-Platform Development Notes

- Always provide both Windows and WSL versions for scripts
- Handle Windows/WSL2 path differences in build configuration
- PCL dependencies managed through Windows PCL installer
- Use atomic git commits for all changes

## Critical Implementation Considerations

### Template Complexity Management
- Use YAML configuration files for template instantiations
- Implement exclusion lists for problematic templates
- Build dependency graphs for template instantiation order

### Memory Management
- Implement zero-copy NumPy integration for point cloud data
- Use proper nanobind memory policies
- Ensure proper C++/Python memory ownership handling

### NumPy Integration Pattern
- `from_array()` methods for creating point clouds from NumPy arrays
- `to_array()` methods for exporting point cloud data
- Buffer protocol implementation for direct memory access

## Build System Configuration

### CMake Integration
```cmake
find_package(PCL 1.15 REQUIRED COMPONENTS common sample_consensus io search)
find_package(nanobind REQUIRED)
target_link_libraries(pclbind PRIVATE ${PCL_LIBRARIES})
```

### Python Package Setup
- Use `setup.py` with nanobind integration
- Include proper dependency management for PCL libraries
- Configure wheel building for cross-platform distribution