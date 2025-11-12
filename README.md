# 🧱 Brick-Based Room Builder – Doors & Windows (Geometry API)

This project simulates **brick wall construction** and allows you to **carve out doors and windows** from the wall geometry using a simple CSV input.

It supports both **procedural wall generation** and **language-based design prompts** via an `openings.csv` file.  
The implementation runs entirely in **Jupyter Notebook**.

---

## 🚀 Features

✅ Generate 4 walls (front, back, left, right) brick-by-brick  
✅ Carve out openings (doors/windows) from geometry  
✅ Load designs from `openings.csv`  
✅ Visualize top and side views in Matplotlib  
✅ Save updated wall structure as `placement_updated.csv`  
✅ Fully Jupyter Notebook compatible (no CLI needed)

---

## 📁 Project Structure


---

## 🧩 Geometry API

### Core Functions

| Function | Description |
|-----------|--------------|
| `carve_opening(df, wall, x_mm, z_mm, width_mm, height_mm)` | Main logic that hides bricks in a specified range |
| `carve_door(df, wall, x_mm, z_mm=0, width_mm=900, height_mm=2100)` | Wrapper for carving a standard door |
| `carve_window(df, wall, x_mm, z_mm=900, width_mm=1200, height_mm=900)` | Wrapper for carving a standard window |

**Walls supported:** `front`, `back`, `left`, `right`  
**Wall thickness:** 200 mm  
**Brick size:** 200 mm cube (default grid spacing)

---

## 📄 openings.csv Format

The `openings.csv` defines every door and window.  
Example:

```csv
wall,x_mm,z_mm,width_mm,height_mm,type
front,0,0,900,2100,door
right,1200,900,1200,900,window

🧠 How It Works (Inside Jupyter)
Step 1 – Load Files
placement_df = pd.read_csv("placement.csv")
openings = pd.read_csv("openings.csv")

Step 2 – Apply Carving
for _, row in openings.iterrows():
    if row["type"] == "door":
        placement_df = carve_door(placement_df, row["wall"], row["x_mm"], row["z_mm"],
                                  row["width_mm"], row["height_mm"])
    elif row["type"] == "window":
        placement_df = carve_window(placement_df, row["wall"], row["x_mm"], row["z_mm"],
                                    row["width_mm"], row["height_mm"])

Step 3 – Visualize
plot_top_view(placement_df)


(Optional: use plot_side_view_for_wall(df, "front") to see elevations.)

Step 4 – Save
placement_df.to_csv("placement_updated.csv", index=False)

🖼 Visualization Examples

Top view (visible vs. carved):

plot_top_view(placement_df)


Side view (by wall):

for w in ["front", "back", "left", "right"]:
    plot_side_view_for_wall(placement_df, w)


The carved areas (red dots) show doors/windows removed from the wall.

🧰 Running the Notebook
Option 1 – Run Entire Notebook

Simply open solve.ipynb in Jupyter or VS Code → Run All Cells.

Option 2 – Interactive Steps

Run section by section (Generate → Carve → Visualize).

🧾 Example Workflow

Open Jupyter Notebook

Upload placement.csv and openings.csv

Run all cells in solve.ipynb

View the top-view plot and carved wall geometry

(Optional) Commit your outputs back to GitHub
