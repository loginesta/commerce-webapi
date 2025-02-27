---
title: moveCartItemsToGiftRegistry mutation | Commerce Web APIs
edition: ee
contributor_name: Atwix
contributor_link: https://www.atwix.com/
---

# moveCartItemsToGiftRegistry mutation

The `moveCartItemsToGiftRegistry` mutation moves all items from the cart to a gift registry.

This mutation requires a valid [customer authentication token](../../customer/mutations/generate-token.md).

## Syntax

```graphql
mutation {
    moveCartItemsToGiftRegistry (
        cartUid: ID!,
        giftRegistryUid: ID!
    ) {
        MoveCartItemsToGiftRegistryOutput
    }
}
```

## Example usage

The following example moves all items from the cart to a gift registry.

**Request:**

``` graphql
mutation {
  moveCartItemsToGiftRegistry (
      cartUid:"8k0Q4MpH2IGahWrTRtqM61YV2MtLPApz",
      giftRegistryUid:"Owu5mdQ3uyfOAWzj8lFlHZW4uCDaMWC6"
  ) {
  gift_registry {
      uid
      created_at
      owner_name
      status
      type {
        label
      }
      message
      items {
        product {
          sku
          name
        }
      }
    }
    status
    user_errors {
      code
      message
      product_uid
      gift_registry_uid
    }
  }
}
```

**Response:**

```json
{
  "data": {
    "moveCartItemsToGiftRegistry": {
      "gift_registry": {
        "uid": "Owu5mdQ3uyfOAWzj8lFlHZW4uCDaMWC6",
        "status": "ACTIVE",
        "created_at": "2021-05-06 21:19:05",
        "owner_name": "Veronica Costello",
        "type": {
          "label": "Birthday"
        },
        "message": "Birthday",
        "items": [
          {
            "product": {
              "sku": "24-UG06",
              "name": "Affirm Water Bottle "
            }
          }
        ]
      },
      "status": true,
      "user_errors": []
    }
  }
}
```

## Input attributes

The `moveCartItemsToGiftRegistry` mutation requires the following input:

Attribute |  Data Type | Description
--- | --- | ---
`cartUid` | ID! | The unique ID that identifies the customer's cart
`giftRegistryUid` | ID! | The unique ID of a `GiftRegistry` object

## Output attributes

The `MoveCartItemsToGiftRegistryOutput` object can contain the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`gift_registry` | [GiftRegistry!](#giftregistry-attributes) | The gift registry containing the moved items
`status` | Boolean! | Indicates whether the attempt to move the cart items to the gift registry was successful
`user_errors` | [[GiftRegistryItemsUserError!](#giftregistryitemsusererror-attributes)] | An array of errors encountered while moving items from the cart to the gift registry

### GiftRegistry attributes

import GiftRegistry from '/src/pages/_includes/graphql/gift-registry.md'

<GiftRegistry />

### GiftRegistryItemsUserError attributes

import GiftRegistryItemsUserError from '/src/pages/_includes/graphql/gift-registry-items-user-error.md'

<GiftRegistryItemsUserError />
