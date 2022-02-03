# Prepering the jscongif 
- I use jsconfig for easy routing and importing 
- In this way I can easy and more effectively import and export my pages and components
```javascript 
<!-- Code of jsconfig -->
{
    "compilerOptions": {
      "baseUrl": ".",
      "paths": {
        "@pages/*": ["pages/*"],
        "@components/*": ["components/*"],
        "@styles/*": ["styles/*"],
        "@content/*": ["content/*"],
        "@utils/*": ["utils/*"]
      }
    }
  }
  ```
 
