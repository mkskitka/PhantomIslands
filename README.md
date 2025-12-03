# Phantom Islands — Setup & Usage Guide

This document explains how to set up and run the **Phantom Islands** project using **TouchDesigner** and **ComfyUI Portable**. It also details the configuration settings available in the project.

---

## **1. Requirements**

To run the project you will need:

* **TouchDesigner** (latest stable build recommended)
* **The project file:** `phantomislands.[highest_value].toe`
* **ComfyUI Portable** installed and running on your machine

---

## **2. Project Setup**

### **Step 1 — Install & Launch ComfyUI Portable**

1. Download the latest **ComfyUI Windows Portable** build.
2. Extract it to a location on your computer.
3. Launch it using `python main.py` or other command, depending on your system.
4. Keep ComfyUI running while using the Phantom Islands project.
5. Copy API/ folder into ComfyUI_windows_portable\ComfyUI. This folder contains the ComfyUI workflow json files that are used.

> **Note:** The path to your ComfyUI installation must match the configuration value in the TouchDesigner project. More on this in configuraiton section of README.

---

### **Step 2 — Open the TouchDesigner Project**

1. Open **TouchDesigner**.
2. Load the project file: `phantomislands.[highest_value].toe`. Highiest value to be replaced with highiest build number for the project.

Inside the network, locate the **Scripts** section at the top left of the network.
There you’ll find the **`PhantomIsland`** component — this is where configuration settings can be edited.

---

## **3. Running Workflows**

The Phantom Islands project uses keyboard input to trigger different ComfyUI workflows.

### **Available Key Controls**

* **Press `1`** — Runs the **regular ComfyUI canny workflow**.
* **Press `3`** — Runs the **inpainting workflow**.

Make sure ComfyUI is running before triggering any workflows. You must have touch designer GUI in focus to use keyboard commands. 

---

## **4. Configuration Settings**

Inside the `PhantomIsland` component (Scripts section), you may edit configuration parameters that determine how frames, images, and prompts are generated.

Below is an explanation of each configuration setting:

### **General**

#### `self.Comfy_path`

Path to your ComfyUI Portable installation.

* Example:

  * `C:/ComfyUI_windows_portable`
* This must point to the root folder of ComfyUI.

---

### **Image Sources**

These specify which image inputs are used at different stages of generation.

#### `self.Start_image`

The **first input image** used when beginning a sequence.

* Typically set to: `COLLAGE`

#### `self.Keyframe_image`

The image used for **keyframes**.

* Determines the start of major transitions.

#### `self.Interp_image`

The image used for **intermediate (in-between) frames**.

* Helps interpolate between keyframes.

---

### **Prompt System**

#### `self.Story`

Name of the **DAT table** that contains the prompts for each keyframe.

* Each **row** = one keyframe prompt
* Changing this DAT changes the narrative or concept.

#### `self.prompt_iterations`

Controls how many in-between frames are generated between keyframes.

* **1** — all keyframes only (no in-between frames)
* **2** — 1 keyframe + 1 interpolated frame
* **3** — 1 keyframe + 2 interpolated frames

---

### **Animation & Zoom Controls**

#### `self.zoomFactor`

Controls zoom applied each frame.

* `0` = no zoom
* `1` = doubles the zoom per frame
* Values between 0–1 allow partial zoom steps.

#### `self.zoom_frames`

Number of frames used to zoom **in** and **out**.

* Higher values = slower, smoother zoom

---

### **Canny Collage Behavior**

#### `self.grow_canny`

Controls how the Canny collage evolves over time.

* **True** — the collage *grows* outward over time
* **False** — the collage fills in the island shape instead of expanding

---

## **5. Editing Configuration**

To edit any settings:

1. Enter the `PhantomIsland` component.
2. Open the **python script** inside.
3. Modify the values under the **CONFIGURATION** section.

Changes take effect immediately when the next workflow is triggered.

---

## **6. Notes & Tips**

* Always start **ComfyUI before TouchDesigner** if you plan to trigger workflows.
* If a workflow doesn’t run, verify:

  * The correct ComfyUI path in `self.Comfy_path`.
  * ComfyUI is actively running.
  * Your prompts DAT table exists and is named correctly.
* Pressing keys multiple times quickly may queue multiple workflow triggers.

---

If you need additional sections (installation troubleshooting, presets, workflow diagrams, etc.), just let me know and I can expand this README.
