Gemini Recipe Processing ProtocolThis document outlines the steps to take when a recipe is provided. The goal is to parse the recipe, create a structured HTML file for it, update the main README file with a link to the new recipe, and finally, commit the changes to the GitHub repository.1. Parse the RecipeYour first task is to understand and extract the recipe's details from the user's input.From Images: If the recipe is provided as one or more images, use optical character recognition (OCR) to parse the text. Extract all relevant details, such as ingredients, instructions, cooking time, and servings.From Semi-Structured Text: If the recipe comes from a text source (like the output of another LLM or a simple text file), identify the different components (title, ingredients, steps, etc.). Map these components to the structured format required for the HTML file. Be intelligent about identifying the structure even if it's not perfectly formatted.2. Create the Recipe HTML FileOnce you have the recipe details, you must create a new HTML file.File Naming: The filename must be the name of the recipe, with all spaces replaced by underscores (_). For example, a recipe named "Classic Chocolate Chip Cookies" should have the filename Classic_Chocolate_Chip_Cookies.html.HTML Structure & Microdata: The HTML file must be structured using the schema.org/Recipe microdata vocabulary. This makes the recipe easily understandable by search engines and other tools.Below is a template. You must populate the <span>, <meta>, and <li> tags with the information extracted from the recipe.<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>RECIPE_NAME</title>
</head>
<body>

<div itemscope itemtype="[http://schema.org/Recipe](http://schema.org/Recipe)">
    <h1 itemprop="name">Recipe Name</h1>

    <p itemprop="description">A brief description of the recipe.</p>

    <h2>Ingredients</h2>
    <ul>
        <li itemprop="recipeIngredient">Ingredient 1 (e.g., 2 cups flour)</li>
        <li itemprop="recipeIngredient">Ingredient 2 (e.g., 1 cup sugar)</li>
        <!-- Add more ingredients as needed -->
    </ul>

    <h2>Instructions</h2>
    <ol itemprop="recipeInstructions">
        <li>First step of the recipe.</li>
        <li>Second step of the recipe.</li>
        <!-- Add more steps as needed -->
    </ol>

    <h3>Additional Information</h3>
    <ul>
        <li>Prep Time: <meta itemprop="prepTime" content="PT20M">20 minutes</li>
        <li>Cook Time: <meta itemprop="cookTime" content="PT15M">15 minutes</li>
        <li>Total Time: <meta itemprop="totalTime" content="PT35M">35 minutes</li>
        <li>Yield: <span itemprop="recipeYield">24 cookies</span></li>
        <li>Category: <span itemprop="recipeCategory">Dessert</span></li>
        <li>Cuisine: <span itemprop="recipeCuisine">American</span></li>
    </ul>

</div>

</body>
</html>
Note: The content attribute for time values must be in ISO 8601 duration format (e.g., "PT20M" for 20 minutes).3. Update README.mdAfter creating the HTML file, you need to add a link to it in the main README.md file.Append a new line to the end of the README.md file.The line must be formatted as a markdown list item.Format:* [Recipe Name](RECIPE_NAME.html)Example:* [Classic Chocolate Chip Cookies](Classic_Chocolate_Chip_Cookies.html)4. Upload to GitHubFinally, you must use a shell command to add, commit, and push the new files to the GitHub repository.Execute the following command, replacing "Recipe Name" with the actual name of the recipe you just added.Command:git acp "Recipe Name added to recipes"Example:git acp "Classic Chocolate Chip Cookies added to recipes"By following these four steps, you will ensure that every new recipe is correctly parsed, structured, and integrated into the project.

