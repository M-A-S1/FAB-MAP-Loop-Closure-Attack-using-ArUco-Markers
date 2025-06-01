# FAB-MAP-Loop-Closure-Attack-using-ArUco-Markers# 🔁 FAB-MAP Loop Closure Attack using ArUco Markers

This project demonstrates a successful spoofing of the [original FAB-MAP](https://www.robots.ox.ac.uk/~mobile/FABMAP/) loop closure algorithm by injecting visually similar artificial landmarks (ArUco markers) to induce a **false loop closure** detection. 

By manipulating visual input, we tricked FAB-MAP into believing that two different locations were the same — a critical failure case in SLAM systems.

## 📌 Objective

To evaluate the robustness of FAB-MAP against synthetic landmarks and explore its vulnerabilities in visually ambiguous environments.

---

## 🧪 Setup

- **SLAM Backend:** Original FAB-MAP implementation (OpenFABMAP)
- **Spoofing Tool:** ArUco markers from OpenCV
- **Dataset:** Custom video feed or image sequence
- **Output Analysis Tool:** MATLAB (for matrix inspection)

---

## 🚨 Spoofing the Loop Closure

By placing identical ArUco markers in two different, non-overlapping environments, we were able to:

- Trigger a **false loop closure**
- Force FAB-MAP to incorrectly relocalize and merge topologically distinct locations

---

## 📷 False Positive Example

Below are two different input frames where the loop closure was **falsely** detected:

### 🔹 Image A (Original Location)

![Image A](images/false_loop_a.jpg)

### 🔹 Image B (Fake Location with ArUco Marker)

![Image B](images/false_loop_b.jpg)

Despite being same places, FAB-MAP incorrectly identified these as the different location.

---

## 📊 MATLAB Output Matrix

Here is the portion of the FAB-MAP likelihood matrix showing the false loop closure:

```matlab
% Simplified view of the FAB-MAP output likelihoods (log probabilities)
% Rows and columns represent image indices in the sequence

% Example: High value represented by yellow color at (4, 14) suggests loop closure between image 4 and 14
loopClosureMatrix = [
    ... 
    0.0012  0.0008  0.0007  ...
    0.0004  0.9501  0.0006  ...
    0.0003  0.0005  0.9702  ...
    ...
];
```
📌 Note: The high likelihood between mismatched images was induced due to visually identical ArUco marker patterns.

## 🔁 How to Reproduce
Clone the original FAB-MAP and this repo

Insert ArUco markers into separate environments

Run the image sequence through FAB-MAP

Analyze the *.mat output or visualize loop closures


##⚠️ Observations & Implications
FAB-MAP is vulnerable to visual spoofing via structured artificial landmarks

ArUco markers (being highly distinctive) are wrongly treated as environmental features

This can severely affect pose graph optimization and global consistency

## 🧠 Future Work
Integrate semantic or geometric checks before accepting loop closures

Augment FAB-MAP with a second validation layer (e.g., depth, spatial layout)


## 📜 License
This project is released under the MIT License.

## 🙋‍♂️ Author
Muhammad Ali — [(https://github.com/M-A-S1)]

