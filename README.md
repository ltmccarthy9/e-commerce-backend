# e-commerce-backend

## Description
This application allows you to interact with an ecommerce themed database to send GET, POST,
PUT, and DELETE requests to a database to view and update products/categories/tags in the database as you wish.
For this application you can use Insomnia to interact with the database. 

## Technologies Used
* Javascript
* Express
* Sequelize
* mySQL
* Insomnia
* Visual Studio Code
* Git
* Gitbash
* mySQL shell
* command line

## Installation 
Clone or copy over this repository.  Before interacting with the databse you will have to open up 
mySQL shell or workbench and create the database using the schema.sql file.  Next you will have to run npm
install to install the correct dependancies.  After this, run "npm run seed" in your terminal to seed the database
tables with some default values.  Next open insomnia and send some calls to your routes.

## Video Demonstration

https://drive.google.com/file/d/1mp3EWM4XOWlTB6HNGf2tp_fcqSnXiZs0/view < - - - - - - - - - - -

## Code 

```Javascript
router.get('/:id', async (req, res) => {
  try {
    const productData = await Product.findByPk(req.params.id, {
      include: [
        {
          model: Category,
          attributes: ['category_name'],
        },
        {
          model: Tag,
          attributes: ['tag_name'],
        },
        ]
    });
    if (!productData) {
      res.status(404).json({ message: "No product with this id"});
      return;
    }

    res.status(200).json(productData);
  } catch (err) {
    res.status(500).json(err)
  }
});
```
Here is an example route to get a single row from the Product table using an id search parameter.

```Javascript
router.post('/', async (req, res) => {
  try {
    const categoryData = await Category.create(req.body);
    res.status(200).json(categoryData);
  } catch (err) {
    res.status(400).json(err);
  }
});
```
This is a post route to add a new category to the Category table.

## License 
MIT License

Copyright (c) 2022 Liam McCarthy

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
