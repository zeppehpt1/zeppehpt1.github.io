Remove alpha channel from tif:
```bash
gdal_translate -b 1 -b 2 -b 3 -of GTiff -co BIGTIFF=YES -co COMPRESS=LZW input.tif output.tif
```

Adjust pixel size:
```bash
gdalwarp -tr 0.034186315034993066 -0.03418631503499349 Theresienhain_DSM_Juli_2022_ds_dtm.tif Theresienhain_DTM_Juli_2022.tif
```

```Python
reference_tif = raster_path
warped = gdal.Warp(output_path, reference_tif, targetAlignedPixels=True, xRes=0.1, yRes=-0.1)
warped = None
```

Select a smaller window from a raster file:
```bash
gdal_translate -srcwin 20000 20000 1000 1000 ortho.tif sample.tif 
```

Make background of .tif transparent:
```bash
gdal_edit.py -a_nodata 0 hain_complete.tif
```

Get information about raster file:
```bash
gdalinfo
```