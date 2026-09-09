## Prototype Development for Image Captioning Using the BLIP Model and Gradio Framework

### AIM:
To design and deploy a prototype application for image captioning by utilizing the BLIP image-captioning model and integrating it with the Gradio UI framework for user interaction and evaluation.

### PROBLEM STATEMENT:
To develop an interactive image captioning application that accepts an input image from the user and automatically generates a meaningful textual description of the image using the pre-trained BLIP model.

### DESIGN STEPS:

#### STEP 1:
Install and import the required libraries such as Transformers, PyTorch, Pillow, and Gradio. Load the pre-trained BLIP image-captioning model and processor.

#### STEP 2:
Create an image captioning function that accepts an uploaded image, processes it using the BLIP processor, and generates a caption using the pre-trained BLIP model.

#### STEP 3:
Design a Gradio interface with an image upload component and a text output component. Launch the interface and test the application with different images.


### PROGRAM:
```python
import os
import time
from PIL import Image
import gradio as gr


def captioner(image):
    if image is None:
        return "Please upload an image."

    prompt = "Write a short, descriptive caption for this image."

    for attempt in range(3):
        try:
            response = client.models.generate_content(
                model="gemini-3.6-flash",
                contents=[image, prompt]
            )

            return response.text

        except Exception as e:
            error_message = str(e)

            if "503" in error_message or "UNAVAILABLE" in error_message:
                if attempt < 2:
                    time.sleep(5)
                    continue

            return f"Error: {error_message}"


gr.close_all()

demo = gr.Interface(
    fn=captioner,
    inputs=gr.Image(
        label="Upload image",
        type="pil"
    ),
    outputs=gr.Textbox(
        label="Caption",
        lines=3
    ),
    title="Image Captioning with Gemini",
    description="Upload an image to generate a descriptive caption using Gemini 3.6 Flash.",
    flagging_mode="never"
)

demo.launch()
```

### OUTPUT:
<img width="1240" height="641" alt="image" src="https://github.com/user-attachments/assets/11f84c67-7380-419d-8e5d-085da62b1e20" />


### RESULT:

Thus, an image captioning prototype using the pre-trained BLIP model and Gradio framework was successfully developed and deployed. The application accepts an image as input and generates a meaningful textual caption as output.
