# Earth observation data configuration files

The use of well-structured configuration files is crucial in the field of Earth Observation (EO) for international development, as these files serve as foundational guides for accessing, interpreting, and analyzing diverse and complex datasets. Configuration files, like those discussed in this thread, provide essential metadata including data sources, spatial and temporal resolutions, coverage, and specific data formats (e.g., GeoTIFF, NetCDF). They also detail the naming conventions of files, which is vital for automated data processing and ensuring consistent data handling across different datasets and time periods.

In contexts like international development, where EO data can inform critical decisions on climate action, disaster response, and resource allocation, these configuration files ensure that analysts, researchers, and decision-makers have a clear, standardized, and accessible way to understand and utilize the data. This not only enhances the efficiency of data analysis processes but also contributes to the accuracy and reliability of insights derived from the data, leading to more informed and effective development interventions.

## Type

Configuration files, such as `.ini`, `.json`, `.yaml`, and `.toml`, play a crucial role in many software and data analysis tasks. Each format has its strengths and weaknesses. Here's a breakdown:

1. **INI**
   
**Strengths:**
* Simple and human-readable.
* Has been used for a long time, especially in Windows environments.
* Lightweight with no nested structures.

**Weaknesses:**
* Doesn't support complex data structures (e.g., lists, nested dictionaries).
* Not standardized; INI parsers might behave differently.
* Less popular for modern applications, especially in the realm of data science and analytics.

2. **JSON (JavaScript Object Notation)**
   
**Strengths:**
* Standardized and widely accepted.
* Supported by most programming languages.
* Supports complex data structures (arrays, nested objects).
* Directly used and interpretable in JavaScript.

**Weaknesses:**
* Less human-readable compared to YAML or INI due to braces, quotes, etc.
* Doesn't support comments natively.

3. **YAML (YAML Ain't Markup Language)**
   
**Strengths:**
* Highly human-readable with a clean format.
* Supports complex data structures.
* Allows comments, which can be beneficial for configuration files.
* Popular in various applications, especially in DevOps (e.g., Docker, Kubernetes).

**Weaknesses:**
* More error-prone (e.g., indentation errors can break parsing).
* Potential security risks if executing dynamic content (always use safe loaders).

4. **TOML (Tom's Obvious, Minimal Language)**
   
**Strengths:**
* Designed to be easy to read due to its clear semantics.
* Supports complex data structures.
* Gaining popularity in certain ecosystems (e.g., Rust's `Cargo.toml`).

**Weaknesses:**
* Not as widely adopted as JSON or YAML.
* Some find its syntax a bit more verbose than that of INI, though it's more expressive.

## Recommendation for Earth Observation Analysis in the Context of Data Science:

Considering our use case, which involves earth observation analysis within Python ecosystem, **YAML** or **JSON** seem like the most fitting choices. Here's why:

* **YAML**: Widely used in the data science community and is very human-readable. Its support for comments can be invaluable in a configuration file where you might want to explain certain choices. Many Python libraries can parse YAML with ease.

* **JSON**: If you anticipate needing to share this configuration with systems or languages where JSON is the default (like web applications or databases), JSON might be more suitable. It's also a bit less prone to user errors than YAML due to its stricter format.

In the end, the best format also depends on the comfort level of your team. If your team is familiar with a particular format, it can be advantageous to stick with it. If starting from scratch, either YAML or JSON would be excellent, with YAML having a slight edge in readability and annotative flexibility.

## Example

Let's create a simple configuration for MODIS data with a focus on NDVI (Normalized Difference Vegetation Index) and EVI (Enhanced Vegetation Index).

**JSON**

```json
{
  "MODIS": {
    "product": "MOD13Q1",
    "description": "16-day 250m vegetation indices",
    "layers": {
      "NDVI": {
        "band_number": 1,
        "description": "Normalized Difference Vegetation Index",
        "scale_factor": 0.0001
      },
      "EVI": {
        "band_number": 2,
        "description": "Enhanced Vegetation Index",
        "scale_factor": 0.0001
      }
    },
    "spatial_resolution": "250m",
    "format": "HDF"
  }
}
```

**YAML**

```yaml
MODIS:
  product: MOD13Q1
  description: 16-day 250m vegetation indices
  layers:
    NDVI:
      band_number: 1
      description: Normalized Difference Vegetation Index
      scale_factor: 0.0001
    EVI:
      band_number: 2
      description: Enhanced Vegetation Index
      scale_factor: 0.0001
  spatial_resolution: 250m
  format: HDF
```

The above configurations provide metadata for the MODIS MOD13Q1 product, detailing the layers available (NDVI and EVI) with associated metadata like band number, description, and a scale factor. It also defines the spatial resolution and file format.

To parse these files using Python:

For JSON:

```python
import json

with open('modis_config.json', 'r') as f:
    config = json.load(f)

ndvi_description = config['MODIS']['layers']['NDVI']['description']
print(ndvi_description)
```

For YAML:

You would need to install PyYAML: `pip install PyYAML`

```python
import yaml

with open('modis_config.yaml', 'r') as f:
    config = yaml.safe_load(f)

ndvi_description = config['MODIS']['layers']['NDVI']['description']
print(ndvi_description)
```

The outputs of the above snippets would both print: `Normalized Difference Vegetation Index`

For the Space2Stats activities, we are agreed to use JSON format as out configuration file.