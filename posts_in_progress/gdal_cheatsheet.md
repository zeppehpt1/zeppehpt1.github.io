Remove alpha channel from tif cmd:
```bash
gdal_translate -b 1 -b 2 -b 3 -of GTiff -co BIGTIFF=YES -co COMPRESS=LZW input.tif output.tif
```
Remove alpha channel from tif python:
```python
kwargs = {
    'format': 'GTiff',
    'outputType': gdal.GDT_Int16
    'bandList' [1,2,3]
}
fn = 'input.tif'
dst_fn = 'output.tif'

ds = gdal.Translate(dst_fn, fn, **kwargs)
ds = None
```

Adjust pixel size cmd:
```bash
gdalwarp -tr 0.034186315034993066 -0.03418631503499349 Theresienhain_DSM_Juli_2022_ds_dtm.tif Theresienhain_DTM_Juli_2022.tif
```

Adjust pixel size python:
```Python
reference_tif = raster_path
warped = gdal.Warp(output_path, reference_tif, targetAlignedPixels=True, xRes=0.1, yRes=-0.1)
warped = None
```

Reproject raster file
```zsh
gdalwarp -s_srs epsg:31468 -t_srs epsg:32632 Bamberg_dtm_31468.tif newly.tif
```

Select a smaller window from a raster file based on the origin of the image file (top left corner of the image):
```bash
gdal_translate -srcwin 20000 20000 1000 1000 ortho.tif sample.tif 
```

Select a smaller window from a raster file based on the given top left corner and bottom right corner coordinates:
```bash
gdal_translate -projwin ulx uly lrx lry input.tif output.tif
```

Make background of .tif transparent:
```bash
gdal_edit.py -a_nodata 0 hain_complete.tif
```

Get information about raster file:
```bash
gdalinfo example.tif
```