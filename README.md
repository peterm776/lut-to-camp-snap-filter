
[**Live Demo**]([https://peterm776.github.io/lut-to-campsnap/])

This is a powerful, browser-based tool for converting industry-standard `.cube` 3D Look-Up Tables (LUTs) into the `.flt` format used by CampSnap digital cameras.

The goal of this converter is to produce the most mathematically accurate and visually faithful `.flt` file possible by modeling the complex, non-linear color transformations of a `.cube` file into the matrix and 1D curve structure of the `.flt` format.

## How to Use

The converter is designed to be simple and powerful.

1. **Upload `.CUBE` File:** Click the first box to select the `.cube` LUT you wish to convert. The conversion process will begin automatically.

2. **Upload Preview Image (Optional):** Click the second box to select a photo. This will display a before-and-after comparison, allowing you to visually verify the accuracy of the conversion.

3. **Download:** Once the analysis is complete, a "Download .FLT File" button will appear. Click it to save your new camera-ready file.

## The Conversion Engine: How It Works

Simply converting a 3D LUT to a 1D format by sampling a grayscale ramp can lead to inaccurate colors, as it misses crucial information (e.g., how reds affect cyans, or how yellows are desaturated). This tool uses a much more sophisticated approach for a more faithful conversion.

1. **Full-Spectrum Analysis:** Instead of a simple grayscale ramp, the engine generates a comprehensive internal color chart containing thousands of unique color values. This chart includes gradients for all primary (RGB) and secondary (CMY) colors.

2. **True Color Matrix Calculation:** The engine performs a linear algebra regression (`Least-Squares Fit`) to calculate the ideal **3x3 color matrix**. This matrix accurately represents the linear components of the color grade, such as changes in brightness, contrast, and overall color balance.

3. **Non-Linear Residual Modeling:** After accounting for the linear changes, the engine calculates the "residual" color transformation—the complex, non-linear adjustments that the matrix cannot represent. This crucial remaining data is modeled into a highly precise set of 1D curves.

4. **Combined Output:** The final `.flt` file contains **both** the calculated color matrix and the specialized residual curves. This two-part approach ensures the most robust and faithful conversion possible, preserving the unique character of the original `.cube` file.

5. **Web Worker Performance:** To ensure the user interface remains smooth and responsive, the entire computationally-intensive analysis is performed on a background thread using a `Web Worker`.

## Technology

This project is built with modern, client-side web technologies.

* **HTML5/CSS3/JavaScript:** The core of the application.

* **Tailwind CSS:** For modern and responsive styling.

* **Web Workers:** For offloading heavy computations from the main UI thread, preventing the browser from freezing during analysis.

* **No Server-Side Dependencies:** This is a fully client-side application. All processing happens securely in the user's browser.

## License

This project is open source and available under the [MIT License](https://opensource.org/licenses/MIT).
