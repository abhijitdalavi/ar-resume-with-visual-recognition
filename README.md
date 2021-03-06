*Read this in other languages: [中国](README-cn.md).*
# Use Watson Visual Recognition and Core ML to create an Augmented Reality based résumé

The easiest way to find and connect to people around the world is through social media apps like Facebook, Twitter and LinkedIn. These, however, only provide text based search capabilities. However, with the recently announced release of the iOS ARKit toolkit, search is now possible using facial recognition. Combining iOS face recognition using Vision API, classification using IBM Visual Recognition, and person identification using classified image and data, one can build an app to search faces and identify them. One of the use cases is to build a Augmented Reality based résumé using visual recognition.

The main purpose of this code pattern is to demonstrate how to identify a person and his details using Augmented Reality and Visual Recognition. The iOS app recognizes the face and presents you with the AR view that displays a résumé of the person in the camera view. The app classifies a person face with Watson Visual Recognition and Core ML. The images are classified offline using a deep neural network that is trained by Visual Recognition.

After completing this code pattern a user will know how to:

* Configure ARKit
* Use the iOS Vision module
* Create a Swift iOS application that uses the Watson Swift SDK
* Classify images with [Watson Visual Recognition](https://www.ibm.com/watson/services/visual-recognition/) and [Core ML](https://developer.apple.com/machine-learning/)

# Flow
![ARResume Architecture](https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/architecture.png)

1. User opens the app on their mobile
2. A face is detected using the iOS Vision module
3. An image of the face is sent to Watson Visual Recognition to be classified
5. The information from the JSON database related to the user is placed in front of the original person's face in the mobile camera view

# Included Components

* [ARKit](https://developer.apple.com/arkit/): ARKit is an augmented reality framework for iOS applications.
* [Watson Visual Recognition](https://www.ibm.com/watson/developercloud/visual-recognition.html): Visual Recognition understands the contents of images - visual concepts tag the image, find human faces, approximate age and gender, and find similar images in a collection.
* [Core ML](https://developer.apple.com/documentation/coreml): With Core ML, you can integrate trained machine learning models into your app.

# Technologies

* [Artificial Intelligence](https://medium.com/ibm-data-science-experience): Artificial intelligence can be applied to disparate solution spaces to deliver disruptive technologies.
* [Mobile](https://mobilefirstplatform.ibmcloud.com/): Systems of engagement are increasingly using mobile technology as the platform for delivery.

# Watch the Video

[![](https://i.ytimg.com/vi/FyeEF0Rb154/0.jpg)](https://youtu.be/M3WlymI1J9E)

# Steps

> As an alternative to the steps below, you can [create this project as a starter kit](https://cloud.ibm.com/developer/appledevelopment/starter-kits/visual-recognition-with-core-ml-and-arkit-for-ios-with-watson) on IBM Cloud, which automatically provisions required services, and injects service credentials into a custom fork of this pattern.

1. At a command line, clone this repo:
```bash
git clone https://github.com/IBM/ar-resume-with-visual-recognition
```

2. Log into [IBM Cloud](https://cloud.ibm.com) account and create a [Watson Visual Recognition](https://cloud.ibm.com/catalog/services/visual-recognition) service. Create a set of credentials and identify your API key.

3. When the app loads, it also loads 3 Core ML models which is bundled part of the app. The models were trained using IBM Watson Visual Recognition Tool and downloaded as Core ML model.
> To create a new classifier use the [Watson Visual Recognition tool](https://cloud.ibm.com/catalog/services/visual-recognition). A classifier will train the visual recognition service, it will be able to recognize different images of the same person. Use at least ten images of your head shot and also create a negative data set by using headshots that are not your own.

4. A JSON file [UserInfo.json](ios_swift/ResumeARStarter/UserInfo.json) is used to store the information about the user. Its indexed by classification identifier. You need to have an entry in this file for any new user that you have classified in visual recognition service.

5. Go to `ios_swift` directory and open the project using `Xcode`.

6. Create a `ResumeARStarter/BMSCredentials.plist` in the project and replace the credentials. The `plist` file looks like below:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>visualrecognitionApi_key</key>
	<string>VR_API_KEY</string>
	<key>cloudantUrl</key>
	<string>CLOUDANT_URL</string>
</dict>
</plist>
```

7. At a command line, run `pod install` to install the [Watson SDK](https://github.com/watson-developer-cloud/swift-sdk#watson-developer-cloud-swift-sdk) and other dependencies.
![Pod Install Output](https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/pod-install-output.png)

8. Once the previous steps are complete go back to Xcode and run the application by clicking the `Build` and `Run` menu options.
![Xcode Build and Run](https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/build-and-run.png)

NOTE: The training in Watson Visual Recognition might take couple of minutes. If the status is in `training`, then the AR will show `Training in progress` in your AR view. You can check the status of your classifier by using following curl command:

```bash
curl "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classifiers?api_key={API_KEY}&verbose=true&version=2016-05-20"
```

Replace the `API_KEY` with the Watson Visual Recognition api key.

9. To test you can use the test images provided in [`TestImages`](https://github.com/IBM/pattern-utils/tree/master/arkit-starter/images/TestImages) folder.

# Sample Output

<img src="https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/sanjeev_sample_output.png" height=250px width=140px> | <img src="https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/steve_sample_output.png" height=250px width=140px> | <img src="https://raw.githubusercontent.com/IBM/pattern-utils/master/arkit-starter/images/scott_sample_output.png" height=250px width=140px> |

# Learn more

* **Artificial Intelligence Code Patterns**: Enjoyed this Code Pattern? Check out our other [AI Code Patterns](https://developer.ibm.com/technologies/artificial-intelligence/).
* **AI and Data Code Pattern Playlist**: Bookmark our [playlist](https://www.youtube.com/playlist?list=PLzUbsvIyrNfknNewObx5N7uGZ5FKH0Fde) with all of our Code Pattern videos
* **With Watson**: Want to take your Watson app to the next level? Looking to utilize Watson Brand assets? [Join the With Watson program](https://www.ibm.com/watson/with-watson/) to leverage exclusive brand, marketing, and tech resources to amplify and accelerate your Watson embedded commercial solution.
* **Offline image classification using Watson Visual Recognition and Core ML** [Visual Recognition Example](https://github.com/watson-developer-cloud/visual-recognition-coreml)

# Troubleshooting
* In order to start from scratch you need to delete the Watson Visual Recognition trained models, delete the data from the Cloudant database and delete the app to delete downloaded models.

# Links

* [ARKit](https://developer.apple.com/arkit)
* [Watson Swift SDK](https://github.com/watson-developer-cloud/swift-sdk)
* [IBM Visual Recognition](https://www.ibm.com/watson/services/visual-recognition)

# License

This code pattern is licensed under the Apache Software License, Version 2.  Separate third party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1 (DCO)](https://developercertificate.org/) and the [Apache Software License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache Software License (ASL) FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
