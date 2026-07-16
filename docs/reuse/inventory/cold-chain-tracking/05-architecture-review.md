2-layer architecture: (1) OpenBoxes tracks which stock items require
cold-chain storage and their designated storage location/alert
thresholds at the inventory-record level; (2) actual sensor telemetry
ingestion (temperature-logger hardware integration) is platform-owned
BUILD, reusing Module 4's `device-protocol-adapters` pattern (per-vendor
adapter, since no product exists per-sensor-vendor by definition — the
same finding class already established there) rather than a dedicated
cold-chain IoT product, none of which survived verification.
