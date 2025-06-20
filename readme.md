# PCLBind

**⚠️ Work In Progress - Not Ready for Use**

High-performance Python bindings for the Point Cloud Library (PCL) using nanobind.

## Overview

PCLBind provides Python bindings for PCL's geometry fitting capabilities, focusing on RANSAC-based model fitting for planes, circles, and cylinders. This project uses nanobind for superior performance compared to traditional binding approaches.

## Status

🚧 **Currently in development** - This project is in the early planning and setup phase.

### Planned Features
- Zero-copy NumPy integration for point cloud data
- RANSAC-based plane, circle, and cylinder fitting
- Template-driven code generation system
- Cross-platform support (Windows/WSL2)
- High-performance nanobind-based bindings

### Target PCL Modules
- `pcl_common` - Core data structures
- `pcl_sample_consensus` - Model fitting algorithms  
- `pcl_io` - Point cloud I/O
- `pcl_search` - Spatial search operations

## Development Environment

- **Python**: 3.13 (miniconda env `fovea`)
- **PCL**: 1.15.0
- **Binding Framework**: nanobind
- **Platform**: Windows/WSL2

## Contributing

This project is in active development. Please see [plan.md](plan.md) for detailed implementation strategy and [CLAUDE.md](CLAUDE.md) for development guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.