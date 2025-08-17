graph TD
    A[Raw Image (e.g., CK+ dataset image)] --> B(Pre-processing: Grayscale Conversion & Upscaling);

    B --> C{Face Detection (dlib's HOG Detector)};
    C -- Face Bounding Box --> D[Face Region of Interest (ROI)];

    D -- Grayscale ROI --> E[HOG Feature Extraction];

    subgraph HOG Internal Steps
        E1[Resize ROI to Standard Size (e.g., 128x128)] --> E2[Compute Gradients (Magnitude & Orientation)];
        E2 --> E3[Divide into Cells (e.g., 8x8 pixels)];
        E3 --> E4[Calculate Histograms of Orientations per Cell];
        E4 --> E5[Group Cells into Overlapping Blocks (e.g., 2x2 cells)];
        E5 --> E6[Normalize Histograms within Blocks];
        E6 --> E7[Concatenate All Normalized Histograms];
    end

    E --> F[HOG Feature Vector];
    F --> G[Store HOG Features in CSV];

    style A fill:#DDEBF7,stroke:#3366CC,stroke-width:2px,color:#000
    style B fill:#F7FAFC,stroke:#8B008B,stroke-width:2px,color:#000
    style C fill:#F7FAFC,stroke:#8B008B,stroke-width:2px,color:#000
    style D fill:#DDEBF7,stroke:#3366CC,stroke-width:2px,color:#000
    style E fill:#FFF2CC,stroke:#FF8C00,stroke-width:2px,color:#000
    style F fill:#E2EFDA,stroke:#6B8E23,stroke-width:2px,color:#000
    style G fill:#DAEEF3,stroke:#008B8B,stroke-width:2px,color:#000

    style E1 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E2 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E3 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E4 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E5 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E6 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000
    style E7 fill:#FFF2CC,stroke:#FF8C00,stroke-width:1px,color:#000