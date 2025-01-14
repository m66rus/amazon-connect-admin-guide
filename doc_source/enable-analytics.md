# Enable Contact Lens for Amazon Connect<a name="enable-analytics"></a>

You can enable Contact Lens in just a few steps\. Just add a [Set recording and analytics behavior](set-recording-behavior.md) block to a flow, and configure it for Contact Lens\.

**To enable Contact Lens in a contact flow**

1. Add the [Set recording and analytics behavior](set-recording-behavior.md) block to a contact flow\.

1. In the contact block, under **Call recording**, choose **On**, **Agent and Customer**\.

   Both agent and customer call recordings are required to use Contact Lens\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

1. Select **Enable Contact Lens for speech analytics**\.

   If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update instance settings](update-instance-settings.md)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior2.png)

1. Choose one of the following:
   + **Post\-call analytics**: Contact Lens analyzes the call recording after the conversation and After Contact Work \(ACW\) is complete\. This option provides the best transcription accuracy\.
   + **Real\-time analytics**: Contact Lens provides both real\-time insights during the call, and post\-call analytics after the conversation has ended and After Contact Work \(ACW\) is complete\.

     If you choose this option, we recommend setting up alerts based on keywords and phrases that the customer may utter during the call\. Contact Lens analyzes the conversation real\-time to detect the specified keywords or phrases, and alerts supervisors\. From there, supervisors can listen in on the live call and provide guidance to the agent to help them resolve the issue faster\.

     For information about setting up alerts, see [Alert supervisors in real\-time based on keywords and phrases](add-rules-for-alerts.md)\.

     If your instance was created before October 2018, additional configuration is needed to access real\-time analytics\. For more information, see [Service\-linked role permissions for Amazon Connect](connect-slr.md#slr-permissions)\.

1. Choose the language\. For a list of available languages for various Contact Lens features, see [Supported languages](supported-languages.md)\.

   For instructions on using an attribute, see [Use contact attributes](#dynamically-enable-analytics-contact-flow)\.

1. Choose **Save**\.

1. If the contact is going to be transferred to another agent or queue, repeat these steps to add another [Set recording and analytics behavior](set-recording-behavior.md) block with **Enable Contact Lens for speech analytics** enabled\. 

**Tip**  
If you want to continue using Contact Lens to collect data after transferring a contact to another agent or queue, you need to add another [Set recording and analytics behavior](set-recording-behavior.md) block with **Enable analytics** enabled for the flow\. This is because a transfer generates a second contact ID and CTR\. Contact Lens needs to run on that CTR as well\.

## How to enable redaction of sensitive data<a name="enable-redaction"></a>

To enable redaction of sensitive data in a contact flow, choose **Redact sensitive data**\. No other configuration is needed\. Contact Lens determines what data can be redacted\.

For more information about using redaction, see [Use sensitive data redaction](sensitive-data-redaction.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-enable-redaction.png)

## Review sensitive data redaction for accuracy<a name="review-sensitive-data-redaction"></a>

The redaction feature is designed to identify and remove sensitive data\. However, due to the predictive nature of machine learning, it may not identify and remove all instances of sensitive data in a transcript generated by Contact Lens\. We recommend you review any redacted output to ensure it meets your needs\.

**Important**  
The redaction feature does not meet the requirements for de\-identification under medical privacy laws like the U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\), so we recommend you continue to treat it as protected health information after redaction\.

For the location of redacted files and examples, see [Example Contact Lens output files](contact-lens-example-output-files.md)\.

## Dynamically enable Contact Lens using contact attributes<a name="dynamically-enable-analytics-contact-flow"></a>

You can dynamically enable Contact Lens and the redaction of the output files based on the language of the customer\. For example, for customers using en\-US, you may want only a redacted file whereas for those using en\-GB, you may want both the original and redacted output files\.
+ Redaction: choose one of the following \(they are case sensitive\)
  + None
  + RedactedOnly
  + RedactedAndOriginal
+ Language: Choose from the [list of available languages](supported-languages.md#supported-languages-contact-lens)\.

You can set these attributes in the following ways:
+ User defined: use a **Set contact attributes** block\. For general instructions about using this block, see [How to reference contact attributes](how-to-reference-attributes.md)\. Define the **Destination key** and **Value** for redaction and language as needed\. 

  The following image shows how to use contact attributes for redaction\. Note that **Value** is case sensitive\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction1.png)

  The following image show how to use contact attributes for language:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction2.png)
+ [Use a Lambda function](attribs-with-lambda.md)\. This is similar to how you set up user\-defined contact attributes\. An AWS Lambda function can return the result as a key\-value pair, depending on the language of the Lambda response\. The following example shows a Lambda response in JSON: 

  ```
  {
     'redaction_option': 'RedactedOnly',
     'language': 'en-US'
  }
  ```

## Availability of Contact Lens features by Region<a name="regions-contactlens"></a>


| Region | Post\-call analytics | Real\-time analytics | Extended language support  | 
| --- | --- | --- | --- | 
|  US East \(N\. Virginia\)  | Yes  | Yes  | Yes  | 
|  US West \(Oregon\)   | Yes  | Yes  | Yes  | 
|  Canada \(Central\)   | Yes  | Yes  | Yes  | 
|  Europe \(Frankfurt\)  | Yes  | Yes  | Yes  | 
|  Europe \(London\)  | Yes  | Yes  | Yes  | 
|  Asia Pacific \(Singapore\)  | Yes | \-  | \-  | 
|  Asia Pacific \(Sydney\)  | Yes  | Yes  | Yes  | 
|  Asia Pacific \(Tokyo\)  | Yes  | Yes  | Yes  | 