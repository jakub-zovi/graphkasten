---
tags:
  - cs
  - cs/data_eng
created: 2024-10-06T10:54
modified: 2026-07-26T13:24
published:
sources:
topics:
  - Data Lake
  - Data Storage Architectures
  - Delta Lake
authors:
ai-assisted:
hidden:
public: true
---
# Data Lake
**Wikipedia Definition:**
	A **data lake** is a system or [repository of data](https://en.wikipedia.org/wiki/Data_repository "Data repository") stored in its natural/raw format, usually object [blobs](https://en.wikipedia.org/wiki/Binary_large_object "Binary large object") or files. A data lake is usually a single store of data including raw copies of source system data, sensor data, social data etc.
	James Dixon, then chief technology officer at [Pentaho](https://en.wikipedia.org/wiki/Pentaho "Pentaho"), coined the term by [2011](https://en.wikipedia.org/wiki/Data_lake#cite_note-woods2011-4) to contrast it with [[Data Mart]](https://en.wikipedia.org/wiki/Data_mart).
### Pros:
- **Flexible data storage**
- **Streaming support**
- **Cost efficient in the cloud**
- **Support for AI and Machine Learning**
### Cons:
- **No transactional support**
- **Poor data reliability**
- **Slow analysis performance**
- **Data governance concerns**
- **Data warehouses still needed**

## Data Lake Issues
Issues of data lake that are solved by using [[Delta Lake]]:
- Lack of ACID transaction support
- Lack of schema enforcement
- Lack of integration with a data catalog
- Ineffective partitioning
- Too many small files
Poorly-managed data lakes have been facetiously called [[Data Swamps]].
