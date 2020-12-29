# Specialized Storage Paradigms

- Blobstore - blob (binary large object) - some arbitrary piece of unstructured data; does not make sense to store in tabular format; specializes in storing massive amounts of unstructured data
  - GCS (Google Cloud Storage)
  - S3
- Time Series Database - specializes in storing data with respect to time - monitoring, high-frequency trading, telemetry data; InfluxDB, Prometheus, kdb
- Graph Database - a db that is built on top of the graph data model; concepts with alot of relationships; most popular is Neo4j
- Spatial DB - optimized for storing spatial data (locations on a map)
  - indexing is optimized for spatial data; quadtree, etc.
    - quadtree - a binary tree but with 4 or no child nodes - grid representation
