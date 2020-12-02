---
layout: post
title: Error on firebase upgrade to 10 with cheking duplicate class.
gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

1. 현상 파이어 베이스 10버전 업그레이드 이후, 얼굴 인식관련 클래스에서 중복 클래스에러가 빌드시에 발생.
Task :app:checkReleaseDuplicateClasses FAILED

FAILURE: Build failed with an exception.

What went wrong: Execution failed for task ':app:checkReleaseDuplicateClasses'.
1 exception was raised by workers: java.lang.RuntimeException: java.lang.RuntimeException: Duplicate class com.google.android.gms.internal.vision.zzbl found in modules jetified-firebase-ml-vision-face-model-17.0.2-runtime.jar (com.google.firebase:firebase-ml-vision-face-model:17.0.2) and play-services-vision-common-19.1.0-runtime.jar (com.google.android.gms:play-services-vision-common:19.1.0) Duplicate class com.google.android.gms.internal.vision.zzbm found in modules jetified-firebase-ml-vision-face-model-17.0.2-runtime.jar (com.google.firebase:firebase-ml-vision-face-model:17.0.2) and play-services-vision-common-19.1.0-runtime.jar (com.google.android.gms:play-services-vision-common:19.1.0) Duplicate class com.google.android.gms.internal.vision.zzbn found in modules jetified-firebase-ml-vision-face-model-17.0.2-runtime.jar (com.google.firebase:firebase-ml-vision-face-model:17.0.2) and play-services-vision-common-19.1.0-runtime.jar (com.google.android.gms:play-services-vision-common:19.1.0) ...

2. 해결 android/app/build.gradle의 dependencies에 다음 내용 추가.

implementation (project(':react-native-camera')) { exclude group: "com.google.android.gms" exclude group: "com.google.android.gms", module: "play-services-vision" exclude group: "com.google.firebase", module: "firebase-ml-vision-face-model" }
