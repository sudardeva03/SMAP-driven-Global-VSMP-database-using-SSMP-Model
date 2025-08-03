# SMAP-driven-Global-VSMP-database-using-SSMP-Model
The Vertical Soil Moisture Profile (VSMP) is a developed database consisting of soil moisture estimated at depths of 10 cm, 20 cm, 51 cm, and 102 cm beneath the surface. The estimates are derived using SMAP surface soil moisture data and a Statistical Soil Moisture Profile model that captures the spatial heterogeneity of the soil system.
## 📁 Data Structure

Each `.zip` file contains 8 annual `.h5` files:

| ZIP Filename              | Depth   | Contents                                      |
|---------------------------|---------|-----------------------------------------------|
| `Global_VSMP_10cm.zip`    | 10 cm   | `Global_VSMP_10cm_2015.h5` to `..._2022.h5`   |
| `Global_VSMP_20cm.zip`    | 20 cm   | `Global_VSMP_10cm_2015.h5` to `..._2022.h5`   |
| `Global_VSMP_51cm.zip`    | 51 cm   | `Global_VSMP_10cm_2015.h5` to `..._2022.h5`   |
| `Global_VSMP_102cm.zip`   | 102 cm  | `Global_VSMP_10cm_2015.h5` to `..._2022.h5`   |

Each `.h5` file contains a 3D dataset called **`combined`**, with the following dimensions:

| Dimension     | Size  | Description                            |
|---------------|-------|----------------------------------------|
| Latitude      | 2288  | From 83.5°N to 73.5°S                  |
| Longitude     | 5086  | From -179° to 179°                     |
| Time (daily)  | 2557  | Daily values from **June 1, 2015** to **June 1, 2022** (inclusive) |

- Units: **Volumetric water content (m³/m³)**
- Total time steps: **2557 days**
- Spatial resolution: **9 km × 9 km**

## 🧪 Sample Python Code to Read Files

```python
import h5py
import numpy as np

file_path = 'Global_VSMP_10cm_2015.h5'

with h5py.File(file_path, 'r') as f:
    print("Datasets:", list(f.keys()))  # Should list 'combined'
    data = f['combined'][:]  # Shape: (2288, 5086, 365 or 366)
    print("Data shape:", data.shape)
    
