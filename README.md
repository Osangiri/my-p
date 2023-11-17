import tkinter as tk
from tkinter import filedialog
from PIL import Image, ImageDraw, ImageFont

def open_file():
    file_path = filedialog.askopenfilename(filetypes=[("Image files", "*.png;*.jpg;*.gif")])
    if file_path:
        process_image(file_path)

def process_image(file_path):
    # Open the selected image
    original_image = Image.open(file_path)

    # Create a copy of the original image
    watermarked_image = original_image.copy()

    # Add a watermark
    draw = ImageDraw.Draw(watermarked_image)
    font = ImageFont.load_default()  # You can replace this with a custom font if needed
    watermark_text = "Your Watermark"
    text_width, text_height = draw.textsize(watermark_text, font)
    text_position = ((original_image.width - text_width) // 2, original_image.height - text_height - 10)
    draw.text(text_position, watermark_text, fill="white", font=font)

    # Save or display the watermarked image
    watermarked_image.show()
    # watermarked_image.save("output_image.jpg")  # Uncomment this line to save the watermarked image

# Create the main window
root = tk.Tk()
root.title("Hello, Tkinter!")

# Create a label and add it to the window
label = tk.Label(root, text="Hello, Tkinter!")
label.pack(padx=10, pady=10)

# Create the "Open File" button
button = tk.Button(root, text="Open File", command=open_file)
button.pack(pady=10)

# Start the Tkinter event loop
root.mainloop()
