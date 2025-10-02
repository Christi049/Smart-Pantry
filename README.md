# SmartPantry
Sustainable 7-day meal planning using LLaMA 3.2 + LoRA adapter.  
Generates curated meal plans based on your available ingredients, prioritizing items nearing expiry to minimize food waste.

---

## Features
- Input your **inventory** with quantities and expiry dates.
- Generates a **7-day meal plan**, prioritizing soon-to-expire items.
- Fine-tuned **LLaMA 3.2 3B 4-bit model** with **LoRA adapter** hosted on Hugging Face.
- Includes **dietary restrictions** and **allergen handling**.
- Provides a **shopping list** for missing or complementary ingredients.

---

## 🧠 Model & Adapter
- **Base Model:** [`unsloth/Llama-3.2-3B-Instruct-bnb-4bit`](https://huggingface.co/unsloth/Llama-3.2-3B-Instruct-bnb-4bit)  
- **LoRA Adapter:** [`Christi049/meal-gen-adapter`](https://huggingface.co/Christi049/meal-gen-adapter)  

The adapter is loaded dynamically from Hugging Face, keeping this repo lightweight.

---

## ⚡ Usage
This project requires GPU memory and a compatible runtime (Colab or LM Studio) to run the model. Cloning the repo alone will not allow local CPU-only execution.
Recommended Setup:
1. Open the Colab notebook:
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/18AObSFJ3AQw-h-yIIqBIhuseXsbSKApp?usp=sharing)
2. Upload the dataset(download from repo) file when prompted. 
3. Scroll to the bottom of the notebook where the input cell is provided. Modify the input JSON as needed to reflect your serving size, dietary restrictions, allergens, and ingredients.
4. Run the input cell to generate your 7-day meal plan, prioritizing ingredients that will expire soon. The output includes both:
  display_text for human-readable meals
  description_for_model used internally by the model

---

## 📋 Sample Input / Output

**INPUT**
{
  "serving_size": 2,
  "dietary_restrictions": ["Vegan"],
  "allergens": ["Nuts"],
  "ingredients": [
    {"name": "Lentils (Toor Dal)", "quantity": "250g", "expiry": "2025-09-02"},
    {"name": "Tofu", "quantity": "200g", "expiry": "2025-09-03"},
    {"name": "Spinach", "quantity": "1 bunch", "expiry": "2025-09-04"},
    {"name": "Cabbage", "quantity": "1 medium head", "expiry": "2025-09-07"},
    {"name": "Potatoes", "quantity": "4 medium", "expiry": "2025-09-10"},
    {"name": "Rice Flour", "quantity": "300g", "expiry": "2025-10-01"}
  ]
}

**OUTPUT**
{
  "meals": {
    "Monday": {
      "breakfast": {"description_for_model": "Idli with coconut chutney, using half the lentils and half the rice flour.", "display_text": "Idli with Coconut Chutney"},
      "lunch": {"description_for_model": "Toor Dal with roti, using remaining lentils.", "display_text": "Toor Dal with Roti"},
      "dinner": {"description_for_model": "Leftover Toor Dal.", "display_text": "Leftover Toor Dal"}
    },
    ...
  },
  "shopping_list": ["Coconut", "Kadala", "Mutton", "Bread", "Vegetables", "Bread"]
}



