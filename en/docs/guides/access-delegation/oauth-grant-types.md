# Configuring OAuth Grant Types

This page guides you through using one of the [OAuth Grant Types](../../../../concepts/authorization/grant-types) to configure authentication for an OAuth/OpenID Connect web application. 

----

{!fragments/register-a-service-provider.md!}

3.  Expand **Inbound Authentication Configuration** section and then **OAuth/OpenID Connect Configuration**. 

4. Click **Configure.**   

5. Select the relevant grant types that you wish to try out from the **Allowed Grant Types** list.
        
6. Enter the **Callback Url**.

    !!! tip
        For more information on `Callback Url` and other advanced configurations, see [Advanced OpenID Connect Configurations](../../authentication/oauth-app-config-advanced).
        
7.  Click **Add**. 

    Note that the **OAuth Client Key** and **Client Secret** are generated. You will need these values later on when sending the request to the authorization endpoint.

8.  Click **Register**.

----

## Authorization code grant type

1. Send the following request using a browser-based application to obtain the authorization code. 

    !!! tip
        You can also use the WSO2 Identity Server Playground sample as the browser-based application to obtain the request. For instructions on using the Playground app, see [Authorization Code Grant with OAuth 2.0 Playground](../../../samples/auth-code-playground).

    ``` tab="Request Format"
    https://<host>:<port>/oauth2/authorize?
    response_type=code&
    client_id=<client_ID>&
    redirect_uri=<callback_url>&
    scope=<scope>
    ```

    ```tab="Sample Request"
    https://localhost:9443/oauth2/authorize?
    response_type=code&
    client_id=0rhQErXIX49svVYoXJGt0DWBuFca&
    redirect_uri=http://wso2is.local:8080/playground2/oauth2client&
    scope=openid
    ```

    You will receive an authorization code. 

    ```
    http://wso2is.local:8080/playground2/oauth2client?code=9142d4cad58c66d0a5edfad8952192
    ```

2. Run the following curl command using the authorization code recieved, to obtain the access token. 

    ``` tab="Request Format"
    curl -v -X POST --basic -u <client_ID>:<client_secret> -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=authorization_code&code=<authorization_code>&redirect_uri=<callback_url> <token_endpoint>
    ```

    ```tab="Sample Request"
    curl -v -X POST --basic -u 7wYeybBGCVfLxPmS0z66WNMffyMa:WYfwHUsbsEvwtqmDLuaxF_VCQJwa -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=authorization_code&code=a0996a17-4a34-3d99-bfcd-6bd1faa604d0&redirect_uri=http://wso2is.local:8080/playground2/oauth2client" https://localhost:9443/oauth2/token
    ```

3. You will receive the following response with the access token and refresh token. 

    ```
    {"access_token":"190c7f98-1451-310f-9c3c-f2e6de116261","refresh_token":"aeb15689-0fb4-377c-bcdb-161e25857927","scope":"default","token_type":"Bearer","expires_in":3600}
    ```

----

## Implicit grant type

Send the following request using a browser-based application to obtain the ID token. 

!!! tip
    You can also use the WSO2 Identity Server Playground sample as the browser-based application to obtain the request. For instructions on using the Playground app, see [Implicit Grant with OAuth 2.0 Playground](../../../samples/implicit-playground).

``` tab="Request Format"
https://<host>:<port>/oauth2/authorize?
response_type=token&
&client_id=<client-ID>
&redirect_uri=<callback-url>
&scope=<scope>
```

```tab="Sample Request"
https://localhost:9443/oauth2/authorize?
response_type=code&
client_id=0rhQErXIX49svVYoXJGt0DWBuFca&
redirect_uri=http://wso2is.local:8080/playground2/oauth2client&
scope=openid
```

You will receive the ID token. 

```
http://wso2is.local:8080/playground2/oauth2client#id_token=eyJ4NXQiOiJNell4TW1Ga09HWXdNV0kw&
expires_in=3600
```

----

## Resource owner / password credentials grant type

Send the following request using a browser-based application to obtain the access token. 

!!! tip
    You can also use the WSO2 Identity Server Playground sample as the browser-based application to obtain the request. For instructions on using the Playground app, see [Password Grant with OAuth 2.0 Playground](../../../samples/password-playground).

``` tab="Request Format"
curl -v -X POST --basic -u <client_ID>:<client_secret> -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=password&username=<username>&password=<password>" <token_endpoint>
```

```tab="Sample Request"
curl -v -X POST --basic -u 7wYeybBGCVfLxPmS0z66WNMffyMa:WYfwHUsbsEvwtqmDLuaxF_VCQJwa -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=password&username=admin&password=admin" https://localhost:9443/oauth2/token
```

You will receive the following response with the access token and refresh token. 

```
{"access_token":"16ab408c-0f31-3321-8bed-313e836df373","refresh_token":"3c285b4f-ec29-3751-9ced-74c92061b327","token_type":"Bearer","expires_in":3600}
```

----

## Client credentials grant type

Send the following request using a browser-based application to obtain the access token. 

!!! tip
    You can also use the WSO2 Identity Server Playground sample as the browser-based application to obtain the request. For instructions on using the Playground app, see [Client Credentials Grant with OAuth 2.0 Playground](../../../samples/client-credentials-playground).

``` tab="Request Format"
curl -v -X POST --basic -u <client_ID>:<client_secret>_VCQJwa -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=client_credentials" <token_endpoint>
```

```tab="Sample Request"
curl -v -X POST --basic -u 7wYeybBGCVfLxPmS0z66WNMffyMa:WYfwHUsbsEvwtqmDLuaxF_VCQJwa -H "Content-Type:application/x-www-form-urlencoded;charset=UTF-8" -k -d "grant_type=client_credentials" https://localhost:9443/oauth2/token
```

You will receive the following response with the access token.

```
{"access_token":"16ab408c-0f31-3321-8bed-313e836df373","token_type":"Bearer","expires_in":2986}
```

----

{!fragments/self-contained-access-tokens.md!}

----

{!fragments/oauth-transaction-logs.md!}


