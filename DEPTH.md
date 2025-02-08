# Depth Data
Since Sensor Logger version 1.41 on iOS, you can capture depth data associated with images from both the front and rear-facing cameras. Depending on the hardware, this depth map is either generated from the disparity across multiple cameras or additional depth sensors such as Lidar or the infrared TrueDepth camera. Sensor Logger does not compute this depth map, it simply surfaces the AVDepthData the operating system has computed. 

To capture depth information, go to Sensor Configuration, then enable Capture Depth. You can see under the toggle a short description about whether your phone and selected camera supports depth. Then, simply collect data using the Camera sensor as usual. 

## Extracting Depth Data
The depth data is packaged inside the captured images. The best way to extract these is via the `exiftool`. On a Mac, you can install via `brew install exiftool`. For other systems, see https://exiftool.org/. In the examples below, we are simply interacting with this command line tool via Python. 

Using the `-json` flag with exiftool, you can check whether depth-related metadata exists in an image captured from the Sensor Logger. The following Python snippet extracts metadata and filters out keys that contain `MPImage`, which may include depth map references:
```python
import json
import subprocess

image_file = 'image_from_sensor_logger.jpg'
exif_cmd = ['exiftool', '-json', image_file]
result = subprocess.run(exif_cmd, capture_output=True, text=True, check=True)
metadata = json.loads(result.stdout)[0]

print({k: v for k, v in metadata.items() if 'MPImage' in k})
```
For example, this may return `{'MPImageFlags': '(none)', 'MPImageFormat': 'JPEG', 'MPImageType': 'Undefined', 'MPImageLength': 35065, 'MPImageStart': 4241276, 'MPImage2': '(Binary data 181206 bytes, use -b option to extract)', 'MPImage3': '(Binary data 35065 bytes, use -b option to extract)'}`. This would imply that the image contains multiple embedded auxiliary images, likely including depth maps or disparity maps, stored within the MP (Multi-Picture) metadata structure. In particular, MPImage2 and MPImage3 exist.

Then you can extract accordingly:
```python
import subprocess
import numpy as np
from PIL import Image
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots

input_file = 'image_from_sensor_logger.jpg'
output_file = 'depth_map.jpg'

with open(output_file, 'wb') as out_f:
    subprocess.run(
        ['exiftool', '-b', '-MPImage3', input_file],
        stdout=out_f,
        check=True
    )

original_img = Image.open(input_file)
depth_img = Image.open(output_file)

original_array = np.array(original_img)
depth_array = np.array(depth_img)

fig = make_subplots(rows=1, cols=2, subplot_titles=["Original Image", "Depth Map"])
fig.add_trace(go.Image(z=original_array), row=1, col=1)
fig.add_trace(go.Heatmap(z=np.fliplr(np.rot90(depth_array, 2)), colorscale="gray", showscale=False), row=1, col=2)
fig.show()
```
<img width="1135" alt="Screenshot 2025-02-08 at 18 13 08" src="https://github.com/user-attachments/assets/e1f8c1fb-e8ee-4bd2-982e-84d8f784449d" />

Wow! Such cool a [LEGO layout](https://www.lego.com/en-gb/product/ninjago-city-gardens-71741) with a multi-layered, deep and stratified architectual composition!
