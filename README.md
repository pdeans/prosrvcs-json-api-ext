# Miva Professional Services JSON API Extensions

Miva Professional Services module for extending the list of available functions for the Miva JSON API. See the list of available extension functions below.

### Table Of Contents

- [Common Request Body Parameters](#common-request-body-parameters)
- [Miva JSON API Extension Functions](#miva-json-api-extension-functions)
    - [Category_Load_Canonical](#category_load_canonical)

## Common Request Body Parameters

The following parameters must be provided for every API request.

| Name | Type | Description |
| --- | --- | --- |
| Store_Code | String | Store Code to run function against. |
| Function | String | This will always have the value of: "**Module**". |
| Module_Code | String | This will always have the value of: "**prosrvcs_json_api_ext**". |
| Module_Function | String | Function to execute. See the request body parameters for each function to get the proper value. |

## Miva JSON API Extension Functions

### Category_Load_Canonical

This function allows you to load the canonical uri for a category.

```
Any of the 3 category identifiers can be used: Category_Id, Category_Code, Edit_Category.
```

**Request Body Parameters**

| Name | Type | Description |
| --- | --- | --- |
| Module_Function | String | Category_Load_Canonical |
| Category_ID | Number | Category ID to load canonical uri. |
| Category_Code | String | Category code to load canonical uri. |
| Edit_Category | String | Category code to load canonical uri. |

**Response Parameters**

| Name | Type | Description |
| --- | --- | --- |
| category_id | Number | The category id. |
| canonical_uri | String | The category canonical uri. |

**Example Request**

```json
{  
    "Store_Code":"test",
    "Function":"Module",
    "Module_Code": "prosrvcs_json_api_ext",
    "Module_Function": "Category_Load_Canonical",
    "Category_Code": "Cat1"
}
```

**Example Resonse**

```json
{
    "success": 1,
    "data": {
        "category_id": 13710,
        "canonical_uri": "/category-uno-buno"
    }
}
```

### WishListItemAndOptions_InsertOrUpdate

This function allows you to add a product to a customer's wishlist

**Request Body Parameters**

| Name | Type | Description |
| --- | --- | --- |
| Module_Function | String | WishListItemAndOptions_InsertOrUpdate |
| Customer_Login | String | Customer Login to use. |
| Wishlist | Object | _Optional_ Wishlist Object. Please see **Wishlist Object Table**. |
| Wishlist_ID | Number | _Optional_ Wishlist ID. |
| Products | Array | Array of Products. Please see **Products Array Table** |

**Wishlist Object**
| Name | Type | Description |
| --- | --- | --- |
| Title | String | _Optional_ Title of Wishlist to create. Defaults to Wishlist Settings in the Miva Admin. |
| Notes | String | _Optional_ Notes of Wishlist getting created. Defaults to empty. |
| Shared | Boolean | _Optional_ If the Wishlist is shared (public), set to 1. Defaults to 0. |

**Products Array**
PLEASE NOTE: One of Product_Code, Product_ID, or Product_SKU is required
| Name | Type | Description |
| --- | --- | --- |
| Product_Code | String | This is the product code of the product you wish to use. |
| Product_ID | Number | This is the product ID of the product you wish to use. |
| Product_SKU | String | This is the product Sku of the product you wish to use. |
| Quantity | Number | Quantity of Product to add to the wishlist. |
| Notes | String | _Optional_ Notes of wishlist item getting inserted. Defaults to empty. |
| Attributes | Array | Array of Attributes. Please see **Product Attributes Array Table** |

**Products Attributes Array**
| Name | Type | Description |
| --- | --- | --- |
| template_code | String | _optional_ Template code for attribute. |
| code | Number | Code of the attribute being used. |
| value | String | Value of the attribute being used. Always use the attribute option code over the prompt. |


**Response Parameters**

| Name | Type | Description |
| --- | --- | --- |
| success | Number | 1 or 0. |

**Example Request**

```json
{  
    "Store_Code":"test",
    "Function":"Module",
    "Module_Code": "prosrvcs_json_api_ext",
    "Module_Function": "WishListItemAndOptions_InsertOrUpdate",
    "Customer_Login": "some-customer-login",
    "WishList": {
        "Title": "Some Title",
        "Notes": "Notes",
        "Public": 1
    },
    "Wishlist_ID": 1,
    "Products": [
        {
            "Product_Code": "some-code",
            "Quantity": 1,
            "Notes": "Some Notes for this Product",
            "Attributes": [
                {
                    "code": "color",
                    "value": "white"
                },
                {
                    "code": "size",
                    "value": "M"
                }
            ]

        }
    ]
}
```

**Example Resonse**

```json
{
    "success": 1
}
```
