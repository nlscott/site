---
title: Google Gemini API
parent: Code
layout: default
---

# Google Gemini API

<br>
I've been starting to use the Googel Gemini API. Delevoping some use cases and ways it can used to add context in automations.

It's pretty easy to get started. Head to [https://ai.google.dev/gemini-api/docs/quickstart]( https://ai.google.dev/gemini-api/docs/quickstart)

Instll the `Gemini API library` and create an API key.

A couple points about the below example. Think of `system_instructions` as the tone of the output you want, and `contents` as the question or problem to solve.

<br>

> **system_instruction**:
> System instructions let you steer the behavior of a model based on your specific use case. When you provide system instructions, you give the model additional context to help it understand the task and generate more customized responses. 

> **contents:**
> Required. The content of the current conversation with the model.



<br>

## Example:

Asking Gemini to create a chicken alfredo recipe, but to convert measurements to grams.

```python
#!/usr/bin/env python

from google import genai
from google.genai import types

api_key="xxxx"

def ask_gemini():
    client = genai.Client(api_key="{}".format(api_key))
    response = client.models.generate_content(
        model = "gemini-2.0-flash",
        config = types.GenerateContentConfig(
            system_instruction = """
            I love to home cook. Convert measurements to grams.
            """),
            contents="""
            whats a good recipe for chicken alfredo
            """
        )

    print(response.text)

def main():
    ask_gemini()

if __name__ == "__main__":
    main()
```



## Output

The output is surprisingly though. With the addiontal conversions to grams!

---
Okay, let's get you a great Chicken Alfredo recipe with some options and tips for making it delicious! I'll give you a base recipe and then some ideas to customize it. I'll also include estimated gram measurements for the ingredients. Keep in mind these are estimates, and slight variations won't ruin the dish.

### Classic Chicken Alfredo Recipe

**Yields:** 4-6 servings
**Prep time:** 15 minutes
**Cook time:** 25 minutes

### Ingredients:

*   **Chicken:**
    *   1.  5 lbs (approximately 680g) boneless, skinless chicken breasts, cut into bite-sized pieces

*   **Pasta:**
    *   1 lb (approximately 454g) Fettuccine pasta (or your favorite pasta shape)

*   **Alfredo Sauce:**
    *   4 tbsp (approximately 57g) unsalted butter
    *   2 cloves garlic, minced (approximately 6g)
    *   1 1/2 cups (approximately 360ml) heavy cream
    *   1 cup (approximately 100g) grated Parmesan cheese, plus more for serving
    *   1/4 cup (approximately 25g) grated Romano cheese
    *   1/4 tsp (approximately 1g) salt (or to taste)
    *   1/4 tsp (approximately 0.5g) black pepper (or to taste)
    *   Pinch of nutmeg (optional)

*   **For Cooking Chicken:**
    *   1 tbsp (approximately 14g) olive oil
    *   1/2 tsp (approximately 2g) Italian seasoning
    *   1/4 tsp (approximately 1g) garlic powder
    *   Salt and pepper to taste

### Equipment:

*   Large pot
*   Large skillet or sauté pan
*   Tongs
*   Whisk

### Instructions:

**1. Cook the Pasta:**

*   Bring a large pot of salted water to a boil. Add the fettuccine and cook according to package directions until al dente. Reserve about 1 cup of pasta water before draining. Drain the pasta and set aside.

**2. Cook the Chicken:**

*   While the pasta is cooking, prepare the chicken. In a bowl, toss the chicken pieces with olive oil, Italian seasoning, garlic powder, salt, and pepper.
*   Heat a large skillet or sauté pan over medium-high heat. Add the chicken and cook until golden brown and cooked through, about 5-7 minutes. Remove the chicken from the pan and set aside.

**3. Make the Alfredo Sauce:**

*   In the same skillet, melt the butter over medium heat. Add the minced garlic and cook for about 30 seconds, until fragrant, being careful not to burn it.
*   Pour in the heavy cream and bring to a simmer, stirring occasionally. Reduce the heat to low and let it simmer for about 3-5 minutes, allowing the cream to thicken slightly.
*   Gradually whisk in the Parmesan cheese and Romano cheese until the sauce is smooth and creamy. Season with salt, pepper, and a pinch of nutmeg (if using).
*   If the sauce is too thick, add a little of the reserved pasta water until it reaches your desired consistency.

**4. Combine Everything:**

*   Add the cooked fettuccine to the skillet with the Alfredo sauce. Toss to coat the pasta evenly.
*   Add the cooked chicken to the pasta and sauce. Toss gently to combine.

**5. Serve:**

*   Serve immediately, garnished with extra Parmesan cheese and freshly ground black pepper, if desired.

### Tips and Variations:

*   **Cream Cheese:** For an extra creamy sauce, add 2-4 ounces (57-113g) of softened cream cheese to the sauce while it's simmering. Whisk until smooth.
*   **Garlic:** Some people like roasted garlic. Roast a whole head and squeeze the cloves into the sauce for a sweeter garlic flavor.
*   **Vegetables:** Add steamed or sautéed vegetables like broccoli, asparagus, peas, mushrooms, or spinach to the pasta for added nutrients and flavor. Add them in the last few minutes of cooking.
*   **Spice:** Add a pinch of red pepper flakes to the sauce for a little heat.
*   **Wine:** Add a splash of dry white wine (like Pinot Grigio or Sauvignon Blanc) to the sauce after the garlic for extra flavor. Let it reduce for a minute or two before adding the cream.
*   **Lemon:** A squeeze of fresh lemon juice at the end brightens up the sauce.
*   **Fresh Herbs:** Garnish with fresh parsley or chives for added flavor and color.
*   **Chicken Thighs:** You can use boneless, skinless chicken thighs instead of breasts for a richer flavor.

### Important Considerations:

*   **Quality of Ingredients:** Use high-quality Parmesan cheese and heavy cream for the best flavor. Freshly grated Parmesan is always better than pre-grated.
*   **Don't Overcook the Pasta:** Al dente pasta holds its shape better and absorbs the sauce better.
*   **Adjust Seasoning:** Taste the sauce and adjust the salt, pepper, and other seasonings to your liking.
*   **Serve Immediately:** Alfredo sauce tends to thicken as it cools, so it's best to serve it right away.

Enjoy your homemade Chicken Alfredo! Let me know if you have any other questions.
