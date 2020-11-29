# VANIR API

### General Information:
1. All the fields in the **errors** in the response are not always present! They appear only if there is an error.
2. For endpoints with the method `GET`, the **request** is passed in the form of URL parameters.
___

### `POST` *{url}/api/login*
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


### `POST` *{url}/api/login*
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


### `POST` *{url}/api/forgot*
* ##### Request:
    * **email:** required & exists is _users_, column _email_
* ##### Response:
    * **success** (boolean)
    * **errors:** (array)
        * **email** (array of strings) Can be "invalid"
* ##### Restricții: _niciuna_


### `POST` *{url}/api/forgot/validate*
* ##### Request:
    * **email:** required & exists is _users_, column _email_ & exists is _password_resets_, column _email_
    * **token:** required
* ##### Response:
    * **success** (boolean)
    * **errors:** (array)
        * **email** (array of strings) Can be either "required" or "exists"
        * **token** (array of strings) Can be "required"
* ##### Restricții: _niciuna_


### `POST` *{url}/api/reset*
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


### `GET` *{url}/api/data/counties*
* ##### Request:
    * **country:** (momentan merge doar penru "ro")
* ##### Response: 
    Un array care conține o listă cu județele din țara specificată.
* ##### Restricții: _niciuna_


### `GET` *{url}/api/categories*
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


### `GET` *{url}/api/categories/:slug*
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


### `GET` *{url}/api/categories/:slug/products*
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


### `GET` *{url}/api/products*
* ##### Request: _(empty)_
* ##### Response:
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


### `GET` *{url}/api/products/:slug*
* ##### Request: _(empty)_
* ##### Response:
        ```
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
        ```
* ##### Restricții: _niciuna_


### `GET` *{url}/api/products/:slug/related*
* ##### Request: _(empty)_
* ##### Response:
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
