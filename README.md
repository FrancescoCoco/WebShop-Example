# WEB SHOP 
> The idea of this project is to reproduce the functionality of a web shop locally. 

[![][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Downloads Stats][npm-downloads]][npm-url]

> Technologies: 

- Angular
- NodeJS Server 
- Stripe 

## ANGULAR COMMANDS 
- Create Project

    ```
    ng new store 
    ```
- Install node_module 
    ```
    npm i 
    ```
- Add dependencies 
    ``` 
    npm i name_of_dependencies
    ```
- Components
    ```
    ng g c Components/name_component
    ```
- Interface 
    ```
    ng g i Models/nome_models
    ```
- Service 
    ```
    ng g s Services/nome_services
    ```

## PRELIMINARY OPERATIONS

- Install [NodeJS](https://nodejs.org/it/download/)
- Install AngularCli from your terminal
    ```
  npm i @angular/cli@14.2.1
    ```

- Install [angular material](https://material.angular.io/components/categories)   
    ```
    ng add @angular/material
    ```
- Use [tailwindcss](https://tailwindcss.com) 
    ```
    npm install -D tailwindcss postcss autoprefixer
    ```
    ```
    npx tailwindcss init
    ```

- In file [server.js](./server/server.js) you need to insert your private key in line 13


## Installation
After you pull this repository, go to folder store. 

To execute the project run these commands: 

```
npm install 
ng serve --open
```

In another terminal run this commands: 

```
cd server 
```
```
npm init -y
```
```
npm i cors@2.8.5 express@4.18 stripe@10.7.0
```
```
node server.js
```


## Release History
* 0.2.0
    * Add implementation of cluster k8s

* 0.1.0
    * Complete Project
* 0.0.1
    * Work in progress


## Dependencies 

    "dependencies": {
        "@angular/animations": "^15.0.0",
        "@angular/cdk": "^15.0.3",
        "@angular/common": "^15.0.0",
        "@angular/compiler": "^15.0.0",
        "@angular/core": "^15.0.0",
        "@angular/forms": "^15.0.0",
        "@angular/material": "^15.0.3",
        "@angular/platform-browser": "^15.0.0",
        "@angular/platform-browser-dynamic": "^15.0.0",
        "@angular/router": "^15.0.0",
        "@stripe/stripe-js": "1.35",
        "rxjs": "~7.5.0",
        "tslib": "^2.3.0",
        "zone.js": "~0.12.0"
    },
    "devDependencies": {
        "@angular-devkit/build-angular": "^15.0.4",
        "@angular/cli": "~15.0.4",
        "@angular/compiler-cli": "^15.0.0",
        "autoprefixer": "^10.4.13",
        "postcss": "^8.4.20",
        "tailwindcss": "^3.2.4",
        "typescript": "~4.8.2"
    }

## PAGES OF APPLICATION 

- Homepage 
    ![Home-Page]
    ![Home-Page-Cart]
- Cart-Page
    ![Cart-Page]
- Stripe CheckOut-Page
    ![CheckOut]


## IMPLEMENTATION OF K8S Cluster 
* The idea is to reproduce locally the functionality of a cloud system using k8s with minikube. 
Above you can visualize the steps to execute it:
    -  First of all open your terminal and digits: 
    
        ```minikube start --driver=hiperkit```
    It's important to use hiperkit because default minikube start with docker driver.
    - We modify the angular/json of the file and we insert the option 
    
        ``` "baseHref": "/store/" ```
    - Now generate the build of the web-app: 
     
        ``` ng build  ```
    -  Now you can build the docker image from the Dockerfile inside WebShop Folder: 
        
        ``` docker build -t webshop-image:v1 . ```

    - If you digit: ``` docker images  ```
     you can visualize it 
    
    - Tag the image with the commands: 
       
       ```docker tag webshop-image:v1 usernamedocker/webshop-image:v1 ```

    - Push image in the docker hub: 

        ```docker push usernamedocker/webshop-image:v1 ```

    - Now you can use the store-deployment.yaml file: 
        
        ``` kubectl apply -f store-deployment.yaml  ```

    - Go to the folder server and repeat the operation for the nodejs server:
        
        ``` docker build -t store-image:v1 . ```
        
        ```docker tag store-image:v1 usernamedocker/store-image:v1 ```

         ```docker push usernamedocker/store-image:v1 ```

        ``` kubectl apply -f server-deployment.yaml  ```
    
    - Return to the main folder and run the ingress: 

        ``` kubectl apply -f store-ingress.yaml  ```

    - Open your file hosts and insert this line: 

        ``` <your_minikubeip> storeweb.info```
    
    - Open browser and goes to: 
       
       ``` storeweb.info/store ```

    

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
[Home-Page]: utils/HomePage.png
[Home-Page-Cart]: utils/HomePageCart.png
[Cart-Page]: utils/CartPage.png
[CheckOut]: utils/StripeCheckOutPage.png
[NPM VERSION]: 'v9.2.0'
