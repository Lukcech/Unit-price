
Dynamic Unit Price Display
This feature dynamically calculates and displays the price per single unit (e.g., price per piece) on the Shopify product page. The calculation updates in real-time when the customer selects a different product variant.

The entire implementation is self-contained within the product.liquid file to ensure it works reliably, bypassing potential theme-specific issues with external CSS and JavaScript file loading.

Prerequisites: Metafield Setup
Before using this feature, a Variant Metafield must be configured in the Shopify store settings.

Go to: Settings -> Custom data -> Variants

Click: Add definition

Name: Unit Count

Namespace and key: custom.pocet_kusu_v_baleni

Content type: Number -> Integer

This metafield will be used to store the number of items for each product variant.

Implementation Details
The solution consists of a single block of code added to the product.liquid template, placed directly after the main product price </span> element. This block contains three parts:

1. Data Script
A <script> tag generates a global JavaScript object named window.variantMetafields. This object is populated on the server-side using Liquid and contains a map of all variant IDs to their corresponding pocet_kusu (unit count) from the metafields. This makes the data available for client-side processing.

2. HTML & CSS
A simple <div class="unit-price"></div> is added as a placeholder for the output.

An embedded <style> block targets the .unit-price class. It uses flex-basis: 100% to ensure the element always appears on a new line (even within a flexbox container) and applies all necessary font, color, and margin styles.

3. JavaScript Logic
A self-contained <script> block, wrapped in a DOMContentLoaded event listener, performs the following actions:

It defines an updateUnitPrice function responsible for the calculation and DOM manipulation.

It attaches an event listener to the product form ([data-product-form]) that listens for the standard 'change' event.

When the event fires, it retrieves the new variant data from the event.dataset.variant property (a behavior specific to this theme).

It calls the updateUnitPrice function with the new variant data, which then updates the innerHTML and display style of the .unit-price element.

The script also handles the initial page load by running the updateUnitPrice function for the default selected variant.

How to Use
For any product, navigate to the variant you wish to edit in the Shopify Admin.

Scroll down to the Metafields section.

Enter the number of units (e.g., 25) into the Unit Count (pocet_kusu_v_baleni) metafield.

Save the variant.

The unit price will now automatically appear and function on the product page for any variant where this metafield has a value greater than zero.