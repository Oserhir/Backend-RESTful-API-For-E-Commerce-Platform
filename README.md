# My Ecommerce Software Requirements

## The features in the API :

- Signing Up, signing in and signing out of users
- Password forgot/reset, confirmation email on signup \*
- Authentication using JSON Web Tokens (JWT).
- Advance searching, sorting, pagination and filtering
- Schema Validation using Express-Validator
- Credit card payment with stripe \*
- Cash on delivery (no online payment required) \*
- Image Upload & Multiple Images Upload and image processing
- Star rating system
- Discount coupon code \*
- Add to wishlist
- Add to cart \*

## Back-end project structure

- index.js
- config
  - database.js
- controllers
  - auth.js
  - brand.js
  - category.js
  - product.js
  - subcategory.js
  - user.js
- middlewares
  - errorMiddleware.js
  - validatorMiddleware.js
- models
  - brands.js
  - category.js
  - product.js
  - subcategory.js
  - user.js
- router
  - auth.js
  - brand.js
  - category.js
  - product.js
  - subcategory.js
  - user.js
- utils
  - APIError.js
  - dummyData
    - seeder.js
    - products.json
  - validators
    - BrandValidators.js
    - categoryValidators.js
    - productValidators.js
    - subCategoryValidators.js

## Database

All the models can be found in the models directory created using mongoose.

User Schema:

- name (String)
- email (String)
- password (String)
- Role(Number)
- history(array)
- Wishlist [ { ObjectId - a reference to the product schema } ]

Category Schema:

- title (String)
- slug (String)
- image (String)

subCategory Schema:

- title (String)
- slug (String)
- category (ObjectId - a reference to the category schema)

brand Schema:

- title (String)
- image (String)

Product Schema:

- title (String)
- slug (String)
- description (String)
- quantity (Number)
- price (Number)
- sold (Number)
- priceAfterDiscount (Number)
- Color ([String])
- imageCover (string)
- images ([String])
- category (ObjectId - a reference to the category schema)
- subcategories (ObjectId - a reference to the subcategories schema)
- brand (ObjectId - a reference to the brand schema)
- ratingsAverage (number)
- ratingsQuantity (number)
- shipping (Boolean)

Review Schema:

- title (String)
- ratings (Number)
- user (ObjectId - a reference to the User schema)
- product (ObjectId - a reference to the product schema)

## Route

Auth Routes:

| @Route      | @Type | @access | @desc                       |
| ----------- | ----- | ------- | --------------------------- |
| /api/signup | GET   | Private | sign up page                |
| /api/signup | POST  | Private | create a new user in db     |
| /api/login  | GET   | Private | log in page                 |
| /api/login  | POST  | Private | authenticate a current user |
| /api/logout | GET   | Private | log a user out              |

User Routes:

| @Route               | @Type | @access | @desc                                 |
| -------------------- | ----- | ------- | ------------------------------------- |
| /api/profile/:userId | GET   | Private | retrieve a user's profile information |

Product Routes:

| @Route                                 | @Type  | @access | @desc                          |
| -------------------------------------- | ------ | ------- | ------------------------------ |
| /api/products/create/:userId           | POST   | Private | Add new product                |
| /api/products/:productId               | GET    | Private | Get a single product           |
| /api/products/:productId/:userId"      | PUT    | Private | Update a product               |
| /api/products/:productId/:userId"      | DELETE | Private | Delete a product               |
| /api/products/related/:productId/      | GET    | Public  | Get related products           |
| /api/products/search                   | POST   | Public  | Product Search                 |
| /api/products/                         | GET    | Public  | Get all products               |
| /api/products?limit=3                  | GET    | Public  | Limit results                  |
| /api/products?sortedBy=price           | GET    | Public  | Sort results                   |
| /api/products?keyword=Clark,Olsen      | GET    | Public  | Search by title or description |
| /api/products?ratingsAverage[gte]=1.6  | GET    | Public  | Filter results                 |
| /api/products?fields=title,description | GET    | Public  | Field Limiting                 |

Category Routes:

| @Route                                  | @Type  | @access | @desc                                                       |
| --------------------------------------- | ------ | ------- | ----------------------------------------------------------- |
| /api/category/create/:userId            | POST   | Private | Add new Category                                            |
| /api/category/?limit=1                  | GET    | Public  | Get List of Categories ( Limit results)                     |
| /api/category/?page=2&limit=1           | GET    | Public  | Get List of Categories                                      |
| /api/category/:categoryId               | GET    | Public  | Get specific Category                                       |
| /api/category/:categoryId/:userId       | PUT    | Private | Update specific Category                                    |
| /api/category/:categoryId/:userId       | DELETE | Private | Delete specific Category                                    |
| /api/category/:categoryId/subcategories | GET    | Public  | Get All Subcategories for Specific Category ( Nested Route) |
| /api/category/:categoryId/subcategories | POST   | Public  | Create Subcategory on Category ( Nested Route)              |

subCategory Routes:

| @Route                                    | @Type  | @access | @desc                                      |
| ----------------------------------------- | ------ | ------- | ------------------------------------------ |
| /api/subcategories/create/:userId         | POST   | Private | Add new subCategory                        |
| /api/subcategories/?limit=1               | GET    | Public  | Get List of subCategories ( Limit results) |
| /api/subcategories/?page=2&limit=1        | GET    | Public  | Get List of subCategories                  |
| /api/subcategories/:subCategoryId         | GET    | Public  | Get specific subCategory                   |
| /api/subcategories/:subCategoryId/:userId | PUT    | Private | Update specific subCategory                |
| /api/subcategories/:subCategoryId/:userId | DELETE | Private | Delete specific subCategory                |

Brand Routes:

| @Route                      | @Type  | @access | @desc                 |
| --------------------------- | ------ | ------- | --------------------- |
| /api/brand/create/:userId   | POST   | Private | Add new Brand         |
| /api/brand/?page=2&limit=1  | GET    | Public  | Get List of Brands    |
| /api/brand/:brandId         | GET    | Public  | Get specific Brand    |
| /api/brand/:brandId/:userId | PUT    | Private | Update specific Brand |
| /api/brand/:brandId/:userId | DELETE | Private | Delete specific Brand |

Review Routes:

| @Route                           | @Type  | @access | @desc                                                  |
| -------------------------------- | ------ | ------- | ------------------------------------------------------ |
| /api/reviews/create/:userId      | POST   | Private | Add new Review                                         |
| /api/reviews/?page=2&limit=1     | GET    | Public  | Get List of reviews                                    |
| /api/reviews/:reviewId           | GET    | Public  | Get specific review                                    |
| /api/reviews/:reviewId/:userId   | PUT    | Private | Update specific review                                 |
| /api/reviews/:reviewId/:userId   | DELETE | Private | Delete specific review                                 |
| /api/products/:IdProduct/reviews | GET    | Public  | Get all reviews on specifique products ( Nested Route) |

wishlist Routes:

| @Route                           | @Type  | @access | @desc                        |
| -------------------------------- | ------ | ------- | ---------------------------- |
| /api/wishlist/:userId            | POST   | Private | Add Product To Wishlist      |
| /api/wishlist/:ProductId/:userId | DELETE | Private | Remove Product From Wishlist |
| /api/wishlist/:userId            | GET    | Public  | Get Logged User Wishlist     |

## Validation Layer

Category:

| Attribute name | Notes                      |
| -------------- | -------------------------- |
| name \*        | String,min 3,max 32,unique |
| slug           | String,lowercase           |

subCategory:

| Attribute name | Notes                                         |
| -------------- | --------------------------------------------- |
| name \*        | String,min 3,max 32,unique                    |
| slug           | String,lowercase                              |
| category \*    | subCategory must be belong to parent category |

Brand:

| Attribute name | Notes                      |
| -------------- | -------------------------- |
| name \*        | String,min 3,max 32,unique |
| image          | String                     |

Product:

| Attribute name     | Notes                                                               |
| ------------------ | ------------------------------------------------------------------- |
| title \*           | String,min 3,max 100                                                |
| slug \*            | String,lowercase                                                    |
| description \*     | String , min 20                                                     |
| quantity \*        | Number                                                              |
| sold               | Number , default: 0                                                 |
| price \*           | Number, max: 200000                                                 |
| priceAfterDiscount | Number , priceAfterDiscount must be lower than price                |
| colors             | [String]                                                            |
| imageCover \*      | String                                                              |
| images             | [String]                                                            |
| category           | Valid MongoDB ObjectId ,Validate Category Existence in The DB       |
| subcategories      | Valid MongoDB ObjectId , Validate Subcategories Existence in Our DB |
| ratingsAverage     | Number min 1,max 5                                                  |
| ratingsQuantity    | Number default: 0                                                   |
| shipping           | boolean                                                             |

Review:

| Attribute name | Notes                                  |
| -------------- | -------------------------------------- |
| title          | String                                 |
| ratings        | Number,min 1,max 5,required            |
| user           | ObjectId (User) ,required              |
| product        | ObjectId (Product) ,isMongoId,required |

## Technology

I use Express on NodeJs for the server, MongoDB to store data as document in JSON format and Mongoose for modeling.

The application is built with:

- express 4.18.2
- mongoose 6.6.5
- dotenv 16.0.3
- bcrypt 5.1.0
- body-parser 1.20.1
- cookie-parser 1.4.6
- express-jwt 7.7.7
- joi 17.6.3
- jsonwebtoken 8.5.1
- uuid 9.0.0
- multer 1.4.5-lts.1
- slugify 1.6.5

## Run

To run this application, you have to set your own environmental variables. For security reasons, Below are the variables that you need to set in order to run the application:

- MONGO_URI
- JWT_SECRET

<!-- 
## How to use it


Products :

Get all products

```JavaScript
fetch('https://x.com/products')
    .then(res=>res.json())
    .then(json=>console.log(json))
```
-- >
