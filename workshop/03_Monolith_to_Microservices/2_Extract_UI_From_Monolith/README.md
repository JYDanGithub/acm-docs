# Extract the User Interface from the Monolith

In this lab ...

![tm-ui-v1](../assets/extract_ui.png)

## Step 1: Define a new Route to the Monolith

1. Create another route for TicketMonster monolith under the name `backend`.
    ```
    oc expose service ticket-monster-monolith --name=backend
    oc get routes
    ``` 

## Step 2: Decouple the UI from the Monolith

1. Switch to the `tm-ui-v1` directory.

1. (optional) Check configuration of Proxy and ReverseProxy in `tm-ui-v1/httpd.conf`:
    ```
    ProxyPass "/rest" "http://backend-xxx.xxx/rest"
    ProxyPassReverse "/rest" "http://backend-xxx.xxx/rest"
    ```
    
1. Deploy the UI
    ```
    oc new-app -e BACKENDURL=<yourbackendurl> --docker-image=dynatracesockshop/tm-ui-v1:latest
    oc expose service tm-ui-v1
    ```