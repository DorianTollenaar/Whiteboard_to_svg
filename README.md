# Whiteboard to robot paths

## Run

```sh
cd ~/Csci/26-grad/fall/robotics/final_local
source ~/Csci/26-grad/fall/robotics/.venv/bin/activate
python main.py
```

The `source` command activates the Python environment containing the project's dependencies.

1. Keep the camera fixed and point it at your board or paper.
2. Click the drawing area's corners: top-left, top-right, bottom-right, bottom-left.
3. Move your hand out of view and press `s` or `c` to capture, process, and export automatically.
4. View the traced drawing in the second window. Capture again to update the outputs.
5. Press `r` to select new corners or `q` to quit.

To choose a camera and set the physical drawing dimensions in meters:

```sh
python main.py --camera 1 --width-m 0.30 --height-m 0.21
```

To process an existing image already cropped to the drawing area:

```sh
python main.py --image drawing.png
```

## Files used

| File | Purpose |
| --- | --- |
| `main.py` | Entry point: camera preview, corner selection, perspective correction, processing, and preview/SVG export. |
| `geometry_corection.py` | Imported by `main.py` to extract centerline strokes from the image. |
| `robot_paths.py` | Imported by `main.py` to convert pixels into meter coordinates and export robot waypoints. |
| `requirements.txt` | Python dependency list for installing a new environment. |
| `tests/test_pipeline.py` | Automated tests; not used during normal capture. |

`scripts/webcam_photo.jpg` is an old saved photo and is not used unless you pass it with `--image`.

## Generated files

Every capture replaces these files in `outputs/`:

| File | Contents |
| --- | --- |
| `whiteboard.png` | Straightened board image. |
| `corrected_lines.png` | Board image with traced strokes shown in red. |
| `drawing.svg` | Vector version of the traced strokes. |
| `drawing_paths.json` | Strokes and movement waypoints in meters. |
| `drawing_waypoints.csv` | Waypoints with stroke ID, pen state, and X/Y/Z coordinates. |

The program generates paths. Running them on a robot requires a separate controller and calibration.
