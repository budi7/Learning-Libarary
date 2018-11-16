# I. Accessing Google Analytics API
**Case :**  
I allready implement google analytics and i want to display analytics report directly from my dashboard app
**Update Version:**  
version 1 - 15 Nov 2018

**Environment**  
- Frontend Environment : html + js
- Backend : laravel
- Programming Tool : VS code

**Docs**  
server side api : https://developers.google.com/analytics/devguides/reporting/core/v3/quickstart/web-php  
registering api credential access : https://support.google.com/analytics/answer/1009702  
plugins : https://github.com/spatie/laravel-analytics

**Step by Step**
  
1. Register and create or select your project. **https://analytics.google.com**

2. Create service Account for your project **https://console.developers.google.com/iam-admin/serviceaccounts**.  
   Select project and click **Create Service Account**. Fill the required info and download the JSON file in the end of the process.

3. Go to vs code and run **composer require spatie/laravel-analytics**.  
   Add the following code to app/config.php
   ```
   'providers' => [
        ...
        Spatie\Analytics\AnalyticsServiceProvider::class,
        ...
    ];

    'aliases' => [
        ...
        'Analytics' => Spatie\Analytics\AnalyticsFacade::class,
        'Period' => Spatie\Analytics\Period::class,
        ...
    ];    
   ```  
4. Copy key to project directory  
   Copy the downloaded json from google analytics to your "\\Project dir\web\storage".  
   **Optional**  
   You don't want to make your secret json to viewed by everybody on github don't you? So, ignore this file from git list.  

5. Enable google API
   Go to **https://console.developers.google.com/apis/dashboard?** and select your project. Click **Enable APIS And Services**, and choose **Google Analytics Reporting API** service. Click **Enable**.

6. Obtain google analytics view id
   Go to **https://analytics.google.com/analytics/web/**. Go to Admin and choose **View Settings** on **View** section. There is your view ID, copy it and we will use it on next step. 

7. Edit your .env file
   Add this to your env
   ```
    GOOGLE_ANALYTICS_VIEW_ID="Your View id"
    GOOGLE_JSON_KEY_PATH="Your Downloaded JSON Filename".json
   ```  
    run **composer dump-autoload -o** afterwhile  
8. Retrieve report from Analytics API
   Create a new function/traits/or whatever you like to and here's the code to query the API :
   ```
    // displaying 7 days analytics report
    // go to https://github.com/spatie/laravel-analytics for more period option
    $analytics = Analytics::fetchVisitorsAndPageViews(Period::days(7));
   ```
   Example:
   ```
    private function getAnalytics(){
        // Get analytics data
        $analytics = Analytics::fetchVisitorsAndPageViews(Period::days(7));

        if(!$analytics){
            // API wont return any value
            return [];
        }
        
        // format data
        $formatted_data = [];
        foreach ($analytics as $key => $analytic) {
            // format date as string 
            $tmp_date = Carbon::createFromFormat('Y-m-d H:i:s', $analytic['date'], 'GMT+7');

            $tmp = [
                'date' => $tmp_date->format("d M Y"),
                'visitors' => $analytic['visitors'],
                'pageViews' => $analytic['pageViews'],
            ];
            array_push($formatted_data, $tmp);
        }

        return $formatted_data;
    }   
   ```
9. JS inegration ?
    If you need to pass it to js variable (ie: draw graph or so) here's the code
   ```
   // retrive from php
    var data_source = {!! json_encode($page_datas->analytics) !!};

    // grouping data?
    var ds_date = [], ds_visitors = [];

    data_source.forEach(function(element) {
        ds_date.push(element.date);
        ds_visitors.push(element.visitors);
    });
   
   ```
    
   


