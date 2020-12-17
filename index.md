# VANIR API

### General Information:
1. All the fields in the **errors** in the response are not always present! They appear only if there is an error.
2. For endpoints with the method `GET`, the **request** is passed in the form of URL parameters.
___

### `POST` *{url}/login*
* ##### Request:
    * **email:** required & exists is _users_, column _email_
    * **password:** required
* ##### Response:
    * **success** (boolean)
    * **token** (string; only if _success_ is true)
    * **errors:** (array)
        * **email** (array of strings) Can be either "required" or "exists" 
        * **password** (array of strings) Can be either "required" or "invalid"
* ##### Restricții: _niciuna_


### `POST` *{url}/login*
* ##### Request:
    * **firstName:** required
    * **lastName:** required
    * **email:** required & does not exist is _users_, column _email_
    * **password:** required
* ##### Response:
    * **success** (boolean)
    * **token** (string; only if _success_ is true)
    * **errors:** (array)
        * **firstName:** (array of strings) Can be "required"
        * **lastName:** (array of strings) Can be "required"
        * **email** (array of strings) Can be either "required" or "unique" 
        * **password** (array of strings) Can be "required"
* ##### Restricții: _niciuna_


### `POST` *{url}/forgot*
* ##### Request:
    * **email:** required & exists is _users_, column _email_
* ##### Response:
    * **success** (boolean)
    * **errors:** (array)
        * **email** (array of strings) Can be "invalid"
* ##### Restricții: _niciuna_


### `POST` *{url}/forgot/validate*
* ##### Request:
    * **email:** required & exists is _users_, column _email_ & exists is _password_resets_, column _email_
    * **token:** required
* ##### Response:
    * **success** (boolean)
    * **errors:** (array)
        * **email** (array of strings) Can be either "required" or "exists"
        * **token** (array of strings) Can be "required"
* ##### Restricții: _niciuna_


### `POST` *{url/reset*
* ##### Request:
    * **email:** required & exists is _users_, column _email_ & exists is _password_resets_, column _email_
    * **token:** required
    * **password:** required
* ##### Response:
    * **success** (boolean)
    * **errors:** (array)
        * **email** (array of strings) Can be either "required" or "exists"
        * **token** (array of strings) Can be either "required" or "invalid"
        * **password** (array of strings) Can be "required"
* ##### Restricții: _niciuna_


### `GET` *{url}/data/counties*
* ##### Request:
    * **country:** (momentan merge doar penru "ro")
* ##### Response: 
    Un array care conține o listă cu județele din țara specificată.
* ##### Restricții: _niciuna_


### `GET` *{url}/categories*
* ##### Request: _(empty)_
* ##### Response:
    ```
    [
        id: number;
        slug: string;
        name: string;
        parent: number|null;
        children: Array<Category>|null;
        icon: string|null;
        image: string|null;
    ]
    ```
* ##### Restricții: _niciuna_


### `GET` *{url}/categories/:slug*
* ##### Request: _(empty)_
* ##### Response:
    ```
    id: number;
    slug: string;
    name: string;
    parent: number|null;
    children: Array<Category>|null;
    icon: string|null;
    image: string|null;
    ```
* ##### Restricții: _niciuna_


### `GET` *{url}/categories/:slug/products*
* ##### Request:
    * **page:** not required;
* ##### Response:
    * remaining: (boolean)
    * data: (array)
        ```
        Array<{
            id: number;
            seller: string;
            categoryName: string;
            categorySlug: string;
            slug: string;
            name: string;
            longName: string;
            smallDescription: string;
            description: string;
            price: number;
            rating: number;
            image: string;
            images: Array<string>;
            attributes: Array<{
                name: string;
                type: 0 (text) / 1 (number) / 2 (boolean) / 3 (colour) / 4 (size);
                value: any;
            }>;
        }>
        ```
* ##### Restricții: _niciuna_


### `GET` *{url}/products*
* ##### Request: _(empty)_
* ##### Response:
        Array<{
            id: number;
            seller: string;
            categoryName: string;
            categorySlug: string;
            slug: string;
            name: string;
            longName: string;
            smallDescription: string;
            description: string;
            price: number;
            rating: number;
            image: string;
            images: Array<string>;
            attributes: Array<{
                name: string;
                type: 0 (text) / 1 (number) / 2 (boolean) / 3 (colour) / 4 (size);
                value: any;
            }>;
        }>
* ##### Restricții: _niciuna_


### `GET` *{url}/products/:slug*
* ##### Request: _(empty)_
* ##### Response:
        {
            id: number;
            seller: string;
            categoryName: string;
            categorySlug: string;
            slug: string;
            name: string;
            longName: string;
            smallDescription: string;
            description: string;
            price: number;
            rating: number;
            image: string;
            images: Array<string>;
            attributes: Array<{
                name: string;
                type: 0 (text) / 1 (number) / 2 (boolean) / 3 (colour) / 4 (size);
                value: any;
            }>;
        }|null
* ##### Restricții: _niciuna_


### `GET` *{url}/products/:slug/related*
* ##### Request: _(empty)_
* ##### Response:
        Array<{
            id: number;
            seller: string;
            categoryName: string;
            categorySlug: string;
            slug: string;
            name: string;
            longName: string;
            smallDescription: string;
            description: string;
            price: number;
            rating: number;
            image: string;
            images: Array<string>;
            attributes: Array<{
                name: string;
                type: 0 (text) / 1 (number) / 2 (boolean) / 3 (colour) / 4 (size);
                value: any;
            }>;
        }>
* ##### Restricții: _niciuna_


### `GET` *{url}/account/general*
* ##### Request: _(empty)_
* ##### Response:
        {
            success: boolean = true;
            firstName: string;
            lastName: string;
            gender: number;
            phone: string;
            birthday: string;
            avatar: string;
         }
* ##### Restricții: authenticated


### `POST` *{url}/account/general*
* ##### Request:
    * **firstName:** required
    * **lastName:** required
    * **gender:** required, in(1, 2)
    * **phone:** required, numeric
    * **birthday:** required, date
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **firstName:** (array of strings) Can be "required".
      * **lastName:** (array of strings) Can be "required".
      * **gender:** (array of strings) Can be either "required" or "invalid".
      * **phone:** (array of strings) Can be either "required" or "phone".
      * **birthday:** (array of strings) Can be either "required" or "date".
   * **newToken:** (string) New JWT token; Present only if `success == true`
* ##### Restricții: authenticated


### `POST` *{url}/account/password*
* ##### Request:
    * **currentPassword:** required & the password of the current user
    * **newPassword:** required
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **currentPassword:** (array of strings) Can be "required" or "password".
      * **newPassword:** (array of strings) Can be "required".
* ##### Restricții: authenticated


### `GET` *{url}/account/personal*
* ##### Request: _(empty)_
* ##### Response:
   * **firstName:** (string)
   * **lastName:** (string)
   * **email:** (string)
   * **emailVerifiedAt:** (string|null)
   * **createdAt:** (string|null)
   * **updatedAt:** (string|null)
   * **avatar:** (string)
* ##### Restricții: authenticated


### `POST` *{url}/account/delete*
* ##### Request:
    * **email:** required & the e-mail of the current user
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **email:** (array of strings) Can be "email_wrong".
* ##### Restricții: authenticated


### `DELETE` *{url}/account/avatar*
* ##### Request: _(empty)_
* ##### Response:
   * **success:** (boolean) always true
   * **newAvatarUrl**: (string) new avatar URL for this user.
   * **newToken**: (string) new JWT token generated for this user
* ##### Restricții: authenticated


### `POST` *{url}/account/avatar*
* ##### Request:
    * **file:** required & file
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **file:** (array of strings) Can be "required" or "file".
   * **newAvatarUrl**: (string) new avatar URL for this user. _Present only if success is true!_
   * **newToken**: (string) new JWT token generated for this user. _Present only if success is true!_
* ##### Restricții: authenticated


### `GET` *{url}/account/addresses*
* ##### Request: _(empty)_
* ##### Response:
   ```
      Array<{
         id: number;
         firstName: string;
         lastName: string;
         phone: string;
         country: string;
         county: string;
         city: string;
         address: string;
         default: boolean;
      }>
   ```
* ##### Restricții: authenticated


### `POST` *{url}/account/addresses*
* Adds a new address for the current user.
* ##### Request:
   * **first_name:** required
   * **last_name:** required
   * **phone:** required & numeric
   * **country:** required & a valid country code
   * **county:** present, can be null
   * **city:** required
   * **address:** required
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **first_name:** (array of strings) Can be "required".
      * **last_name:** (array of strings) Can be "required".
      * **phone:** (array of strings) Can be "required" or "numeric".
      * **country:** (array of strings) Can be "required" or "invalid".
      * **county:** (array of strings) Can be "present".
      * **city:** (array of strings) Can be "required".
      * **address:** (array of strings) Can be "required".
   * **data**: (object) Present only if `success` is `true`.
      ```
      {
         id: number;
         firstName: string;
         lastName: string;
         phone: string;
         country: string;
         county: string;
         city: string;
         address: string;
         default: boolean;
      }
      ```
* ##### Restricții: authenticated


### `DELETE` *{url}/account/addresses*
* ##### Request:
   * **address_id:** required & exists in `delivery_addresses`, column `id`.
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **address_id:** (array of strings) Can be "required" or "exists".
   * **newAddresses**: (array) Present only if `success` is `true`.
      ```
         Array<{
            id: number;
            firstName: string;
            lastName: string;
            phone: string;
            country: string;
            county: string;
            city: string;
            address: string;
            default: boolean;
         }>
      ```
* ##### Restricții: authenticated


### `PUT` *{url}/account/addresses*
* Updates an existing address for the current user.
* ##### Request:
   * **id:** required & exists in `delivery_addresses`, column `id`.
   * **first_name:** required
   * **last_name:** required
   * **phone:** required & numeric
   * **country:** required & a valid country code
   * **county:** present, can be null
   * **city:** required
   * **address:** required
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **id:** (array of strings) Can be "required" or "exists".
      * **first_name:** (array of strings) Can be "required".
      * **last_name:** (array of strings) Can be "required".
      * **phone:** (array of strings) Can be "required" or "numeric".
      * **country:** (array of strings) Can be "required" or "invalid".
      * **county:** (array of strings) Can be "present".
      * **city:** (array of strings) Can be "required".
      * **address:** (array of strings) Can be "required".
   * **data**: (object) Present only if `success` is `true`.
      ```
      {
         id: number;
         firstName: string;
         lastName: string;
         phone: string;
         country: string;
         county: string;
         city: string;
         address: string;
         default: boolean;
      }
      ```
* ##### Restricții: authenticated


### `PATCH` *{url}/account/addresses*
* Marks an address as default.
* ##### Request:
   * **address_id:** required & exists in `delivery_addresses`, column `id`.
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (array)
      * **address_id:** (array of strings) Can be "required" or "exists".
   * **newAddresses**: (array) Present only if `success` is `true`.
      ```
         Array<{
            id: number;
            firstName: string;
            lastName: string;
            phone: string;
            country: string;
            county: string;
            city: string;
            address: string;
            default: boolean;
         }>
      ```
* ##### Restricții: authenticated


### `POST` */checkout*
* Inserts an order into the database (first step of checking out).
* ##### Request:
   * **cartId:** required
   * **paymentType:** required, either `cash` or `card`.
   * **shippingAddress:** required
     * id: number;
     * firstName: string;
     * lastName: string;
     * phone: string;
     * country: string;
     * county: string;
     * city: string;
     * address: string;
   * **billingAddress:** required
     * id: number;
     * firstName: string;
     * lastName: string;
     * phone: string;
     * country: string;
     * county: string;
     * city: string;
     * address: string;
   * **coupon:** string sau `null`
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (object of arrays)
   * **orderId**: (string) The new order's id.
   
### `POST` */checkout/pay*
* Pay for an order (second step of checking out).
* ##### Request:
   * **orderId:** required
   * **paymentType:** required, either `cash` or `card`.
   * **paymentMethod:** required
   * **paymentIntent:** not required; used if the card required further actions (like 3D secure).
* ##### Response:
   * **success:** (boolean)
   * **errrors**: (object of arrays)
   * ~~**orderId**: (string) The order's id.~~ **WILL BE REMOVED**
   * **intent**: (string) The intent generated for confirmation.
   * **error**: (string) The general error. Retry this with an added `paymentIntent` if this value is `authentication_required`.
   
   
### `GET` */orders*
* ##### Request: _(empty)_
* ##### Response:
   ```
      Array<{
         id: string;
         user: null or {
              id: number;
              firstName: string;
              lastName: string;
              email: string;
              emailVerifiedAt: string;
              gender: number;
              phone: string;
              birthday: string;
              avatar: string;
              admin: boolean;
              seller: boolean;
              sellerInfo: null or {
                 name: string;
                 slug: string;
                 image: string;
                 stripeConnectCompleted: boolean;
              };
         };
         payment: {
            type: 'cash' or 'card';
            completed: boolean;
         };
         coupon: {
            code: string or null;
            value: float;
         };
         sections: Array<{
           seller: {
              id: number;
              name: string;
              slug: string;
              image: string;
              phone: string;
              email: string;
              address: string;
              rating: number;
           };
           status: number;
           shipping: number;
           products: {
               productId: number;
               slug: string;
               name: string;
               image: string;
               price: number;
               quantity: number;
           };
         }>
         date: date;
         shipping: {
           firstName: string;
           lastName: string;
           phone: string;
           country: string;
           county: string;
           city: string;
           address: string;
         };
         billing: {
           firstName: string;
           lastName: string;
           phone: string;
           country: string;
           county: string;
           city: string;
           address: string;
         };
      }>
   ```
* ##### Restricții: authenticated
   
### `GET` */orders/{id}*
* ##### Request: _(empty)_
* ##### Response:
   ```
      {
         id: string;
         user: null or {
              id: number;
              firstName: string;
              lastName: string;
              email: string;
              emailVerifiedAt: string;
              gender: number;
              phone: string;
              birthday: string;
              avatar: string;
              admin: boolean;
              seller: boolean;
              sellerInfo: null or {
                 name: string;
                 slug: string;
                 image: string;
                 stripeConnectCompleted: boolean;
              };
         };
         payment: {
            type: 'cash' or 'card';
            completed: boolean;
         };
         coupon: {
            code: string or null;
            value: float;
         };
         sections: Array<{
           seller: {
              id: number;
              name: string;
              slug: string;
              image: string;
              phone: string;
              email: string;
              address: string;
              rating: number;
           };
           status: number;
           shipping: number;
           products: {
               productId: number;
               slug: string;
               name: string;
               image: string;
               price: number;
               quantity: number;
           };
         }>
         date: date;
         shipping: {
           firstName: string;
           lastName: string;
           phone: string;
           country: string;
           county: string;
           city: string;
           address: string;
         };
         billing: {
           firstName: string;
           lastName: string;
           phone: string;
           country: string;
           county: string;
           city: string;
           address: string;
         };
      }
   ```
* ##### Restricții: authenticated, only if the order has an user associated
   
