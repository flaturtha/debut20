*from: https://help.shopify.com/en/manual/online-store/themes/managing-themes/upgrading-themes*

Upgrading to Online Store 2.0

Migrate your current theme manually
You can upgrade your current theme to Online Store 2.0 by migrating your current theme templates to the new architecture.

You should upgrade your own theme to Online Store 2.0 only if you're comfortable with editing HTML, CSS, and Liquid. If you're not comfortable with editing code, then you can hire a Shopify Partner to help you. Learn more about hiring a Shopify Partner.

If your theme was built specifically for you, then consider contacting the developer or agency that built the theme to plan the upgrade.

To start migrating your theme, follow the migration guide on Shopify.dev. If you're migrating your current theme to Online Store 2.0, then you should duplicate the theme and migrate the duplicate copy. You can publish the duplicate when you're ready.

*from: https://shopify.dev/docs/storefronts/themes/os20/migration*

Migrating templates to Online Store 2.0
Many Online Store 2.0 features rely on JSON templates. You can migrate your theme to add support for these features by converting a Liquid template into a JSON template, and moving any required Liquid code or HTML into sections that you can include in the new JSON template.

In this tutorial, you'll move the code from a Liquid template file into a section file, and then include that section file in a new JSON template. You'll also add support for app blocks to your sections.

This tutorial uses Debut as an example, and moves code from a product.liquid template file into a product-template.liquid section file, which can then be included in a new product.json template.

You can perform all of these steps using Shopify CLI or the code editor.

https://youtu.be/bbd8zLhtONA?si=2i965AF056vwC0AX

Transcript of the above video is instructions/transcript.md

Requirements
Before you start, do the following:

Identify the theme that you want to migrate.
If you want to migrate your theme using your local development environment and Shopify CLI:
Install Shopify CLI.
Make sure that you have a collaborator account or a staff account for the store you want to work on, or you're the owner of the store. If you have a collaborator account or staff account, then you must be granted the Manage themes permission or Themes permission for the store. Store owners have these permissions by default.
Note the URL of the store that you want to work on.
Step 1: Back up the themeAnchor link to section titled "Step 1: Back up the theme"
After you identify the theme that you want to work on, make a copy of it.

If you're editing the theme using the code editor, then duplicate the theme. Make sure that the theme is unpublished while you're editing it. This is because you'll be removing files from the theme, which would impact the live storefront. You might also need a back-up copy to reference or revert to later.

If you're editing the theme locally using Shopify CLI, then download the theme files using the shopify theme pull command.

Step 2: Identify sections and remove section referencesAnchor link to section titled "Step 2: Identify sections and remove section references"
To start converting your Liquid template into a JSON template, you must make note of and then remove any {% section %} tags.

You need to remove these references so that you can move the rest of the code into a section file. Section files can't contain references to other section files.

Open your theme in the code editor or your local development environment.
Locate the product.liquid file in the /templates directory.
Search for any {% section %} tags where sections are being included. Note their names and where they are located.

For example, in Debut, there are two sections included at the top of the template:



Copy
1
2
{% section 'product-template' %}
{% section 'product-recommendations' %}
The first section tag references the product-template section, which contains most of the markup needed to render the product page. That includes the product title, product images, add to cart button, and more.

Next is a reference to the product-recommendations section, which displays a list of products automatically selected as suggestions for customers.

After you've found any {% section %} tags and made a note of their location, delete the tags from the product.liquid file.

Step 3: Move code from the template into a sectionAnchor link to section titled "Step 3: Move code from the template into a section"
After you remove the {% section %} tags from the template code, you need to decide where to move it. You can move this code to an existing section or a new section.

Option 1: Add code to an existing sectionAnchor link to section titled "Option 1: Add code to an existing section"
You might already have a section that renders a large portion of the code for a page. For example, in Debut, the product-template section contains a portion of the code for the product page.

Open the section file where you want to add the template code.
Copy the remaining code from product.liquid.
Paste the code into the section file above the opening {% schema %} tags.
Option 2: Add code to a new sectionAnchor link to section titled "Option 2: Add code to a new section"
If none of the existing section files in your theme are appropriate, then you can create a new section to host your Liquid template code.

Create a new file in the /sections directory. For example, product-content.liquid. If you're creating the section through the code editor, then delete the placeholder code for the section.
After you create your new section file, copy the remaining code from the product.liquid file and paste it into the empty section file.
Step 4: Delete the Liquid template fileAnchor link to section titled "Step 4: Delete the Liquid template file"
After you copy the code from product.liquid, delete product.liquid from the /templates directory. This is because it will be replaced with a product.json file, and a product.liquid and product.json file can't be stored in the /templates directory at the same time.

Step 5: Create a JSON template fileAnchor link to section titled "Step 5: Create a JSON template file"
After the product.liquid file has been deleted, you can create the replacement JSON template.

Create a new file in the /templates directory called product.json:

If you're using the code editor:
Select Add a new template.
From the Create a template for drop-down menu, choose Product.
Select JSON as the template type.
If you're editing the theme locally, then create a new file called product.json and save it in the /templates directory.
After you create the product.json file, replace any default code inside this file with the following:



Copy
1
2
3
4
5
6
7
8
9
10
{
  "sections": {
    "main": {
      "type": "product-template"
    }
  },
  "order": [
    "main"
  ]
}
The type property should reference the name of the section file where you transferred the markup of the product template file in step 3.

Save the file.

Step 6: Test the templateAnchor link to section titled "Step 6: Test the template"
After you create your new template, open it in the theme editor to make sure that it renders correctly.

To access the theme editor using Shopify CLI:

In a terminal, type shopify login --store <DOMAIN>, where <DOMAIN> is the store that you want to log in to. Click the link to finish the login process.
Navigate to the working directory for the theme.
Type shopify theme dev. The dev command returns a link to the Shopify admin theme editor.
Open the theme editor and navigate to a product page. An Add section button should appear in the left sidebar. All the sections that were previously accessible only from the home page should now appear in the Add section menu.

Step 7: Add references to sectionsAnchor link to section titled "Step 7: Add references to sections"
If the original product.liquid template file contained references to additional sections, such as a product recommendations section, then you can define these within the product.json file, and then define their order.

Open product.json. The file currently references only a main section, the section that contains your migrated code.



Copy
1
2
3
4
5
6
7
8
9
10
{
  "sections": {
    "main": {
      "type": "product-template"
    }
  },
  "order": [
    "main"
  ]
}
Add additional sections using this structure. For example, you can add a reference to a product-recommendations section.

In this example, below the main object, you can insert a second object called recommendations. The type property contains the filename of this section:



Copy
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
{
  "sections": {
    "main": {
      "type": "product-template"
    },
    "recommendations": {
      "type": "product-recommendations"
    }

  },
  "order": [
    "main"

  ]
}
Define the order in which the sections appear.

For example, you can order the recommendation section relative to the main section.

Within the order array, add recommendations where the section should appear. In this case, the section should appear below the existing main section.

After you define the order, your product.json file should look like this:



Copy
1
2
3
4
5
6
7
8
9
10
11
12
13
14
{
  "sections": {
    "main": {
      "type": "product-template"
    },
    "recommendations": {
      "type": "product-recommendations"
    }
  },
  "order": [
    "main",
    "recommendations"
  ]
}
When you navigate to the theme editor and select a product page, the product recommendations section should now appear on the page below the product template section.

Tip
You can also add a section, or adjust the order of the sections, using the theme editor.

Step 8: Add support for app blocks to sectionsAnchor link to section titled "Step 8: Add support for app blocks to sections"
If you want to let merchants add app blocks to sections in your theme, then you need to make the following changes to your section code:

Add the necessary schema
Render the block content
You need to make these changes for every section where you want to support app blocks. Learn more about supporting app blocks in your theme.

Note
App blocks are built using theme app extensions, which are currently available only as a developer preview. You can test your updated section code by adding the product reviews sample app.

Enable app blocks in the section schemaAnchor link to section titled "Enable app blocks in the section schema"
To let merchants add an app block to a section, you need to add blocks of type @app to the section's schema. Blocks of type @app aren't supported in statically rendered sections.

For example, to add support for app blocks to the Debut product-template section, you can add the code below. Because the section doesn't contain any blocks, you can add a new blocks node after the schema's settings node.



Copy
1
2
3
4
5
6
7
8
"settings": [
  ...
]
"blocks": [
  {
    "type": "@app"
  }
]
Render app blocksAnchor link to section titled "Render app blocks"
To render an app block in your theme, check for the appropriate type, and then render the block using a {% render block %} tag. You can add this code wherever it makes sense for your section.

For example:



Copy
1
2
3
4
5
6
7
{% for block in section.blocks %}
  {% case block.type %}
    {% when '@app' %}
      {% render block %}
    ...
  {% endcase %}
{% endfor %}
Step 9: Repeat the processAnchor link to section titled "Step 9: Repeat the process"
You can repeat the process outlined above to convert all of the sections in your theme.

Next stepsAnchor link to section titled "Next steps"
After you create new JSON templates based off your Liquid templates, consider enhancing your theme further:

Make your template more modular - You can extract functionality that existed in the core template code into sections and blocks. For example, you can convert a Show vendor checkbox into a block that represents the vendor. Learn some best practices for using sections and blocks.
Connect theme settings to dynamic sources - You can update your theme's default settings to reference dynamic sources. For example, you can reference a product attribute as a default value of a text box. Learn about dynamic sources.
Add version control to your theme - To make later theme updates simpler, and to track theme changes made in the theme editor, code editor, and more, you can connect your theme to a GitHub repository.
Explore tools for building Shopify themes - As a part of Online Store 2.0, Shopify released a new suite of developer tools that help you to streamline your theme development and testing process. Learn more about the tools that are now available.