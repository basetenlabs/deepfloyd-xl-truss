# DeepFloyd XL

This is a [Truss](https://truss.baseten.co/) for DeepFloyd-IF. DeepFloyd-IF is a pixel-based text-to-image triple-cascaded diffusion model, that can generate pictures with new state-of-the-art for photorealism and language understanding. The result is a highly efficient model that outperforms current state-of-the-art models, achieving a zero-shot FID-30K score of 6.66 on the COCO dataset.

To deploy this model, you'll need to

1. Accept the terms of service of the Deepfloyd XL model [here](https://huggingface.co/DeepFloyd/IF-I-XL-v1.0).
2. Retrieve your Huggingface token from the [settings](https://huggingface.co/settings/tokens).
3. Set your Huggingface token as a Baseten secret [here](https://app.baseten.co/settings/secrets) with the key `hf_api_key`.

# Deploying to Baseten

To deploy this Truss on Baseten, first install the Baseten client:

```
$ pip install baseten
```

Then, in a Python shell, you can do the following to have an instance of CLIP deployed
on Baseten:

```python
import baseten
import truss

deepfloyd_handle = truss.load(".")
baseten.deploy(deepfloyd_handle, model_name="DeepFloyd-XL")
```


# Model Details
- Developed by: DeepFloyd, StabilityAI
- Model type: pixel-based text-to-image cascaded diffusion model
- Cascade Stage: I
- Num Parameters: 4.3B
- Language(s): primarily English and, to a lesser extent, other Romance languages
- License: [DeepFloyd IF License Agreement](https://huggingface.co/spaces/DeepFloyd/deepfloyd-if-license)
- Model Description: DeepFloyd-IF is modular composed of frozen text mode and three pixel cascaded diffusion modules, each designed to generate images of increasing resolution: 64x64, 256x256, and 1024x1024. All stages of the model utilize a frozen text encoder based on the T5 transformer to extract text embeddings, which are then fed into a UNet architecture enhanced with cross-attention and attention-pooling

# Usage

## Input

This deployment of DeepFloyed takes as input a dictionary with the following keys:
* `prompt` - the prompt for image generation

It also supports a number of other parameters detailed in [this blog post](https://huggingface.co/blog/if).

## Output

The result will be a dictionary containing:
* `status` - either `success` or `failed`
* `data` - list of base 64 encoded images
* `message` - will contain details in the case of errors

```json
{"status": "success", "data": ["/9j/4AAQSkZJRgABAQAAAQABAA...."], "message": null}
```

## Example

```
curl -X POST https://app.staging.baseten.co/models/EqwKvqa/predict \
  -H 'Authorization: Api-Key fs8S62Qy.7YtQSzoCJKjQeI6L7VvdFFCLZu3CTt7d' \
  -d '{"prompt": "maan on moon"}'
{"model_id": "EqwKvqa", "model_version_id": "yqvx0rw", "model_output": {"status": "success", "data": ["/9j/4AAQSkZJRgABAQAAAQABAA...."], "message": null}}
```