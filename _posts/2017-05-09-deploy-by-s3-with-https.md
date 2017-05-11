---
layout: post
comments: true
author: Harrison Jung
title: "AWS Cloudfront 도메인 연결하기"
description: "AWS Cloudfront에 HTTPS적용되는 도메인 연결하기"
category: tip
date: 2017-04-26 11:45:00
tags: [aws,cloudfront,domain,https,s3]
ogimage: "/assets/post/cloud/20170509_Amazon-Cloudfront.png"
---

꿈많은청년들은 지난번에 FBStart를 통해서 무려 $5000 라는 AWS 크레딧을 받았습니다. 그런데, 저희는 GCP 파트너사이기도 하고, 현재 주로 GCP를 쓰다보니 AWS를 쓸일이 없었습니다.

그러나, 크레딧을 그냥 날리기는 아깝고 해서 생각해 낸 방법이 그냥 S3를 활용하여 트래픽을 전부 AWS에서 처리하고, GCP에서는 나머지 기능을 사용하자! 라는 결론을 내렸습니다.

원래 저희는 GCP를 쓰기도 했고 그러다 보니 AWS가 익숙치 않아서, 삽질을 한 내용들을 올리게 되었습니다.

## 1. S3 Bucket 만들기

- [ https://console.aws.amazon.com/s3 ]
- 적당한 이름으로 S3 Bucket을 생성합니다. 도메인이름을 이용하면 나중에 기억하기도 좋고, 생성하기도 쉽습니다.
    - 예를들면 cdn.example.com 의 형태로 만드는 것도 괜찮습니다.
- 생성한 Bucket에 외부에서 접속이 가능하도록 몇가지 설정
    - [ Permissions ] > [ Bucket Policy ] 에서 전체 접속이 가능하도록, 하단에서 [ Policy generator ]를 선택.
    - [ Select Type of Policy ] > S3 Bucket Policy
    - [ Principal ] > *
    - [ Action ] > GetObject
    - [ Amazon Resource Name (ARN) ] > arn:aws:s3:::<bucket_name>/*
        - ( bucket_name 에는 만든 버켓의 이름을 입력합니다. )
    - 생성!
        - 생성된 값을 입력

## 2. CloudFront

- 콘솔에 접속 [  https://console.aws.amazon.com/cloudfront/ ]
- [ Create Distribution ]를 클릭하여 새로 생성하기
- [ Web ] > Get Started
- [ Origin Domain Name ]를 누르시면 목록이 나오는데, 앞에서 생성한 버켓을 선택합니다.
- 만약에 HTTPS를 이용하려면 구입한 인증서를 업로드 하거나 혹은 생성 버튼을 클릭하여 업로드 하실 수 있습니다.
- [ Viewer Protocol Policy ] > Redirect HTTP to HTTPS 를 추천합니다.
- [ Alternate Domain Names (CNAMEs) ]에는 이제 사용할 도메인 이름을 넣습니다. 물론, 서브 도메인도 가능합니다.
- 생성하고 나면 목록에서 [ abcdefg.cloudfront.net ]과 같은 이름의 Domain Name 이 생성됩니다. 이걸 잠시후에 사용합니다.
- [ Status ]가 [ In Progress ]상태가 됩니다. 전체 엣지 로케이션으로 배포되는데 시간이 꽤 걸립니다. 기다리세요.

## 3. DNS 설정

- 앞에서 사용했던 서브 도메인의 이름을 이곳에 입력합니다. 예를 들면 cdn.example.com 이라면 cdn 이라는 이름으로 CNAME을 생성합니다.
- CNAME 에는 [ abcdefg.cloudfront.net ]를 입력합니다.
- 이제 기다립니다.

대충 이정도로 하면 HTTPS가 적용된 자체 도메인으로 서비스가 가능한데, 대신에 S3 로 직접 서비스하는것에 비해 네트워크 비용이 더 비쌉니다.
https://cdn.example.com/filename.png 와 <br>
https://s3.ap-northeast-2.amazonaws.com/cdn.example.com/filename.png 의 차이라고 생각하시면 될듯 합니다.<br>
( 물론 버켓 이름을 짧게 쓸순 있을겁니다. )
