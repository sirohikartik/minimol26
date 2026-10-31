# Problem Statement: HiveNet — Distributed Edge Cloud Storage & Smart Router

## Objective
Build a decentralized, peer-to-peer cloud storage standalone application (**HiveNet**) where multiple connected devices (smartphones/laptops) pool their local filesystem storage into a unified, serverless cloud drive.

Users can upload photos/images from any device. Every image must be **compressed on the client app**, and an intelligent **storage router** must dynamically dispatch the image (or chunks) to the most optimal phone currently connected to the hive net.

---

## Technical Stack: Standalone Apps Only
* **Runtime Mandate:** **Strictly Standalone Applications (No Web Browsers).** 
  * Solutions must be built as an installable/runnable app on mobile or desktop.
* **Framework Freedom:** Any app framework of your choice:
  * **Cross-Platform Mobile:** Flutter, React Native, Expo, Kotlin Multiplatform.
  * **Native Mobile:** Swift (iOS), Kotlin/Java (Android).
  * **Desktop / Cross-Platform:** Tauri, Electron, Native C++/Rust/Go GUI.
* **Storage Target:** Native device filesystem / disk storage (e.g. app documents directory, local disk cache, SQLite BLOBs, or raw filesystem I/O).

---

## Core System Architecture & Router Mandate

```
[ Device A (App): Uploader ]
            │
            ▼
 1. Compress Image (Client App)
            │
            ▼
 2. Query HiveNet Router  ──► "Which node has free disk space, low latency & uptime?"
            │
            ▼
 3. Smart Route & Store (Replication Factor = 2)
            ├─── Chunk 1 / Copy A ──────► [ Device B (App Node 1: Local Disk) ]
            └─── Chunk 2 / Copy B ──────► [ Device C (App Node 2: Local Disk) ]
```

### The Router Decision Engine:
The storage router must **not** blindly store images locally or spam all nodes. When an image is uploaded, the router must evaluate peer telemetry:
1. **Available Device Disk Quota:** Avoid overflowing nodes that are running low on physical disk storage.
2. **Network Proximity / Latency:** Route to nodes with the fastest, most reliable peer connection.
3. **Redundancy (Replication Factor $\ge 2$):** Store redundant copies or parity chunks across at least two distinct peer apps so that if one phone disconnects, data is not lost.

---

## Hard Requirements
1. **Standalone App Execution:** The storage system must run as an installed or running native application on the devices, using native filesystem/disk I/O.
2. **Decentralized Storage:** Images must physically reside on the local storage/disk of the connected peer devices. **No centralized database or cloud storage (no S3, no Firebase).**
3. **Mandatory Client-Side Compression:** Images must be compressed before network transfer (e.g. modern WebP/AVIF compression, native image downscaling, or custom chunk quantization). Raw uncompressed uploads are rejected.
4. **Content-Addressable Retrieval:** Any app on the mesh can view the gallery and retrieve/view any stored image on-demand by requesting it from the host phone across the mesh.
5. **Node Disconnect Resilience:** If one storage node is turned off (airplane mode / app terminated), any image stored on it must still be retrievable from the redundant replica node.

---

## Strictly Prohibited
* **NO Web Browser Implementations:** The app must run as a standalone application, not inside a Safari/Chrome browser tab.
* **NO Central Cloud Storage Buckets:** No AWS S3, Google Cloud Storage, Cloudinary, Firebase Storage, or remote SQL/NoSQL databases holding the image files.
* **NO Uncompressed Blobs:** Uploading raw multi-megabyte PNG/JPEG files over the network without client-side compression.
* **NO Monolithic Single-Phone Storage:** All nodes must participate in the storage pool; a single phone cannot hold 100% of the data while others hold 0%.
