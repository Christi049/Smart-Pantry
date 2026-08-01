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
- **Dataset:** [`Christi049/meal-gen/Dataset.json`](https://huggingface.co/datasets/Christi049/meal-gen/blob/main/Dataset.json)

The LoRA adapter is created from the custom dataset and uploaded to Hugging Face

---

## ⚡ Usage
This project requires GPU memory and a compatible runtime (Colab or LM Studio) to run the model. Cloning the repo alone will not allow local CPU-only execution.
Recommended Setup:
1. Open the Colab notebook:
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/18AObSFJ3AQw-h-yIIqBIhuseXsbSKApp?usp=sharing)
2. Upload the dataset(download from provided link) file when prompted. 
3. Scroll to the bottom of the notebook where the input cell is provided. Modify the input JSON as needed to reflect your serving size, dietary restrictions, allergens, and ingredients.
4. Run the input cell to generate your 7-day meal plan, prioritizing ingredients that will expire soon. The output includes both:
  display_text for human-readable meals
  description_for_model used internally by the model

---

## 📋 Sample Input / Output

### Sample Input
```json
{
   serving_size": 2,
   "dietary_restrictions": ["Vegan"],
   "allergens": ["Nuts"],
   "ingredients":
      [{"name": "Lentils (Toor Dal)", "quantity": "250g", "expiry": "2025-09-02"},
      {"name": "Tofu", "quantity": "200g", "expiry": "2025-09-03"},
      {"name": "Spinach", "quantity": "1 bunch", "expiry": "2025-09-04"},
      {"name": "Cabbage", "quantity": "1 medium head", "expiry": "2025-09-07"},
      {"name": "Potatoes", "quantity": "4 medium", "expiry": "2025-09-10"},
      {"name": "Rice Flour", "quantity": "300g", "expiry": "2025-10-01"}
   ]
}
```

### Sample Output

```json
{
   ### Meal Plan for 2 people, prioritizing ingredients that will expire soon.
   ### Monday
   - Breakfast: Upma made with 100g of rice flour, with jaggery syrup (no nuts).
   - Lunch: Masala Dosa, using 100g of rice flour, with potato masala (using 1 medium potato and some onions from shopping list).
   - Dinner: Leftover dosa with sambhar (made with store-bought sambhar powder and vegetables from shopping list).
   
   ### Tuesday
   - Breakfast: Puttu, made from 100g of rice flour, with Kadala (made from grated coconut and jaggery, no nuts).
   - Lunch: Tofu curry with rice, using 100g of tofu and vegetables from shopping list.
   - Dinner: Leftover Tofu curry with roti (made from 100g of rice flour).
   
   ### Wednesday
   - Breakfast: Upma with vegetables (using the remaining spinach and some onions from shopping list).
   - Lunch: Spinach and cabbage thoran (Kerala-style stir-fry) using the remaining spinach and half the cabbage, with rice.
   - Dinner: Leftover thoran with roti.
   
   ### Thursday
   - Breakfast: Rice flour pancakes with syrup.
   - Lunch: Vegetable Biryani, using the remaining cabbage and potatoes.
   - Dinner: Leftover Biryani.
   
   ### Friday
   - Breakfast: Toast with jam (from shopping list).
   - Lunch: Tofu scramble with sautéed cabbage and potatoes (using the remaining tofu and cabbage).
   - Dinner: Leftover scramble with rice.
   
   ### Saturday
   - Breakfast: Toast with jam.
   - Lunch: Simple dal with rice.
   - Dinner: Leftover dal with roti.
   
   ### Sunday
   - Breakfast: Toast with jam.
   - Lunch: Vegetable curry with rice.
   - Dinner: Leftover curry with roti.
   
   ### Shopping List:
   - Jaggery
   - Onions
   - Sambhar powder
   - Kadala (coconut)
   - Roti flour
   - Vegetable scraps for sambhar
   - Biryani spices
   - Biryani ingredients (if not available)
   - Jam
   - Toast
}
```

