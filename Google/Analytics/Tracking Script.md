# I. Accessing Google Analytics API
**Case :**  
I allready implement google analytics and i want to display analytics report directly from my dashboard app
**Update Version:**  
version 1 - 16 Nov 2018

**Environment**  
- Frontend Environment : html + js
- Backend : laravel
- Programming Tool : VS code

**Docs**  
https://analytics.google.com

**Step by Step**
  
1. Register and create or select your project. **https://analytics.google.com**

2. Go to **https://analytics.google.com/analytics/web**. On section **Property** choose **Tracking Info** and click **Tracking Code**

3. Embbedd the code 
   Copy your Global Site Tag to your base template of your website. Since i'm using laravel and blade, i'll put it on my root template/parent of the page. And put (something like) this code insed the **head tag** of the page.
   ``` 
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script async src="https://www.googletagmanager.com/gtag/js?id=UA-YOUR_CODE"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());

        gtag('config', 'UA-YOUR_CODE');
    </script>
   ``` 
4. Done