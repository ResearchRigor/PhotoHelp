
import cv2
import numpy as np
from PIL import Image, ImageEnhance
import tensorflow as tf

perfect = 0
adjusted = 0

def analyze_image(image_path):

    img = cv2.imread(image_path)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

    brightness = np.mean(img_rgb)
    contrast = np.std(img_rgb)
    sharpness = cv2.Laplacian(img_rgb, cv2.CV_64F).var()
    
    return brightness, contrast, sharpness

def generate_advice(brightness, contrast, sharpness):
    advice = []
  
    if brightness < 100:
        advice.append("Consider increasing exposure or using additional lighting.")
        perfect += 1
    elif brightness > 200:
        advice.append("The image may be overexposed. Try reducing exposure or using ND filters.")
        perfect += 1
    
    if contrast < 50:
        advice.append("Increase contrast in post-processing or adjust lighting for more dynamic range.")
        perfect += 1
    
    if sharpness < 100:
        advice.append("The image appears soft. Check focus or use a tripod for sharper results.")
        perfect += 1
    
    return advice

def get_photography_advice(image_path):
    brightness, contrast, sharpness = analyze_image(image_path)
    advice = generate_advice(brightness, contrast, sharpness)
    
    print("Image Analysis Results:")
    print(f"Brightness: {brightness:.2f}")
    print(f"Contrast: {contrast:.2f}")
    print(f"Sharpness: {sharpness:.2f}")
    
    print("\nPhotography Advice:")
    if perfect == 0:
        print("Your photo looks great!!!\n")
    else:
        for tip in advice:
            print(f"- {tip}\n\n")

def auto_adjust():
    
    brightfix = 0
    brightmin = 100
    brightmax = 200
    brightness_enhancer = ImageEnhance.Brightness(image)
    while brightfix < brightmin or brightfix > brightmax:
        if brightfix < brightmin:
            brightfix_image = brightness_enhancer.enhance(1.01)
        elif brightfix > brightmax:
            brightfix_image = brightness_enhancer.enhance(0.99)

    contrastfix = 0
    contrast_enhancer = ImageEnhance.Contrast(brightfix_image)
    while contrastfix < 50:
        contrastfix_image = contrast_enhancer.enhance(1.01)
    
    sharpnessfix = 0
    sharpness_enhancer = ImageEnhance.Sharpness(contrastfix_image)
    while sharpnessfix < 100:
        adj_image = sharpness_enhancer.enhance(1.01)
    
    adj_image.save("adjusted_image.jpg")

    



input_path = input("Please input the path to your image here: ")
image_path = input_path.replace('\\', '\\\\')
image = Image.open(image_path)
image.show()
print("\n")
get_photography_advice(image_path)
edit_yn = input("Would you like us to edit your image? Type Y or N: ")
print("\n\n")
if edit_yn == "Y":
    print("******EDITING******\n\n")
    if perfect > 0:
        autofix_choice = input("Would you like us to automatically fix your image? Y or N: ")
        if autofix_choice == "Y":
            auto_adjust
            "Your image has been adjusted to fit the suggested parameters."
            adj_image = Image.open("adjusted_image.jpg")
            adj_image.show()
            adjusted += 1

        else:
            print("No automatic adjustments made.")
    
    edit_choice = input("What would you like to edit? Type B for Brightness, C for Contrast, or S for Sharpness: ")
    if edit_choice == "B":
        if adjusted > 0:
