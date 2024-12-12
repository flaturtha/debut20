# Liquid Templates to Update to JSON

The following Liquid template files need to be migrated to JSON templates:

- `templates/article.liquid` 
- `templates/blog.liquid`
- `templates/cart.liquid`
- `templates/collection.liquid`
- `templates/customers/account.liquid` 
- `templates/customers/activate_account.liquid`
- `templates/customers/addresses.liquid`
- `templates/customers/login.liquid`
- `templates/customers/order.liquid`
- `templates/customers/register.liquid`
- `templates/customers/reset_password.liquid`
- `templates/list-collections.liquid`
- `templates/page.liquid`
- `templates/product.liquid`

Each of these `.liquid` files needs to be:
1. Have its content/code moved into a section file 
2. Deleted and replaced with a `.json` file of the same name
3. Have the JSON file reference the section(s) the content was moved to