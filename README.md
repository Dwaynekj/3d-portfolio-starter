# PointFusion3D: 3D Portfolio Starter

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Dwaynekj/3d-portfolio-starter/blob/main/PointFusion3D_student.ipynb)

Build a 3D point-cloud registration pipeline from scratch: take two messy, partial 3D scans of the same object and fuse them into one aligned model. This is the starter notebook for **Reboot × Spatial AI Foundations**, a four-session hands-on intro to 3D computer vision.

You fill in the core algorithms yourself, and the notebook checks your work as you go:

| Part | You build | How you know it works |
|---|---|---|
| 1 | Load a 3D scan and see it as an `(N, 3)` NumPy array | The plot shows the Stanford Bunny |
| 2 | `remove_outliers()`: a KD-tree outlier filter | Prints how many junk points it removed |
| 3 | `find_correspondences()`: nearest-neighbor search | Toy test prints `PASS` |
| 4 | `icp()`: the Iterative Closest Point loop | Scan B snaps onto Scan A |
| 5 | (given) Ground-truth grader | Prints `PASS` within 5° and 2 cm |
| 6 | Run the same code, unchanged, on a real room scan | Prints `PASS` within 5 cm of the true pose |
| 7 | `make_gaussian_seed()`: the first step of a Gaussian splat | Prints the seed's shape and scale range |
| 8–9 | (optional) Your own phone scan, then ship it | Your own repo and resume bullet |
| HW | `sample_points_on_mesh()`: turn a real phone scan of Elmo into a point cloud | Prints `PASS` when points cover the surface evenly |

## Get started

**In Colab (recommended):** click the **Open in Colab** badge above, then **File → Save a copy in Drive** so your work is saved. Run the Setup cell first. It installs Open3D and downloads the data from this repo, which takes about a minute.

**On your own machine:**

```bash
git clone https://github.com/Dwaynekj/3d-portfolio-starter.git
cd 3d-portfolio-starter
pip install -r requirements.txt
jupyter notebook PointFusion3D_student.ipynb
```

Run the cells top to bottom. Cells with `# TODO` are yours to complete. Everything else is given so you can focus on the algorithms.

## What's in the repo

```
PointFusion3D_student.ipynb   the notebook you work in
requirements.txt              Python packages for running locally
data/
  scanA_bunny_partial1.ply           Scan A: partial scan of the Stanford Bunny
  scanB_bunny_partial2_raw.ply       Scan B: second view, rotated, noisy, with outliers
  bunny_known_R.npy, bunny_known_t.npy   the true rotation and translation (Part 5 grader)
  room_fragment_A_downsampled.ply    real RGB-D room scan, fragment A (Part 6)
  room_fragment_B_downsampled.ply    real RGB-D room scan, fragment B (Part 6)
  room_A_to_B.npy                    true 4x4 alignment of the two room fragments (Part 6 grader)
```

The Elmo phone scan for the homework (an 11 MB textured mesh from KIRI Engine) isn't in the repo. The homework cell downloads it from the [`data-elmo-v1` release](https://github.com/Dwaynekj/3d-portfolio-starter/releases/tag/data-elmo-v1).

## Data credits

- **Stanford Bunny:** [Stanford 3D Scanning Repository](https://graphics.stanford.edu/data/3Dscanrep/), Stanford University Computer Graphics Laboratory. Sampled down and split into two partial views for this notebook.
- **Room fragments:** from the Redwood indoor RGB-D dataset (Choi, Zhou and Koltun), as distributed with [Open3D](https://www.open3d.org/)'s `DemoICPPointClouds`, downsampled to 5 cm. The reference alignment was computed with Open3D's point-to-plane ICP.

## Keep going

- [Open3D ICP registration tutorial](https://www.open3d.org/docs/release/tutorial/pipelines/icp_registration.html): point-to-plane ICP and global registration
- [KIRI Engine](https://www.kiriengine.app/): free phone app for capturing your own 3D scans (Part 8)
- [Gaussian Splatting Colab](https://colab.research.google.com/github/camenduru/gaussian-splatting-colab/blob/main/gaussian_splatting_colab.ipynb): turn a point cloud into a trained splat (needs a T4 GPU runtime)
