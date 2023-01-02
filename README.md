There are two basic model in this repo, sanet and csbnet. \
Both are encoder-decoder model, need to download vgg encoder/decoder. 

## sanet
download pre-trained vgg encoder [here](https://drive.google.com/file/d/1nReMU44xMcqUxmUoiq6HLV3Kd9pTMYyU/view?usp=share_link). \
download pre-trained sanet transformer [here](https://drive.google.com/file/d/18fQH2BY63RKUVAFlYYTQeH50JDtlHYku/view?usp=share_link). \
download pre-trained vgg decoder [here](https://drive.google.com/file/d/18jPL5MgDkUMciZRTidkWGLZdDGGq1Pf_/view?usp=share_link)
### Image transformation


--mask_path: parameter specify to image tdtm. \
--alpha: level of stylization,input type should  be float/int/string. \
--cutoff: do stylization separably for background and forward image. \
--interpolation: beta parameter, may be unstable with others parameters. \


```
# By default,if input with both content and content_dir (style and style_dir), model will precede directory path over image path.
# basic usage:
    --content <frame location> \
    --content_dir <frame folder location>
    --style <style location> \
    --style_dir <style folder location> \
    --output <output folder> \
    --vgg_path <vgg path> \    
    --decoder_path <decoder path> \
    --transform_path <sanet transformer path> \
```

```
  # stable version
  python sanet.py \
    --content <frame location> \
    --content_dir <frame folder location>
    --style <style location> \
    --style_dir <style folder location> \
    --output <output folder> \
    --mask_path <ur mask path>/TDTM_mask.jpg \
    --background <ur background style>/style_0.jpg \
    --alphas '0.8,1.0' \
    --cutoff \
    --vgg_path <vgg path> \    
    --decoder_path <decoder path> \
    --transform_path <sanet transformer path> \
```
Dont use interpolation parameter!
  
### video transformation
```
  python sanet_video.py \
    --video_path \ 
    --style \
    --output
```
  
## csbent
need imageio package
```
pip install imageio-ffmpeg
```
download pre-trained vgg [here](https://drive.google.com/file/d/1DP_P7t4En07cZjho6hnXNuyv5E5yVno-/view?usp=share_link) \
download pre-trained csbent[here](https://drive.google.com/file/d/1-Ac9I5wYJMNJZG7r60e0GnVrAo6sNcrV/view?usp=share_link)

### Image transformation
Do not care about KC,KS parameters, these are choosen by experimets.
```
  python csbnet_image.py \
  --content_dir <image path or dir path> \
  --style_dir <image path or dir path> \
  --KC 4 --KS -10 \
  --output_dir <output dir path> \
  --vgg_path models/vgg_normalised.pth \
  --csbnet_path models/csbnet.pth  
```

### Video transformation
```
  python cbnet_video.py \
  --content_dir <video_path>  \
  --style_dir  <style path or dir path > \
  --KC 4 --KS -10 \
  --fps 10 \
  --output_dir  <output dir path> \
  --vgg_path models/vgg_normalised.pth \
  --csbnet_path models/csbnet.pth 
```
