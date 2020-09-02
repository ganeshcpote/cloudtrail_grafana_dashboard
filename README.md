# Cloudtrail Grafana Dashboard


## Installation and Usage instructions
For those familiar with AWS. Lambda code is in **/lambda-code/** and you'll need to setup an event trigger on your CloudTrail bucket to call the Lambda function. Then visit the Grafana interface and import the **/dashboard/grafana-dashboard-export.json** file which imports the dashboard and all the required searches/virtualizations

### Part 1: Deploying
1. Git clone the repo or download the whole thing from the release page

2. Create Lambda function using **/lambda-code/index.js** file with following environment variables
   * elasticsearchurl	
   * snsTopicArn	
  
3. Go to S3 cloudtrail bucket where all the events are generated by cloudtrail
   * Browse to your bucket and select **Properties** and **events**
   ![S3config](/images/image1.png)

   * Create a new event filter on **put** operations and select your lambda function from the drop down!
   ![S3config](/images/image2.png)
 
4. Now cloudtrail logs written to S3 events should be starting to be processed by the cloudtrail lambda function and will start pushing those into elasticsearch. You can check by looking at the ElasticSearch index's. You should see an index titled logstash-YYYY-MM-DD

### Part 2: Setting up the dashboard
1. Now you can visit your Grafana URL

2. Click import and select the **/dashboard/grafana-dashboard-export.json** file.
![kibanaImport](/images/image3.png)

4. If all goes successfully you should see the following saved objects post the import. You can now go and view your dashboard by going to **Dashboard** selecting **open** and selecting **Main-Dashboard**
  ![GrafanaPostImport](/images/image4.png)

  ![GrafanaPostImport](/images/image5.png)
