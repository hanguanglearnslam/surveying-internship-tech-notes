# Surveying Data Workflow

  ## Background

  Surveying and geospatial engineering projects usually involve multiple types of spatial data, such as UAV images,
  remote sensing images, point clouds, DEM/DSM products, vector data, and 3D models.

  In real engineering workflows, technical support is not only about using software tools. It also requires
  understanding how data is collected, organized, checked, processed, delivered, and integrated into GIS or 3D
  geospatial platforms.

  This document summarizes a general surveying data workflow based on internship learning and technical practice. It
  does not contain any confidential project data or internal information.

  ## Workflow Overview

  A typical surveying data workflow can be divided into the following stages:

  ```text
  Data Collection
      ↓
  Data Organization
      ↓
  Coordinate System Check
      ↓
  Data Preprocessing
      ↓
  Quality Inspection
      ↓
  Format Conversion
      ↓
  Platform Integration
      ↓
  Result Delivery
```
  Each stage has its own technical requirements and common problems.

  ## 1. Data Collection

  Surveying data may come from different sensors and platforms.

  Common data sources include:

  - UAV aerial photography
  - Satellite remote sensing images
  - Mobile mapping systems
  - Terrestrial laser scanning
  - Airborne LiDAR
  - GNSS field measurements
  - Existing GIS databases
  - Manual survey records

  Common data types include:

   Data Type                Description                                   Common Formats
  ━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━
   UAV images               Aerial images collected by drones             JPG, TIFF
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   Remote sensing images    Satellite or aerial imagery                   GeoTIFF, TIFF
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   DEM                      Digital Elevation Model                       TIFF, IMG
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   DSM                      Digital Surface Model                         TIFF, IMG
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   DOM                      Digital Orthophoto Map                        GeoTIFF
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   Vector data              Boundaries, roads, parcels, points            SHP, GeoJSON, GeoPackage
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   Point cloud              3D point data from LiDAR or reconstruction    LAS, LAZ, PLY, TXT
  ───────────────────────  ────────────────────────────────────────────  ──────────────────────────
   3D model                 Mesh or tiled 3D model                        OSGB, OBJ, 3D Tiles

  ## 2. Data Organization

  Before processing, data should be organized clearly. Poor data organization can cause missing files, repeated files,
  wrong versions, and delivery errors.

  A recommended folder structure is:

  project_name/
    raw_data/
      images/
      point_cloud/
      vector/
      control_points/
    processed_data/
      dom/
      dem/
      dsm/
      point_cloud_cleaned/
      model_3d/
    platform_data/
      tiles/
      map_services/
      3d_services/
    documents/
      data_description.md
      quality_check_report.md
      delivery_checklist.md

  Important checks:

  - Are all required files included?
  - Are file names consistent?
  - Are folder names readable?
  - Are raw data and processed data separated?
  - Is there a document explaining the data source and processing steps?
  - Are old versions and final versions clearly distinguished?

  ## 3. Coordinate System Check

  Coordinate system problems are very common in surveying and GIS projects.

  Typical issues include:

  - Missing projection information
  - Wrong coordinate system
  - Mixed coordinate systems
  - Incorrect unit settings
  - Offset between raster, vector, and 3D data
  - Confusion between geographic coordinates and projected coordinates

  Recommended checks:

  - Check whether projection files exist.
  - Confirm EPSG code or local coordinate system definition.
  - Compare data with known reference layers.
  - Check whether units are meters or degrees.
  - Verify whether vector, raster, point cloud, and 3D model data align correctly.

  Example checklist:

  [ ] Projection information exists
  [ ] Coordinate system is confirmed
  [ ] Unit is confirmed
  [ ] Data aligns with reference layer
  [ ] Raster and vector data align
  [ ] Point cloud and imagery align
  [ ] 3D model position is reasonable

  ## 4. Data Preprocessing

  Different data types require different preprocessing steps.

  ### Raster and Remote Sensing Images

  Possible preprocessing tasks:

  - Image format conversion
  - Image clipping
  - Mosaic generation
  - Resolution checking
  - NoData value checking
  - Coordinate system correction
  - Image pyramid generation

  ### Vector Data

  Possible preprocessing tasks:

  - Attribute table cleaning
  - Geometry validity check
  - Duplicate feature removal
  - Coordinate system transformation
  - Layer classification
  - Field name standardization

  ### Point Cloud Data

  Possible preprocessing tasks:

  - Format conversion
  - Noise removal
  - Point density check
  - Coordinate alignment
  - Ground and non-ground classification
  - Data tiling
  - File size reduction

  ### 3D Model Data

  Possible preprocessing tasks:

  - Model format conversion
  - Texture checking
  - Coordinate alignment
  - Model simplification
  - Tile generation
  - Level-of-detail optimization
  - Web visualization preparation

  ## 5. Quality Inspection

  Quality inspection is one of the most important stages in surveying data workflows.

  Common quality problems include:

  - Missing files
  - Wrong file names
  - Incomplete folders
  - Coordinate offset
  - Broken geometries
  - Empty attribute fields
  - Image distortion
  - Point cloud noise
  - Model holes
  - Texture loss
  - Extremely large file size
  - Platform loading failure

  A simple quality inspection table:

   Check Item                Description                              Result
  ━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━
   File completeness         Required files are included              To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Naming consistency        File and folder names follow rules       To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Coordinate system         Projection and units are correct         To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Data alignment            Layers align correctly                   To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Attribute completeness    Key fields are not empty                 To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Visualization             Data can be opened and displayed         To be checked
  ────────────────────────  ───────────────────────────────────────  ───────────────
   Platform loading          Data can be loaded by GIS/3D platform    To be checked

  ## 6. Format Conversion

  Format conversion is often required before data can be used by different software tools or platforms.

  Common examples:

   Original Format    Target Format        Purpose
  ━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   SHP                GeoJSON              WebGIS visualization
  ─────────────────  ───────────────────  ────────────────────────────
   GeoTIFF            tiled map service    Web map publishing
  ─────────────────  ───────────────────  ────────────────────────────
   LAS / LAZ          PLY / TXT            Point cloud processing
  ─────────────────  ───────────────────  ────────────────────────────
   OSGB               3D Tiles             Web-based 3D visualization
  ─────────────────  ───────────────────  ────────────────────────────
   OBJ                3D Tiles             Platform integration
  ─────────────────  ───────────────────  ────────────────────────────
   CSV                SHP / GeoJSON        Spatial data conversion

  Important notes:

  - Always keep original data unchanged.
  - Record conversion tools and parameters.
  - Check coordinate system after conversion.
  - Compare converted data with original data.
  - Avoid repeated conversion that may reduce quality.

  ## 7. Platform Integration

  After processing, data may need to be integrated into GIS or 3D platforms.

  Common platform-related tasks include:

  - Data upload
  - Map service publishing
  - Layer configuration
  - 3D model loading
  - Attribute query testing
  - Permission setting
  - Visualization testing
  - Performance testing

  Questions to ask during platform integration:

  - What data format does the platform support?
  - Is preprocessing required before upload?
  - Does the platform use a specific coordinate system?
  - How are map services or 3D services published?
  - Can the data be queried and visualized correctly?
  - Does the platform load large data smoothly?
  - Are there any permission or access-control requirements?

  ## 8. Result Delivery

  Final delivery should include both data and documentation.

  A typical delivery package may include:

  delivery_package/
    final_data/
    documents/
      data_description.md
      quality_check_report.md
      processing_workflow.md
      delivery_checklist.md
    examples/
      screenshots_or_public_demo_outputs/

  Delivery checklist:

  [ ] Final data files are complete
  [ ] Folder structure is clear
  [ ] Data formats are documented
  [ ] Coordinate system is documented
  [ ] Processing workflow is documented
  [ ] Quality inspection has been completed
  [ ] Platform loading has been tested
  [ ] No confidential or unrelated files are included

  ## Common Problems

  ### 1. Coordinate Offset

  Possible causes:

  - Wrong projection
  - Missing projection file
  - Mixed coordinate systems
  - Unit mismatch
  - Incorrect transformation parameters

  Possible solutions:

  - Check projection metadata.
  - Compare with reference data.
  - Confirm coordinate system with project documentation.
  - Reproject data if necessary.

  ### 2. Missing or Incomplete Files

  Possible causes:

  - Manual copying error
  - Incorrect folder structure
  - Version confusion
  - Incomplete export

  Possible solutions:

  - Use a delivery checklist.
  - Generate file inventory automatically.
  - Compare required files with actual files.
  - Keep raw data and processed data separated.

  ### 3. Large File Size

  Possible causes:

  - High-resolution imagery
  - Dense point cloud
  - Detailed 3D model
  - No tiling or compression

  Possible solutions:

  - Use tiling.
  - Generate image pyramids.
  - Simplify 3D models.
  - Compress point clouds.
  - Use platform-friendly formats.

  ### 4. Platform Loading Failure

  Possible causes:

  - Unsupported format
  - Wrong coordinate system
  - Missing texture files
  - File path problems
  - Data size too large

  Possible solutions:

  - Check platform format requirements.
  - Test with a small sample first.
  - Verify relative paths and texture files.
  - Convert data into supported formats.
  - Optimize file size before publishing.

  ## Possible Automation

  Many repetitive tasks in surveying data workflows can be automated.

  Potential automation tools:

  - File inventory generator
  - Folder structure checker
  - File naming checker
  - Delivery checklist generator
  - Coordinate metadata extractor
  - Batch format conversion script
  - Log summary tool
  - Data completeness checker

  Example automation idea:

  Input: A project folder
  Process:
    - Scan all files
    - Count file types
    - Calculate file sizes
    - Check required folders
    - Export a CSV report
  Output: file_inventory.csv

  This type of tool can reduce repetitive manual checking and make technical support more efficient.

  ## Research Connections

  This workflow is related to several research directions in surveying and geospatial science:

  - Photogrammetry
  - Remote sensing
  - Point cloud processing
  - 3D reconstruction
  - SLAM
  - Geospatial artificial intelligence

  Engineering workflows can also inspire research questions, such as:

  - How to automatically detect errors in geospatial data?
  - How to improve 3D model quality inspection?
  - How to optimize large-scale point cloud processing?
  - How to integrate photogrammetry and AI-based reconstruction?
  - How to build efficient pipelines for web-based 3D geospatial visualization?

  ## Summary

  A complete surveying data workflow is not only about operating software. It requires understanding data sources,
  coordinate systems, preprocessing, quality inspection, format conversion, platform integration, and final delivery.

  For an internship, the most important goal is to move from simple technical support to workflow understanding. By
  documenting real engineering processes, identifying repeated tasks, and building small automation tools, technical
  support work can become valuable preparation for both future employment and doctoral research.
