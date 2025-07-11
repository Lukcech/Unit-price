
Case Study: Dynamic Unit Price Calculation in Shopify
Summary
This project involved the implementation of a custom-built solution for a Shopify store to dynamically calculate and display a product's unit price (e.g., price per piece). The feature updates in real-time as the customer selects a different product variant, providing transparent price information for easier comparison.

The Problem
The client needed to display a calculated price per single unit for products sold in packages of varying sizes (e.g., 25 pcs, 21 pcs, 19 pcs). The standard Shopify product page only showed the total price for the entire package. The goal was to ensure this unit price updated instantly and reliably whenever a customer selected a different variant (package size).

The Solution
Given the specifics of the theme and challenges with external asset loading, the final solution was engineered as a self-contained module directly within the product.liquid template. This approach ensures stability and independence from the theme's core scripts. The module consists of three main parts:

Data Layer: A server-side Liquid script generates a global window.variantMetafields JavaScript object. This object maps each variant's ID to its corresponding unit count, which is pulled from a custom metafield (custom.pocet_kusu_v_baleni), making the data available on the client-side.

HTML & CSS: A simple <div class="unit-price"></div> element is inserted into the DOM to act as a placeholder. An embedded <style> block contains all necessary CSS rules to control the element's appearance and ensure it correctly wraps to a new line within its parent flexbox container.

Logic: A self-contained JavaScript module listens for the standard 'change' event on the product form. When a new variant is selected, it triggers an updateUnitPrice function. This function performs the calculation (variant price / unit count), formats the result as local currency using the Intl.NumberFormat API, and dynamically injects it into the HTML placeholder. The script also handles the initial page load to display the price for the default selected variant.

The Result
The new feature provides customers with clear and instant information about the price per unit, improving the user experience and price transparency. The solution is fully dynamic and robust.