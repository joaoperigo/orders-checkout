# Checkout and orders app
## Instructions
###
```
git clone https://github.com/joaoperigo/orders-checkout
cd app-devio
npm install
```
### Run Backend server (json-server)
```
npm run backend
```
### Run Frontend server
```
npm run serve
```

## About
The checkout screen is focused on mobile viewports. And cozinha (kitchen) in desktop. The retirada (withdraw), in both.
The primary color is used in main actions. Secondary in less important. Tertiary in the focused objects. White, exceptionaly in views menu, not a main flow event.
### Link to figjam
To see some roughs of this test [click here](https://www.figma.com/file/C5WLDdWNkRC4e5NNysbyuw/Teste-DEVIO?node-id=0%3A1)
### Conclusion
#### Implement in next sprint
Some compability problems with sass-loader and oher dependencies
Study values for alts in images
Develope better warning in feedbacks
Implement money mask value in button pay
Implement forms validators
Insert some add, remove button, in featured produts
Suggest client table number in crud to PO
Try some foreign key, to get name of products, instead of create a new value in pedido.produto.titulo, use the name o product, selected by the pedido.produto.id
Change name of AllProductList, to something like CheckoutCrud
Only get value from cliente name input after insert some letters
Implement form layout in search, like insert name
Suggest client name edit
Install font inside application with @font-face, instead of google cdn
Started Observations, but couldn’t finish
Missed some extras in requirements
Need mor time to get better layout
Need more time to organize scss and css style structure
For now retirada (withdraw)  is a copy of cozinha (kitchen)
