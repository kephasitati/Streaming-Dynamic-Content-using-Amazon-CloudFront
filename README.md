# Streaming Dynamic Content using Amazon CloudFront

## Lab Overview and Objectives

This repository contains the instructions and code for a lab that demonstrates how to use Amazon CloudFront to deliver a dynamic, multiple bit-rate stream to a connected device using Apple's HTTP Live Streaming (HLS) protocol. The lab also utilizes Amazon Elastic Transcoder to convert a source video into multiple bit-rates that are delivered through CloudFront.

### Objectives

After completing this lab, you should be able to:

1. Create multiple bit-rate versions of a given source media file using Amazon Elastic Transcoder.
2. Use Amazon CloudFront to deliver the dynamic (multi bit-rate) stream created by Amazon Elastic Transcoder.

## Getting Started

Before starting the lab, ensure that you have the necessary AWS credentials and permissions to create resources such as S3 buckets, CloudFront distributions, and Elastic Transcoder pipelines.

## Task 1: Set Up the Environment

1. In the AWS Management Console, navigate to the S3 service.
2. Open the S3 bucket named "awstrainingreinvent."
3. Inside the bucket, locate the "input" folder, which contains a sample video file named "AmazonS3Sample.mp4."

**Note:** If the file is not immediately visible, wait for up to ten minutes or manually refresh the bucket content.

## Task 2: Create an Amazon CloudFront Distribution

1. In the AWS Management Console, go to the CloudFront service.
2. Choose "Create a CloudFront distribution."
3. Under "Origin Settings," select the S3 bucket created earlier with "awstrainingreinvent" in its name.
4. Leave "Origin access" as Public.
5. Under "Web Application Firewall (WAF)," select "Do not enable security protections."
6. Scroll to the bottom and choose "Create Distribution."

## Task 3: Create an Amazon Elastic Transcoder Pipeline

### Create a Pipeline

1. In the AWS Management Console, go to the Elastic Transcoder service.
2. Choose the same region as the S3 bucket.
3. On the Pipelines page, select "Create a new Pipeline."
4. Enter "InputPipeline" as the Pipeline Name.
5. For "Input Bucket," select the "awstrainingreinvent" S3 bucket.
6. For "IAM Role," choose "AmazonElasticTranscoderRole."
7. In the S3 Bucket settings, configure the bucket and storage class.
8. In the Thumbnails settings, configure the bucket and storage class.
9. Choose "Create Pipeline."

### Create a Job

1. On the Pipelines page, choose "Create New Job" within the "InputPipeline."
2. For "Output Key Prefix," enter "output/".
3. For "Input Key," select the input file labeled "input/AmazonS3Sample.mp4."

### Configure Output Details

Configure three output files for bit-rates (2Mbps, 1.5Mbps, and 1Mbps).

1. Select "System preset: HLS 2M" for the first preset.
2. Enter details for the second and third presets.
3. Click "+ Add Another Output" for each additional preset.

### Configure a Playlist

1. Under "Playlists (Adaptive Streaming)," choose "Add Playlist."
2. Configure the playlist with the name "primary," format "HLSv3," and select all three outputs.
3. Choose "Create New Job."

## Task 4: Test Playback of the Dynamic Stream

### Construct the Playback URL

1. Obtain the CloudFront domain name from the CloudFront distribution created earlier.
2. Obtain the playlist file path from the S3 bucket.

### Test Playback

1. Construct the playback URL by combining the CloudFront domain name and playlist file path.
2. Type the URL into the default browser of an iOS or Android device or a computer browser.
3. The stream should start playing, dynamically adjusting based on bandwidth and CPU conditions.

## Conclusion

Congratulations! You have successfully completed the lab, learning to use AWS services like Amazon S3, Amazon Elastic Transcoder, and Amazon CloudFront to deliver HLS media files to iOS or Android devices.
