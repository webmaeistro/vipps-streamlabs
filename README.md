# Vipps for Streamlabs

A quick hack from an internal Vipps hackathon. No guarantees whatsoever.

This is a
[Spring Boot](https://spring.io/projects/spring-boot)
Java application which integrates with the
[Vipps eCom v2 API](https://github.com/vippsas/vipps-ecom-api)
and
[Streamlabs API](https://dev.streamlabs.com/reference).

This was useful for us:
* [Getting started with Spring Boot](https://spring.io/guides/gs/spring-boot/).
* [Validating Form Input](https://spring.io/guides/gs/validating-form-input/).

## Vipps API

* Get Accesstoken: [`POST:/accesstoken/get`](https://vippsas.github.io/vipps-ecom-api/#/Authorization%20Service/fetchAuthorizationTokenUsingPost)
* Initiate Payment: [`POST:/ecomm/v2/payments`](https://vippsas.github.io/vipps-ecom-api/#/Vipps%20eCom%20API/initiatePaymentV3UsingPOST)
* Listen for callback on a successful, or unsuccesful, payment in the Vipps app ([`POST:[callbackPrefix]/v2/payments/{orderId}`](https://vippsas.github.io/vipps-ecom-api/#/Endpoints%20required%20by%20Vipps%20from%20the%20merchant/transactionUpdateCallbackForRegularPaymentUsingPOST)).

**Please note**: [Refunds](https://vippsas.github.io/vipps-ecom-api/#/Vipps%20eCom%20API/refundPaymentUsingPOST),
[Get Payment Details](https://vippsas.github.io/vipps-ecom-api/#/Vipps%20eCom%20API/getPaymentDetailsUsingGET)
and more is not implemented.
This is just _bare minimum_ implementation for the hackathon.
We make the code available here, in case it may be useful for others.
[Issues](issues) and [PRs](pulls) are welcome!

## Streamlabs API

* If a callback from Vipps API was successful, it triggered a POST request to
the Streamlabs [`POST:/donations`](https://dev.streamlabs.com/reference#donations-1)
endpoint. The streamer then has to configure in the admin panel how the donation will be
shown in the stream.

In the StreamlabService class there is a _hardcoded_ accesstoken passed from
`application.properties`. Streamlabs informed us that this had no expiry date,
so we got the access token when testing in [Postman](https://www.getpostman.com)
and copied into the properties file.