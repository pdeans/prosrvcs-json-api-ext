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
| Product_Code | String | Product code to use. |
| Quantity | Number | Quantity of product you wish to add. |
| Wishlist_ID | Number | _Optional_ Wishlist ID. |
| Attributes | Array | Optional, unless the product requires attributes. |

```
Attributes is an array with the following parameters for each attribute:
code
template_code
value
```

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
	"Product_Code": "some-product-code",
	"Wishlist_ID": 1,
	"Quantity": 1,
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
```

**Example Resonse**

```json
{
    "success": 1,
}
```
