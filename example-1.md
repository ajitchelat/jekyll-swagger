---
layout: swagger
title: Example 1
---
swagger: "2.0"
info:
  version: "1.0.0"
  title: ""
basePath: "/xenmobile/api/v1"
tags:
- name: "Device Filter"
- name: "Mobile Application"
- name: "Web & SaaS Application"
- name: "ShareFile Connector Filter"
- name: "Groups"
- name: "Web Link Applications"
- name: "Ldap"
- name: "Delivery Groups Filter"
- name: "Public Store Application"
- name: "Application Filter"
- name: "ShareFile Connector"
- name: "Netscaler Gateway"
- name: "Device"
- name: "Enrollment"
- name: "Authentication"
- name: "Client Properties"
- name: "Client Branding"
- name: "ShareFile Enterprise"
- name: "Application"
- name: "Enrollment Filter"
- name: "Role Based Access Control"
- name: "Local Users Groups"
- name: "Users"
- name: "Server Properties"
- name: "Delivery Groups"
- name: "ShareFile Connector Storage Zones"
- name: "Notification Server"
schemes:
- "http"
paths:
  /application:
    delete:
      tags:
      - "Application"
      summary: "Delete multiple applications by a list of container ids"
      description: ""
      operationId: "deleteApplications"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "containerIds"
        description: "List of container ids"
        required: true
        schema:
          type: "array"
          items:
            type: "integer"
            format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/filter:
    post:
      tags:
      - "Application Filter"
      summary: "Get the list of filtered applications"
      description: ""
      operationId: "applyFiltersAndGetAppsTree"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/AppsFilterDataModel"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GetAppResponseData"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/mobile/{containerid}:
    get:
      tags:
      - "Mobile Application"
      summary: "Returns mobile application by container id"
      description: ""
      operationId: "getMobileApplication"
      produces:
      - "application/json"
      parameters:
      - name: "containerid"
        in: "path"
        description: "Container id of mobile application"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/MobileAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/mobile/{type}/{platform}:
    post:
      tags:
      - "Mobile Application"
      summary: "Upload mobile application"
      description: ""
      operationId: "uploadMobileApp"
      consumes:
      - "multipart/form-data"
      produces:
      - "application/json"
      parameters:
      - name: "platform"
        in: "path"
        description: "Platform of application, possible values are \"google\", \"\
          android_work\", \"iphone\", \"ipad\", \"amazon\", \"windows\", \"windows_phone\""
        required: true
        type: "string"
      - name: "type"
        in: "path"
        description: "Application type, possible values are \"mdx\" or \"enterprise\""
        required: true
        type: "string"
        default: "mdx"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      - name: "uploadFile"
        in: "formData"
        description: "uploaded file"
        required: true
        type: "file"
      - name: "appInfo"
        in: "formData"
        description: "importData text"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/MobileAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/mobile/{type}/{platform}/{containerId}:
    post:
      tags:
      - "Mobile Application"
      summary: "Add platform data to application container"
      description: ""
      operationId: "addPlatformToExistingContainer"
      consumes:
      - "multipart/form-data"
      produces:
      - "application/json"
      parameters:
      - name: "platform"
        in: "path"
        required: true
        type: "string"
      - name: "containerId"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "type"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      - name: "uploadFile"
        in: "formData"
        description: "uploaded file"
        required: true
        type: "file"
      - name: "appInfo"
        in: "formData"
        description: "importData text"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/MobileAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Mobile Application"
      summary: "Update platform data in application container"
      description: ""
      operationId: "editPlatformInfoInContainer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "platform"
        in: "path"
        description: "Platform of application, possible values are \"google\", \"\
          android_work\", \"iphone\", \"ipad\", \"amazon\", \"windows\", \"windows_phone\""
        required: true
        type: "string"
        default: "iphone"
      - name: "containerId"
        in: "path"
        description: "Application container id"
        required: true
        type: "integer"
        format: "int32"
      - name: "type"
        in: "path"
        description: "Application type, possible values are \"mdx\" or \"enterprise\""
        required: true
        type: "string"
        default: "mdx"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/MobileAppPlatformData"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/MobileAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/saas:
    post:
      tags:
      - "Web & SaaS Application"
      summary: "Add web/saas application"
      description: ""
      operationId: "addWebSaasApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/WebSaasAppData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/saas/connector:
    get:
      tags:
      - "Web & SaaS Application"
      summary: "Get all Web and SaaS connectors"
      description: ""
      operationId: "getWebSaasConnectors"
      produces:
      - "application/json"
      parameters: []
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ConnectorsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/saas/connector/{connectorName}:
    get:
      tags:
      - "Web & SaaS Application"
      summary: "Get Web and SaaS connector by connector name"
      description: ""
      operationId: "getWebSaasConnector"
      produces:
      - "application/json"
      parameters:
      - name: "connectorName"
        in: "path"
        description: "connector name of Web and SaaS connector"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ConnectorResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/saas/{containerId}:
    get:
      tags:
      - "Web & SaaS Application"
      summary: "Get Web and SaaS application by container id"
      description: ""
      operationId: "getWebSaasApplication"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "Container id of Web and SaaS application"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Web & SaaS Application"
      summary: "Update web/saas application"
      description: ""
      operationId: "updateWebSaasApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "container id of Web and SaaS application"
        required: true
        type: "integer"
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/WebSaasAppData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/store:
    post:
      tags:
      - "Public Store Application"
      summary: "Add app store application container"
      description: ""
      operationId: "addPublicStoreApplicationContainer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/PublicStoreAppContainerRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/store/{containerId}:
    get:
      tags:
      - "Public Store Application"
      summary: "Get app store application by container id"
      description: ""
      operationId: "getPublicStoreApplicationContainer"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "Container id of app store application"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Public Store Application"
      summary: "Update app store application by container id"
      description: ""
      operationId: "updatePublicStoreApplicationContainer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "Container id of app store application"
        required: true
        type: "integer"
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/PublicStoreAppContainerRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/store/{containerId}/platform/{platform}:
    post:
      tags:
      - "Public Store Application"
      summary: "Add app store application in existing container"
      description: ""
      operationId: "addPublicStoreApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "platform"
        in: "path"
        description: "Platform of application, possible values are \"android\", \"\
          android_work\", \"iphone\", \"ipad\", \"windows\", \"windows_phone\""
        required: true
        type: "string"
        enum:
        - "iphone"
        - "ipad"
        - "android"
        - "android_work"
        - "windows"
        - "windows_phone"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/PublicStoreAppData"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Public Store Application"
      summary: "Update app store application platform data"
      description: ""
      operationId: "updatePublicStoreApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "platform"
        in: "path"
        description: "Platform of application, possible values are \"android\", \"\
          android_work\", \"iphone\", \"ipad\", \"windows\", \"windows_phone\""
        required: true
        type: "string"
        enum:
        - "iphone"
        - "ipad"
        - "android"
        - "android_work"
        - "windows"
        - "windows_phone"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/PublicStoreAppData"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Public Store Application"
      summary: "Delete app store application from a container"
      description: ""
      operationId: "deletePublicStoreApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "platform"
        in: "path"
        description: "Platform of application, possible values are \"android\", \"\
          android_work\", \"iphone\", \"ipad\", \"windows\", \"windows_phone\""
        required: true
        type: "string"
        enum:
        - "iphone"
        - "ipad"
        - "android"
        - "android_work"
        - "windows"
        - "windows_phone"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/PublicStoreAppContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/weblink:
    post:
      tags:
      - "Web Link Applications"
      summary: "Add weblink application"
      description: ""
      operationId: "addWebLinkApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/WebAppData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/weblink/{containerId}:
    get:
      tags:
      - "Web Link Applications"
      summary: "Get web link application by container Id"
      description: ""
      operationId: "getWebLinkApplication"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "Container id of web link application"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Web Link Applications"
      summary: "Update weblink application"
      description: ""
      operationId: "updateWebLinkApplication"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/WebAppData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/WebApplicationContainerResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /application/{containerId}:
    delete:
      tags:
      - "Application"
      summary: "Delete application by container id"
      description: ""
      operationId: "deleteApplication"
      produces:
      - "application/json"
      parameters:
      - name: "containerId"
        in: "path"
        description: "Id of container"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /authentication/cwclogin:
    post:
      tags:
      - "Authentication"
      summary: "CWC Login"
      description: "Operation for logging in to access public REST API through CWC"
      operationId: "cwcLogin"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "Authorization"
        in: "header"
        required: false
        type: "string"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/CwcLoginData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LoginResponse"
        400:
          description: "Bad Request : Request is missing parameters or json is invalid"
        403:
          description: "Forbidden : You may not have priveleges to invoke this service"
        500:
          description: "Internal Server Error : An error occured on the server side"
  /authentication/login:
    post:
      tags:
      - "Authentication"
      summary: "Login"
      description: "Operation for logging in to access public REST API"
      operationId: "login"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LoginData"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LoginResponse"
        400:
          description: "Bad Request : Request is missing parameters or json is invalid"
        403:
          description: "Forbidden : You may not have priveleges to invoke this service"
        500:
          description: "Internal Server Error : An error occured on the server side"
  /authentication/logout:
    post:
      tags:
      - "Authentication"
      summary: "Logout"
      description: "Operation for logging out of public REST API"
      operationId: "logout"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LogoutData"
      responses:
        400:
          description: "Bad Request : Request is missing parameters or json is invalid"
        403:
          description: "Forbidden : You may not have priveleges to invoke this service"
        500:
          description: "Internal Server Error : An error occured on the server side"
  /clientbranding/{identifier}:
    put:
      tags:
      - "Client Branding"
      summary: "Set a new client brand"
      description: "Uploads a new client logo as a client brand"
      operationId: "addClientBranding"
      consumes:
      - "multipart/form-data"
      produces:
      - "application/json"
      parameters:
      - name: "identifier"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      - name: "uploadFile"
        in: "formData"
        description: "uploaded branding file"
        required: true
        type: "file"
      - name: "device"
        in: "formData"
        description: "device data"
        required: true
        type: "string"
        enum:
        - "phone"
        - "tablet"
      - name: "worxStoreView"
        in: "formData"
        description: "worxStoreView data"
        required: true
        type: "string"
        enum:
        - "default"
        - "category"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientBrandingResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    delete:
      tags:
      - "Client Branding"
      summary: "Delete client brand"
      description: "Deletes client brand for the given device"
      operationId: "deleteClientBranding"
      produces:
      - "application/json"
      parameters:
      - name: "identifier"
        in: "path"
        required: true
        type: "string"
        enum:
        - "phone"
        - "tablet"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientBrandingResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /clientproperties:
    get:
      tags:
      - "Client Properties"
      summary: "Get client properties"
      description: "Get client properties"
      operationId: "getClientProperties"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesGetResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    post:
      tags:
      - "Client Properties"
      summary: "Add new client property"
      description: "Add new client property"
      operationId: "addClientProperties"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ClientPropertiesAddRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    delete:
      tags:
      - "Client Properties"
      summary: "Delete client properties"
      description: "Delete client properties"
      operationId: "deleteClientProperties"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /clientproperties/{key}:
    get:
      tags:
      - "Client Properties"
      summary: "Get client property by key"
      description: "Get client property by key"
      operationId: "getClientProperty"
      produces:
      - "application/json"
      parameters:
      - name: "key"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesGetResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    put:
      tags:
      - "Client Properties"
      summary: "Update the client property"
      description: "Update the client property"
      operationId: "updateClientProperty"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ClientPropertiesRequest"
      - name: "key"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesGetResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    delete:
      tags:
      - "Client Properties"
      summary: "Delete client property"
      description: "Delete client property"
      operationId: "deleteClientProperty"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "key"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ClientPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /deliverygroups:
    get:
      tags:
      - "Delivery Groups"
      summary: "Get all delivery groups"
      description: "Get all delivery groups"
      operationId: "getRoles"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/BaseResponseModel"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    post:
      tags:
      - "Delivery Groups"
      summary: "Add delivery group"
      description: "Add delivery group"
      operationId: "addRole"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeliveryGroupRequestDataModel"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Delivery Groups"
      summary: "Update delivery group"
      description: "Update delivery group"
      operationId: "updateRole"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeliveryGroupUpdateRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Delivery Groups"
      summary: "Delete delivery group"
      description: "Delete delivery group"
      operationId: "deleteRoles"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "Ids"
        description: "List of delivery group ids or names"
        required: true
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleNamesResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /deliverygroups/deploy:
    post:
      tags:
      - "Delivery Groups"
      summary: "Deploy delivery groups by name or Id"
      description: "Deploy delivery groups by name or Id"
      operationId: "deploy"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeliveryGroupDeployRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/BaseResponseModel"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /deliverygroups/filter:
    post:
      tags:
      - "Delivery Groups Filter"
      summary: "Get list of delivery groups based on provided filter criteria"
      description: "Get list of delivery groups based on provided filter criteria"
      operationId: "applyFiltersAndGetRoleTree"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeliveryGroupsFilterDataModel"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GetDgResponseDataModel"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /deliverygroups/getdeploymentstatus/{Id}:
    get:
      tags:
      - "Delivery Groups"
      summary: "Get deployment status of delivery group by delivery group name or\
        \ Id"
      description: "Get deployment status of delivery group by delivery group name\
        \ or Id"
      operationId: "getRoleStatus"
      produces:
      - "application/json"
      parameters:
      - name: "Id"
        in: "path"
        description: "Delivery group id or name"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleDeployStatusResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /deliverygroups/{Id}:
    get:
      tags:
      - "Delivery Groups"
      summary: "Get delivery group by name or Id"
      description: "Get delivery group by its name or Id"
      operationId: "getRole"
      produces:
      - "application/json"
      parameters:
      - name: "Id"
        in: "path"
        description: "Delivery group Id or name"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /deliverygroups/{Id}/{enabled}:
    put:
      tags:
      - "Delivery Groups"
      summary: "Enable/Disable delivery group by name or Id"
      description: "Enable/Disable delivery group by name or Id"
      operationId: "enableRole"
      produces:
      - "application/json"
      parameters:
      - name: "Id"
        in: "path"
        description: "Delivery group Id or name"
        required: true
        type: "string"
      - name: "enabled"
        in: "path"
        description: "enable/disable"
        required: true
        type: "string"
        pattern: "enable|disable"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleNameResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device:
    delete:
      tags:
      - "Device"
      summary: "Delete devices in bulk"
      description: "Delete devices in bulk"
      operationId: "deleteDevices"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "List of numerical id of the device"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
  /device/activationLockBypass:
    post:
      tags:
      - "Device"
      summary: "Activation lock bypass a list of devices based on Device ID"
      description: "Activation lock bypass a list of devices based on Device ID of\
        \ the devices"
      operationId: "activationLockBypassDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/appLock:
    post:
      tags:
      - "Device"
      summary: "App Lock a list of devices based on Device ID"
      description: "App Lock a list of devices based on Device ID of the devices"
      operationId: "appLockDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/appWipe:
    post:
      tags:
      - "Device"
      summary: "App wipe a list of devices based on Device ID"
      description: "App wipe a list of devices based on Device ID of the devices"
      operationId: "appWipeDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/authorize:
    post:
      tags:
      - "Device"
      summary: "Authorize a list of devices to connect to server based on Device ID"
      description: "Authorize a list of devices to connect to server based on Device\
        \ ID of the devices"
      operationId: "authorizeDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerLock:
    post:
      tags:
      - "Device"
      summary: "Lock container of a list of devices based on Device ID"
      description: "Lock container of a list of devices based on Device ID of the\
        \ devices"
      operationId: "containerLockDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerLock/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the container lock of a list of devices based on Device ID"
      description: "Cancel the container lock of a list of devices based on Device\
        \ ID of the devices"
      operationId: "wsCancelDevicesContainerLock"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerPwdReset:
    post:
      tags:
      - "Device"
      summary: "Reset the container password of a list of devices based on Device\
        \ ID"
      description: "Reset the container password of a list of devices based on Device\
        \ ID of the devices"
      operationId: "containerPasswordResetDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerPwdReset/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the container password reset of a list of devices based on\
        \ Device ID"
      description: "Cancel the container password reset of a list of devices based\
        \ on Device ID of the devices"
      operationId: "cancelDevicesContainerPasswordReset"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerUnlock:
    post:
      tags:
      - "Device"
      summary: "Unlock the container of a list of devices based on Device ID"
      description: "Unlock the container of a list of devices based on Device ID of\
        \ the devices"
      operationId: "containerUnlockDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/containerUnlock/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the container unlock of a list of devices based on Device ID"
      description: "Cancel the container unlock of a list of devices based on Device\
        \ ID of the devices"
      operationId: "cancelDevicesContainerUnlock"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/depActivationLock:
    post:
      tags:
      - "Device"
      summary: "Enable the activation lock for a list of DEP devices based on Device\
        \ ID"
      description: "Enable the activation lock for a list of DEP devices based on\
        \ Device ID"
      operationId: "depActivationLockDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/disableLostMode:
    post:
      tags:
      - "Device"
      summary: "Disable the lost mode for a list of devices based on Device ID."
      description: "Disable the lost mode for a list of devices based on Device ID."
      operationId: "disableLostMode"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/disableLostMode/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the disable lost mode for a list of devices based on Device\
        \ ID."
      description: "Cancel the disable lost mode for a list of devices based on Device\
        \ ID."
      operationId: "cancelDisableLostMode"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/enableLostMode:
    post:
      tags:
      - "Device"
      summary: "Enable the lost mode for a list of devices based on Device ID."
      description: "Enable the lost mode for a list of devices based on Device ID."
      operationId: "enableLostMode"
      produces:
      - "application/json"
      parameters:
      - name: "message"
        in: "query"
        description: "message"
        required: false
        type: "string"
      - name: "phoneNumber"
        in: "query"
        description: "phoneNumber"
        required: false
        type: "string"
      - name: "footnote"
        in: "query"
        description: "footnote"
        required: false
        type: "string"
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/enableLostMode/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the enable lost mode for a list of devices based on Device\
        \ ID."
      description: "Cancel the enable lost mode for a list of devices based on Device\
        \ ID."
      operationId: "cancelEnableLostMode"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/filter:
    post:
      tags:
      - "Device Filter"
      summary: "Get Devices based on Filters"
      description: "Get devices based on filter criteria"
      operationId: "getDevicesByFilter"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeviceFilterRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceFilterResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/knownProperties:
    get:
      tags:
      - "Device"
      summary: "Get All devices known properties (name, group and value type)"
      description: "Get All devices known properties (name, group and value type)"
      operationId: "getKnownProperties"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceKnownPropertiesResponse"
        400:
          description: "Bad Request"
  /device/lastLocation/{deviceId}:
    get:
      tags:
      - "Device"
      summary: "Retrieve the last known GPS ccordinates of the device"
      description: "Retrieve the last known GPS ccordinates of the device based on\
        \ device id"
      operationId: "lastDeviceGPSLocation"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceCoordinateResponse"
        400:
          description: "Bad Request"
  /device/locate:
    post:
      tags:
      - "Device"
      summary: "Locate a list of devices based on Device ID"
      description: "Locate a list of devices based on Device ID of the devices"
      operationId: "locateDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/locate/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the locating of a list of devices based on Device ID"
      description: "Cancel the locating of a list of devices based on Device ID of\
        \ the devices"
      operationId: "cancelDevicesLocate"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/locations/{deviceId}:
    get:
      tags:
      - "Device"
      summary: "Retrieve GPS ccordinates of the device"
      description: "Retrieve GPS ccordinates of the device based on device id"
      operationId: "filterDeviceGPSLocation"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "startDate"
        in: "query"
        description: "start date for coordinates filter"
        required: false
        type: "integer"
        format: "int64"
        x-example: 1479975747000
      - name: "endDate"
        in: "query"
        description: "end date for coordinates filter"
        required: false
        type: "integer"
        format: "int64"
        x-example: 1479975749000
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceCoordinatesResponse"
        400:
          description: "Bad Request"
  /device/lock:
    post:
      tags:
      - "Device"
      summary: "Lock a list of devices based on Device ID"
      description: "Lock a list of devices based on Device ID of the devices"
      operationId: "lockDevices"
      produces:
      - "application/json"
      parameters:
      - name: "newPinCode"
        in: "query"
        description: "new pin code"
        required: false
        type: "string"
      - name: "resetPinCode"
        in: "query"
        description: "add a reset pin code request to the lock request, works only\
          \ for Windows phone 8.1"
        required: false
        type: "boolean"
        default: false
      - name: "lockMessage"
        in: "query"
        description: "add a message to the lock request, works only for IOS 7 and\
          \ later"
        required: false
        type: "string"
      - name: "phoneNumber"
        in: "query"
        description: "add a phone number to the lock request, works only for IOS 7\
          \ and later"
        required: false
        type: "string"
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/lock/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the lock of a list of devices based on Device ID"
      description: "Cancel the lock of a list of devices based on Device ID of the\
        \ devices"
      operationId: "cancelDevicesLock"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/mdmstatus/{deviceId}:
    get:
      tags:
      - "Device"
      summary: "Retrieve iOS MDM status for a given device"
      description: "Retrieve iOS MDM status for a given device based on device id"
      operationId: "getMdmStatus"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceMdmStatusResponse"
        400:
          description: "Bad Request"
  /device/notify:
    post:
      tags:
      - "Device"
      summary: "Send notifications to Devices"
      description: "Send notifications to devices"
      operationId: "sendNotification"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DeviceNotifyRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceNotifyResponse"
        400:
          description: "Bad Request"
  /device/pincode/generate:
    get:
      tags:
      - "Device"
      summary: "Generate a new pin code"
      description: "Generate a new pin code"
      operationId: "generatePinCode"
      produces:
      - "application/json"
      parameters:
      - name: "PinCodeLength"
        in: "query"
        description: "Length of the requested pin code"
        required: true
        type: "integer"
        default: 4
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GeneratePinCodeResponse"
        400:
          description: "Bad Request"
  /device/properties/{deviceId}:
    get:
      tags:
      - "Device"
      summary: "Retrieve device properties for a given device based on device ID"
      description: "Retrieve device properties for a given device based on device\
        \ ID"
      operationId: "getDeviceProperties"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DevicePropertiesResponse"
        400:
          description: "Bad Request"
    put:
      tags:
      - "Device"
      summary: "Save device properties for a given device based on device ID"
      description: "Save device properties for a given device based on device ID"
      operationId: "saveDeviceProperties"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DevicePropertiesRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DevicePropertyResponse"
        400:
          description: "Bad Request"
  /device/property/{id}:
    post:
      tags:
      - "Device"
      summary: "Add or update a device property to device based on property id"
      description: "Add or update a device property to device based on property id"
      operationId: "addOrUpdateDeviceProperty"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/DevicePropertyRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DevicePropertyResponse"
        400:
          description: "Bad Request"
    delete:
      tags:
      - "Device"
      summary: "Delete a device property based on property id"
      description: "Delete a device property based on property id"
      operationId: "deleteDeviceProperty"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        description: "Numerical id of the property"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
  /device/refresh:
    post:
      tags:
      - "Device"
      summary: "Enforce devices to connect to server and refresh their statuses based\
        \ on Device ID"
      description: "Enforce devices to connect to server and refresh their statuses\
        \ based on Device ID of the devices"
      operationId: "refreshDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/requestMirroring:
    post:
      tags:
      - "Device"
      summary: "Request an AirPlay mirroring for a list of devices based on Device\
        \ ID"
      description: "Request an AirPlay mirroring for a list of devices based on Device\
        \ ID of the devices"
      operationId: "requestMirroring"
      produces:
      - "application/json"
      parameters:
      - name: "destinationName"
        in: "query"
        description: "destination name, Pass either destination name or destination\
          \ device id"
        required: false
        type: "string"
      - name: "destinationDeviceId"
        in: "query"
        description: "destination device id, Pass either destination name or destination\
          \ device id"
        required: false
        type: "string"
      - name: "scanTime"
        in: "query"
        description: "scan time"
        required: true
        type: "string"
      - name: "screenSharingPassword"
        in: "query"
        description: "password for screen sharing"
        required: false
        type: "string"
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/requestMirroring/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel a request AirPlay mirroring for a list of devices based on\
        \ Device ID"
      description: "Cancel a request AirPlay mirroring for a list of devices based\
        \ on Device ID of the devices"
      operationId: "cancelRequestMirroring"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/restart:
    post:
      tags:
      - "Device"
      summary: "Restart a list of devices based on Device ID"
      description: "Restart a list of devices based on Device ID of the devices"
      operationId: "restartDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/restart/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the restart of a list of devices based on Device ID"
      description: "Cancel the restart of a list of devices based on Device ID of\
        \ the devices"
      operationId: "cancelDevicesRestart"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/restrictions/clear:
    post:
      tags:
      - "Device"
      summary: "Clear the restrictions of a list of devices based on Device ID"
      description: "Clear the restrictions of a list of devices based on Device ID\
        \ of the devices"
      operationId: "clearDevicesRestrictions"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/restrictions/clear/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the clear restrictions of a list of devices based on Device\
        \ ID"
      description: "Cancel the clear restrictions of a list of devices based on Device\
        \ ID of the devices"
      operationId: "cancelClearDevicesRestrictions"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/revoke:
    post:
      tags:
      - "Device"
      summary: "Revoke a list of devices to forbid them to connect to server based\
        \ on Device ID"
      description: "Revoke a list of devices to forbid them to connect to server based\
        \ on Device ID of the devices"
      operationId: "revokeDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/ring:
    post:
      tags:
      - "Device"
      summary: "Make ring a list of devices based on Device ID"
      description: "Make ring a list of devices based on Device ID of the devices"
      operationId: "ringDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/ring/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel ring a list of devices based on Device ID"
      description: "Cancel ring a list of devices based on Device ID of the devices"
      operationId: "cancelDevicesRing"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/sdcardwipe:
    post:
      tags:
      - "Device"
      summary: "SDCard wipe a list of devices based on Device ID"
      description: "SDCard wipe a list of devices based on Device ID of the devices"
      operationId: "sdCardWipeDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/sdcardwipe/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the SDCard wipe of a list of devices based on Device ID"
      description: "Cancel the SDCard wipe of a list of devices based on Device ID\
        \ of the devices"
      operationId: "cancelDevicesSdCardWipe"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/selwipe:
    post:
      tags:
      - "Device"
      summary: "Selective wipe a list of devices based on Device ID"
      description: "Selective wipe a list of devices based on Device ID of the devices"
      operationId: "selectiveWipeDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/selwipe/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the selective wipe of a list of devices based on Device ID"
      description: "Cancel the selective wipe of a list of devices based on Device\
        \ ID of the devices"
      operationId: "cancelDevicesSelectiveWipe"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/shutdown:
    post:
      tags:
      - "Device"
      summary: "ShutDown a list of devices based on Device ID"
      description: "ShutDown a list of devices based on Device ID of the devices"
      operationId: "shutdownDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/shutdown/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the shutdown of a list of devices based on Device ID"
      description: "Cancel the shutdown of a list of devices based on Device ID of\
        \ the devices"
      operationId: "cancelDevicesShutdown"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/stopMirroring:
    post:
      tags:
      - "Device"
      summary: "Stop an AirPlay mirroring for a list of devices based on Device ID"
      description: "Stop an AirPlay mirroring for a list of devices based on Device\
        \ ID of the devices"
      operationId: "stopMirroring"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/stopMirroring/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel a stop AirPlay mirroring for a list of devices based on Device\
        \ ID"
      description: "Cancel a stop AirPlay mirroring for a list of devices based on\
        \ Device ID of the devices"
      operationId: "cancelStopMirroring"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/track:
    post:
      tags:
      - "Device"
      summary: "GPS tracking a list of devices based on Device ID"
      description: "GPS tracking a list of devices based on Device ID of the devices"
      operationId: "gpsTrackDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/track/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the GPS tracking of a list of devices based on Device ID"
      description: "Cancel the GPS tracking of a list of devices based on Device ID\
        \ of the devices"
      operationId: "cancelDevicesGPSTracking"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/unlock:
    post:
      tags:
      - "Device"
      summary: "Unlock a list of devices based on Device ID"
      description: "Unlock a list of devices based on Device ID of the devices"
      operationId: "unlockDevices"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/unlock/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the unlock of a list of devices based on Device ID"
      description: "Cancel the unlock of a list of devices based on Device ID of the\
        \ devices"
      operationId: "cancelDevicesUnlock"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/usedProperties:
    get:
      tags:
      - "Device"
      summary: "Retrieve all used properties"
      description: "Retrieve all used properties"
      operationId: "getUsedProperties"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceUsedPropertiesResponse"
        400:
          description: "Bad Request"
  /device/wipe:
    post:
      tags:
      - "Device"
      summary: "Wipe a list of devices based on Device ID"
      description: "Wipe a list of devices based on Device ID of the devices"
      operationId: "wipeDevices"
      produces:
      - "application/json"
      parameters:
      - name: "eraseMemoryCard"
        in: "query"
        description: "force erase memory card"
        required: false
        type: "boolean"
        default: true
      - name: "pinCode"
        in: "query"
        description: "pin code, works only for mac devices"
        required: true
        type: "string"
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/wipe/cancel:
    post:
      tags:
      - "Device"
      summary: "Cancel the wipe of a list of devices based on Device ID"
      description: "Cancel the wipe of a list of devices based on Device ID of the\
        \ devices"
      operationId: "cancelDevicesWipe"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "deviceIds"
        description: "list of database device IDs in json format, request body, sample\
          \ value [1,2]"
        required: true
        schema:
          type: "string"
          default: "[]"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionResponse"
        400:
          description: "Bad Request"
  /device/{deviceId}:
    get:
      tags:
      - "Device"
      summary: "Get device information based on ID"
      description: "Get device information based on the ID of the device"
      operationId: "getDevice"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Device"
      summary: "Delete a device"
      description: "Delete a device"
      operationId: "deleteDevice"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
  /device/{deviceId}/actions:
    get:
      tags:
      - "Device"
      summary: "Get actions for the device , based on device ID"
      description: "Get actions for the device , based on device ID"
      operationId: "getDeviceActions"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceActionsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/{deviceId}/apps:
    get:
      tags:
      - "Device"
      summary: "Get applications for the device , based on device ID"
      description: "Get applications for the device , based on device ID"
      operationId: "getDeviceApps"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceAppsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/{deviceId}/deliverygroups:
    get:
      tags:
      - "Device"
      summary: "Get delivery groups for the device , based on device ID"
      description: "Get delivery groups for the device , based on device ID"
      operationId: "getDeviceDeliveryGroups"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceDeliveryGroupsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/{deviceId}/managedswinventory:
    get:
      tags:
      - "Device"
      summary: "Get managed software inventory for the device , based on device ID"
      description: "Get managed software inventory for the device , based on device\
        \ ID"
      operationId: "getManagedSwInventory"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceSwInventoryResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/{deviceId}/policies:
    get:
      tags:
      - "Device"
      summary: "Get policies for the device , based on device ID"
      description: "Get policies for the device , based on device ID"
      operationId: "getDevicePolicies"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DevicePoliciesResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /device/{deviceId}/softwareinventory:
    get:
      tags:
      - "Device"
      summary: "Get software inventory for the device"
      description: "Get software inventory for the device , based on device ID"
      operationId: "getDeviceSoftwareInventory"
      produces:
      - "application/json"
      parameters:
      - name: "deviceId"
        in: "path"
        description: "Numerical id of the device"
        required: true
        type: "integer"
        default: -1
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/DeviceSoftwareInventoryResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment:
    post:
      tags:
      - "Enrollment"
      summary: "Create enrollment invitation"
      description: "Creates an enrollment invitation and sends the One Time Password\
        \ (OTP) for the user"
      operationId: "createEnrollmentInvitation"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/EnrollmentCreateRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/EnrollmentCreateResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment/filter:
    post:
      tags:
      - "Enrollment Filter"
      summary: "Retrieves current enrollment invitations in the system"
      description: "Retrieves current enrollment invitations in the system, based\
        \ on filter criteria"
      operationId: "getEnrollmentByFilter"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/EnrollmentFilterRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/EnrollmentFilterResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment/info:
    get:
      tags:
      - "Enrollment"
      summary: "Get OTP information"
      description: "Lists all the information required to send out enrollment invitations"
      operationId: "getEnrollmentInformation"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "platform"
        in: "query"
        description: "Enrollment info will be return for the provided platform"
        required: false
        type: "string"
        default: "iOS"
        enum:
        - "WINDOWS"
        - "iOS"
        - "ANDROID"
        - "SYMBIAN"
        - "RIM"
        - "UNKNOWN"
        - "WINPHONE"
        - "WINPC"
        - "WINRT"
        - "WINDOWS8"
        - "MACOSX"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/EnrollmentInfoResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment/modes:
    get:
      tags:
      - "Enrollment"
      summary: "Get available enrollment modes"
      description: "Lists the available enrollment modes"
      operationId: "getEnrollmentModes"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/EnrollmentModesResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment/notify:
    post:
      tags:
      - "Enrollment"
      summary: "Trigger notification using OTP(s)"
      description: "Trigger sending out invitation(s) using OTP(s). Supports multiple\
        \ OTPs"
      operationId: "triggerNotification"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "tokenList"
        description: "list of enrollment tokens"
        required: true
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /enrollment/urls:
    post:
      tags:
      - "Enrollment"
      summary: "Get Enrollment URLs for OTP(s)"
      description: "Get Enrollment URLs for OTP(s)"
      operationId: "getEnrollmentUrls"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/EnrollmentUrlRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/EnrollmentUrlResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /groups:
    get:
      tags:
      - "Groups"
      summary: "Get groups"
      description: "Get groups"
      operationId: "getGroups"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserGroupsResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /groups/local:
    get:
      tags:
      - "Groups"
      summary: "Get all local groups"
      description: "Get all local groups"
      operationId: "getAllLocalGroups"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserGroupsResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    post:
      tags:
      - "Groups"
      summary: "Add local group"
      description: "Add local group"
      operationId: "addLocalGroup"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/CPGroup"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserGroupResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /groups/local/{groupName}:
    delete:
      tags:
      - "Groups"
      summary: "Delete local groups"
      description: "Delete local groups"
      operationId: "deleteLocalGroup"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "groupName"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserGroupsResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /groups/search:
    get:
      tags:
      - "Groups"
      summary: "Get group"
      description: "Get group by key"
      operationId: "getGroupsBySearchKey"
      produces:
      - "application/json"
      parameters:
      - name: "searchKey"
        in: "query"
        required: false
        type: "string"
      - name: "domain"
        in: "query"
        required: false
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserGroupsResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap:
    get:
      tags:
      - "Ldap"
      summary: "Get all configured LDAP"
      description: "Get all configured LDAP"
      operationId: "getAllConfiguredLdap"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap/default/{ldapName}:
    put:
      tags:
      - "Ldap"
      summary: "Update active directory"
      description: "Update active directory"
      operationId: "setDefaultLdap"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "ldapName"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap/delete:
    delete:
      tags:
      - "Ldap"
      summary: "Delete multiple ldap config"
      description: "Delete ldap multiple config"
      operationId: "deleteMultipleLdapConfig"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap/msactivedirectory:
    post:
      tags:
      - "Ldap"
      summary: "Add active directory"
      description: "Add active directory"
      operationId: "addMsActiveDirectory"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LdapRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap/msactivedirectory/{ldapName}:
    put:
      tags:
      - "Ldap"
      summary: "Update active directory"
      description: "Update active directory"
      operationId: "updateMsActiveDirectory"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LdapRequest"
      - name: "ldapName"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /ldap/{ldapName}:
    delete:
      tags:
      - "Ldap"
      summary: "Delete ldap config"
      description: "Delete ldap config"
      operationId: "deleteLdapConfig"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "ldapName"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LdapResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /localusersgroups:
    get:
      tags:
      - "Local Users Groups"
      summary: "Get users"
      description: "Get users"
      operationId: "getLocalUsers"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUsersResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    post:
      tags:
      - "Local Users Groups"
      summary: "Add User"
      description: "Add User"
      operationId: "addLocalUser"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LocalUserRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Local Users Groups"
      summary: "Update User"
      description: "Update User"
      operationId: "updateLocalUser"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LocalUserRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /localusersgroups/deletelocalusers:
    delete:
      tags:
      - "Local Users Groups"
      summary: "Delete Users"
      description: "Deleted Users"
      operationId: "deleteLocalUsers"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /localusersgroups/importprovisioningfile:
    post:
      tags:
      - "Local Users Groups"
      summary: "Import Provisioning File User"
      description: "Import Provisioning File User"
      operationId: "importProvisioningFile"
      consumes:
      - "multipart/form-data"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      - name: "uploadFile"
        in: "formData"
        description: "uploaded file"
        required: true
        type: "file"
      - name: "importdata"
        in: "formData"
        description: "importData text"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUsersResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /localusersgroups/password:
    put:
      tags:
      - "Local Users Groups"
      summary: "Reset User"
      description: "Reset User"
      operationId: "resetUserPassword"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/LocalUserRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /localusersgroups/{name}:
    get:
      tags:
      - "Local Users Groups"
      summary: "Get User"
      description: "Get User"
      operationId: "getLocalUser"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "name"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Local Users Groups"
      summary: "Delete User"
      description: "Delete User"
      operationId: "deleteLocalUser"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "name"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/LocalUserResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /netscaler:
    get:
      tags:
      - "Netscaler Gateway"
      summary: "Get netscaler gateway configurations"
      description: "Get netscaler gateway configurations"
      operationId: "getNetscalerGateways"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    post:
      tags:
      - "Netscaler Gateway"
      summary: "Add netscaler gateway configurations"
      description: "Add netscaler gateway configurations"
      operationId: "addNetscalerGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/NSGRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Netscaler Gateway"
      summary: "Delete netscaler gateway configurations"
      description: "Delete netscaler gateway configurations"
      operationId: "deleteNetscalerGateways"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "integer"
            format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /netscaler/default/{id}:
    put:
      tags:
      - "Netscaler Gateway"
      summary: "Set default netscaler gateway configurations"
      description: "Set default netscaler gateway configurations"
      operationId: "setDefaultNetscalerGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /netscaler/{id}:
    put:
      tags:
      - "Netscaler Gateway"
      summary: "Update netscaler gateway configurations"
      description: "Update netscaler gateway configurations"
      operationId: "updateNetscalerGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/NSGRequest"
      - name: "id"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Netscaler Gateway"
      summary: "Add netscaler gateway configuration"
      description: "Add netscaler gateway configuration"
      operationId: "deleteNetscalerGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/NSGResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver:
    get:
      tags:
      - "Notification Server"
      summary: "Get all notification servers"
      description: "Get all notification servers"
      operationId: "getAllNotificationServers"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ListResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/activate/sms/{id}:
    put:
      tags:
      - "Notification Server"
      summary: "Activate SMS gateway"
      description: "Activate SMS gateway"
      operationId: "activateSmsGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/activate/smtp/{id}:
    put:
      tags:
      - "Notification Server"
      summary: "Activate SMTP server"
      description: "Activate SMTP server"
      operationId: "activateSmtpServer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/sms:
    post:
      tags:
      - "Notification Server"
      summary: "Add SMS server"
      description: "Add SMS server"
      operationId: "addSmsGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/SmsServer"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/sms/{id}:
    put:
      tags:
      - "Notification Server"
      summary: "Update SMS server"
      description: "Update SMS server"
      operationId: "updateSmsGateway"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/SmsServer"
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/smtp:
    post:
      tags:
      - "Notification Server"
      summary: "Add SMTP server"
      description: "Add SMTP server"
      operationId: "addSmtpServer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/SmtpServer"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/smtp/{id}:
    put:
      tags:
      - "Notification Server"
      summary: "update SMTP server"
      description: "Update SMTP server"
      operationId: "updateSmtpServer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/SmtpServer"
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /notificationserver/{id}:
    get:
      tags:
      - "Notification Server"
      summary: "Get notification server details"
      description: "Get  notification server details"
      operationId: "getServerDetails"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ListResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Notification Server"
      summary: "Delete notification server"
      description: "Delete notification server"
      operationId: "deleteServer"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /rbac/adgroups/{role}:
    get:
      tags:
      - "Role Based Access Control"
      summary: "Get groups associated with the role"
      description: "Gives all the groups associated with the role"
      operationId: "getRoleAdGroups"
      produces:
      - "application/json"
      parameters:
      - name: "role"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessGetAdGroupsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /rbac/permissiontree/{role}:
    get:
      tags:
      - "Role Based Access Control"
      summary: "Get the role definition tree"
      description: "Gives all the permissions which are available for the given role\
        \ in tree format"
      operationId: "getRolePermissionTree"
      produces:
      - "application/json"
      parameters:
      - name: "role"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleDefinitionTreeResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /rbac/role:
    post:
      tags:
      - "Role Based Access Control"
      summary: "Add a role definition"
      description: "Add a role definition"
      operationId: "addRoleDefinition"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/RoleDefinitionAddRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /rbac/role/{role}:
    get:
      tags:
      - "Role Based Access Control"
      summary: "Get the role definition"
      description: "Gives all the permissions which are available for the given role"
      operationId: "wsGetRoleDefinitionList"
      produces:
      - "application/json"
      parameters:
      - name: "role"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessGetRoleDefResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "Role Based Access Control"
      summary: "Update a role definition"
      description: "Update a role definition"
      operationId: "updateRoleDefinition"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/RoleDefinitionUpdateRequest"
      - name: "role"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "Role Based Access Control"
      summary: "Delete a role definition"
      description: "Delete a role definition"
      operationId: "deleteRoleDefinition"
      produces:
      - "application/json"
      parameters:
      - name: "role"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /rbac/roles:
    get:
      tags:
      - "Role Based Access Control"
      summary: "Get the list of roles"
      description: "Gives the name of all the roles"
      operationId: "getRoleList"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/RoleBasedAccessGetRolesResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /serverproperties:
    get:
      tags:
      - "Server Properties"
      summary: "Get all server properties"
      description: "Get all server properties"
      operationId: "getAllEwProperties"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesGetResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    post:
      tags:
      - "Server Properties"
      summary: "Add server property"
      description: "Add server property"
      operationId: "addEwProperties"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ServerPropertiesRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    put:
      tags:
      - "Server Properties"
      summary: "Update server property"
      description: "Update server property"
      operationId: "editEwProperties"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ServerPropertiesRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
    delete:
      tags:
      - "Server Properties"
      summary: "Delete server properties"
      description: "Delete server properties"
      operationId: "deleteEwConfigProperties"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /serverproperties/filter:
    post:
      tags:
      - "Server Properties"
      summary: "Get server properties by filter"
      description: "Get server properties by filter"
      operationId: "getEwProperties"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ServerPropertiesFilterData"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesGetResponse"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /serverproperties/reset:
    post:
      tags:
      - "Server Properties"
      summary: "Reset server property"
      description: "Reset server property"
      operationId: "resetEwConfigProperties"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ResetPropertiesRequestData"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ServerPropertiesResponseModel"
        400:
          description: "Bad Request"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        403:
          description: "Forbidden"
          schema:
            $ref: "#/definitions/ExceptionContainer"
        500:
          description: "Internal Server Error"
          schema:
            $ref: "#/definitions/ExceptionContainer"
  /sharefile/connectors:
    post:
      tags:
      - "ShareFile Connector"
      summary: "Add new Share File Connector"
      description: "Add new Share File Connector"
      operationId: "addShareFileConnector"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileConnectorCreateRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileConnectorResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /sharefile/connectors/filter:
    post:
      tags:
      - "ShareFile Connector Filter"
      summary: "Get Share File Connectors by filters"
      description: "Get Share File  by filters"
      operationId: "getShareFileConnectors"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileConnectorFetchRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileConnectorsResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /sharefile/connectors/storagezones:
    get:
      tags:
      - "ShareFile Connector Storage Zones"
      summary: "Get all Share File Storage Zones"
      description: "Get all Share File Storage Zones"
      operationId: "getAllShareFileStorageZones"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileStorageZonesResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    post:
      tags:
      - "ShareFile Connector Storage Zones"
      summary: "Add Share File Storage Zone"
      description: "Add Share File Storage Zone"
      operationId: "addShareFileStorageZone"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileStorageZoneRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileStorageZoneResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /sharefile/connectors/storagezones/{storageZoneId}:
    get:
      tags:
      - "ShareFile Connector Storage Zones"
      summary: "Get Share File Storage Zone"
      description: "Get Share File Storage Zone by Id"
      operationId: "getShareFileStorageZoneById"
      produces:
      - "application/json"
      parameters:
      - name: "storageZoneId"
        in: "path"
        required: true
        type: "integer"
        format: "int64"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileStorageZoneResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "ShareFile Connector Storage Zones"
      summary: "Update Share File Storage Zone"
      description: "Update Share File Storage Zone by Id"
      operationId: "updateShareFileStorageZone"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "storageZoneId"
        in: "path"
        required: true
        type: "integer"
        format: "int64"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileStorageZoneRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileStorageZoneResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "ShareFile Connector Storage Zones"
      summary: "Delete Share File Storage Zone"
      description: "Delete Share File Storage Zone by Id"
      operationId: "deleteShareFileStorageZone"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "storageZoneId"
        in: "path"
        required: true
        type: "integer"
        format: "int64"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /sharefile/connectors/{id}:
    get:
      tags:
      - "ShareFile Connector"
      summary: "Get ShareFile Connector by Id"
      description: "Get ShareFile Connector by Ids"
      operationId: "getShareFileConnector"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileConnectorResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "ShareFile Connector"
      summary: "Update Share File Connector"
      description: "Update Share File Connector"
      operationId: "updateShareFileConnector"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "integer"
        format: "int32"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileConnectorCreateRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileConnectorResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "ShareFile Connector"
      summary: "Delete Share File Connector by Id"
      description: "Delete Share File Connector by Id"
      operationId: "deleteShareFileConnector"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "id"
        in: "path"
        required: true
        type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /sharefile/enterprise:
    get:
      tags:
      - "ShareFile Enterprise"
      summary: "Get Share File Enterprise Application"
      description: "Get Share File Enterprise Application"
      operationId: "getShareFileEnterprise"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileEnterpriseResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    post:
      tags:
      - "ShareFile Enterprise"
      summary: "Add Share File Enterprise Application"
      description: "Add Share File Enterprise Application"
      operationId: "addShareFileEnterprise"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileEnterpriseRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileEnterpriseResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    put:
      tags:
      - "ShareFile Enterprise"
      summary: "Update Share File Enterprise Application"
      description: "Update Share File Enterprise Application"
      operationId: "updateShareFileEnterprise"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/ShareFileEnterpriseRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ShareFileEnterpriseResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
    delete:
      tags:
      - "ShareFile Enterprise"
      summary: "Delete Share File Enterprise Application"
      description: "Delete Share File Enterprise Application"
      operationId: "deleteShareFileEnterprise"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/GenericResponse"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /user/{name}/localgroups:
    put:
      tags:
      - "Users"
      summary: "Update local groups for a user"
      description: "Update local groups for a user"
      operationId: "updateUserLocalGroups"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "name"
        in: "path"
        description: "user name"
        required: true
        type: "string"
      - in: "body"
        name: "body"
        required: false
        schema:
          type: "array"
          items:
            type: "string"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserLocalGroupResponseModel"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
  /user/{name}/property:
    post:
      tags:
      - "Users"
      summary: "Add or update user property"
      description: "Add or update user property"
      operationId: "updateUserProperty"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "name"
        in: "path"
        description: "user name"
        required: true
        type: "string"
      - in: "body"
        name: "body"
        required: false
        schema:
          $ref: "#/definitions/UserPropertyRequest"
      - name: "auth_token"
        in: "header"
        description: "authentication token"
        required: true
        type: "string"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/UserPropertyResponseModel"
        400:
          description: "Bad Request"
        403:
          description: "Forbidden"
        500:
          description: "Internal Server Error"
definitions:
  CwcLoginData:
    type: "object"
    properties:
      context:
        type: "string"
      customerId:
        type: "string"
  DeviceUser:
    type: "object"
    required:
    - "userLogin"
    properties:
      user:
        $ref: "#/definitions/SimpleUser"
      lastAuthDate:
        type: "integer"
        format: "int64"
        example: 1479921911405
        description: "User's last authentication date "
      prevAuthDate:
        type: "integer"
        format: "int64"
        example: 1479921911026
        description: "User's previous authentication date "
      userLogin:
        type: "string"
        example: "abc"
        description: "User login name "
    description: "Device User Information"
  DeliveryGroupDeployRequest:
    type: "object"
    required:
    - "roles"
    properties:
      roles:
        type: "array"
        example: "[2, 3]"
        description: "List of delivery group ids or names"
        items:
          type: "string"
    description: "Model for capturing the delivery group deploy request"
  GetAppResponseData:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      applicationListData:
        $ref: "#/definitions/ApplicationListDataModel"
    description: "Application list response data"
  ShareFileStorageZoneRequest:
    type: "object"
    required:
    - "fqdn"
    - "name"
    - "password"
    - "port"
    - "secure"
    - "userName"
    properties:
      name:
        type: "string"
        example: "StorageZone1"
        description: "Name of sharefile storage zone"
      fqdn:
        type: "string"
        example: "subdomain.sharefile.com"
        description: "FQDN of sharefile storage zone"
      port:
        type: "integer"
        format: "int32"
        example: 443
        description: "Port for sharefile storage zone"
      secure:
        type: "boolean"
        example: true
        description: "Set sharefile storage zone secure"
        default: false
      userName:
        type: "string"
        example: "user"
        description: "User name of sharefile storage zone account"
      password:
        type: "string"
        example: "password"
        description: "Password of sharefile storage zone account"
    description: "Model for creating sharefile storage zones"
  Store:
    type: "object"
    required:
    - "faqs"
    - "rating"
    - "screenshots"
    - "storeSettings"
    properties:
      rating:
        $ref: "#/definitions/Rating"
      screenshots:
        type: "array"
        description: "List of screenshots"
        items:
          $ref: "#/definitions/Screenshot"
      faqs:
        type: "array"
        description: "List of frequently asked questions"
        items:
          $ref: "#/definitions/Faq"
      storeSettings:
        $ref: "#/definitions/StoreSettings"
  DeviceActionParameters:
    type: "object"
    properties:
      message:
        type: "string"
        example: "Unable to perform asked action on device '1'"
        description: "Device action failure message"
      id:
        type: "string"
        example: "1"
        description: "Device ID for failed action"
    description: "Device Action Parameters Model"
  DeliveryGroupListDataModel:
    type: "object"
    properties:
      totalMatchCount:
        type: "integer"
        format: "int32"
        example: 10
        description: "Count of total matched records after applying filters"
      totalCount:
        type: "integer"
        format: "int32"
        example: 100
        description: "Count of total records"
      dgList:
        type: "array"
        xml:
          name: "list"
        description: "List of delivery group data"
        items:
          $ref: "#/definitions/DeliveryGroupModel"
    description: "Delivery group list response data"
  SSOStore:
    type: "object"
    required:
    - "acsUrl"
    - "isDomainRequired"
    - "loginUrl"
    - "nameIdFormat"
    - "samlVersion"
    - "ssoMechanismId"
    properties:
      acsUrl:
        type: "string"
        example: "https://access-url.com"
        description: "Access url for connector"
      relayStateUrl:
        type: "string"
        example: "https://relay-url.com"
        description: "Relay state url for connector"
      nameIdFormat:
        type: "string"
        example: "EmailAddress"
        description: "Name id format of connector. Possible values are:<br/>\"EmailAddress\"\
          \ or \"Unspecified\""
      loginUrl:
        type: "string"
        example: "https://login-url.com"
        description: "Login url for connector"
      domainName:
        type: "string"
        example: "domain-name.net"
        description: "Domain name for connectors"
      enterpriseAttrs:
        type: "object"
        example: "{'AcsUrl':''}"
        description: "Enterprise attributes for connector"
        additionalProperties:
          type: "string"
      samlType:
        type: "string"
        example: "idp"
        description: "Security assertion markup language type"
      ssoMechanismId:
        type: "integer"
        format: "int32"
        example: 1
        description: "Single sign on mechanism id"
      samlVersion:
        type: "string"
        example: "1.1"
        description: "Security assertion markup language version"
      isDomainRequired:
        type: "boolean"
        example: true
        description: "Domain required flag for connector"
        default: false
    description: "Mobile store data model"
  DeviceUsedPropertyParameters:
    type: "object"
    properties:
      type:
        type: "string"
        example: "STRING"
        description: "Type of the property"
        enum:
        - "STRING"
        - "INTEGER"
        - "INTEGER_PERCENT"
        - "INTEGER_DATA_SIZE"
        - "INTEGER_SPEED_FREQUENCY"
        - "INTEGER_PIXEL"
        - "INTEGER_PPI"
        - "DECIMAL_INCH"
        - "INTEGER_LEVEL_ENCRYPTION"
        - "INTEGER_MCC"
        - "INTEGER_CELLULAR_TECHNOLOGY"
        - "DATE"
        - "BOOLEAN"
        - "BOOLEAN_CORPORATE_EMPLOYEE"
        - "BOOLEAN_YES_NO"
        - "BOOLEAN_PASSED_FAILED"
        - "OS_FAMILIY"
        - "STRING_AFW_INSTALL_TYPE"
      name:
        type: "string"
        example: "SYSTEM_OEM"
        description: "Name of the property"
      displayName:
        type: "string"
        example: "Device model"
        description: "Display name of the property"
    description: "Device used property parameters data model"
  MobileAppContainerResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      container:
        $ref: "#/definitions/MobileAppContainer"
    description: "Resource container response data"
  UserLocalGroupResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Model for storing the user local group response."
  PolicyResourceDeployState:
    type: "object"
    properties:
      resourceType:
        type: "string"
        example: "SOFTWARE_INVENTORY"
        description: "Resource type of policy "
        enum:
        - "APP_NATIVE"
        - "APP_MDMWEBLINK"
        - "APP_MDX"
        - "APP_WEBLINK"
        - "APP_SAAS"
        - "APP_FMD"
        - "TUNNEL"
        - "REGISTRY"
        - "SERVERGROUP"
        - "SOFTWARE_INVENTORY"
        - "SIGNING_CERTIFICATE"
        - "ENTERPRISE_HUB"
        - "CUSTOM_XML"
        - "DEVICE_HEALTH_ATTESTATION"
        - "FILE"
        - "WIFI"
        - "PROXY"
        - "CERTIFICATE"
        - "EMAIL"
        - "EXCHANGE"
        - "PASSWORD"
        - "VPN"
        - "HUB"
        - "SCHEDULING"
        - "RESTRICTIONS"
        - "LOCATIONSERVICES"
        - "APN"
        - "APPLOCK"
        - "XMOPTIONS"
        - "ROAMING"
        - "MDM_LICENSE_KEY"
        - "SIDELOADINGKEY"
        - "STORAGE"
        - "REMOTE_SUPPORT"
        - "CALENDAR_SUBSCRIPTION"
        - "AIRPLAY"
        - "OS_UPDATE"
        - "AIRPRINT"
        - "SSO_ACCOUNT"
        - "CELLULAR"
        - "PERSONAL_HOTSPOT"
        - "SCEP"
        - "WEB_CONTENT_FILTER"
        - "LDAP"
        - "CALDAV_ACCOUNT"
        - "CARDDAV_ACCOUNT"
        - "FONT"
        - "CREDENTIAL"
        - "MANAGED_DOMAINS"
        - "APP_RESTRICTIONS"
        - "MDM_OPTIONS"
        - "ORGANIZATION_INFO"
        - "BROWSER_OPTIONS"
        - "XEN_MOBILE_UNINSTALL"
        - "APP_ATTRIBUTES"
        - "APP_UNINSTALL_RESTRICTIONS"
        - "FIREWALL"
        - "APP_CONFIGURATION"
        - "IMPORT_PROFILE"
        - "KIOSK"
        - "APP_ACCESS"
        - "PROFILE_REMOVAL"
        - "TERMS_CONDITIONS"
        - "WORX_STORE"
        - "PROVISIONING"
        - "MDM_WEBLINK"
        - "DELETE_APPLICATION"
        - "SMART_ACTION"
        - "ENROLLMENT"
        - "APP_RESTRICTIONS_ANDROID_WORK"
        - "SEAMS"
        - "PROVISIONING_PROFILE"
        - "PROVISIONING_PROFILE_REMOVAL"
        - "CONNECTION_MANAGER"
        - "DELETE_FOLDER_FILE"
        - "DELETE_REGISTRY_KEY_VALUE"
        - "WINCE_PKI_CERTIFICATE"
        - "WIP"
        - "NETWORK_USAGE"
        - "WALLPAPER"
        - "DEVICE_NAME"
        - "DEFENDER"
        - "LAUNCHER_CONFIGURATION"
        - "HOMESCREEN_LAYOUT"
        - "UNCATEGORIZED"
        - "EDUCATION_CONFIGURATION"
        - "MEDIA_IBOOK"
      resourceTypeLabel:
        type: "string"
        example: "Software Inventory"
        description: "Resource Label of policy"
      name:
        type: "string"
        example: "App Inventory"
        description: "Resource name of policy"
      packageInfo:
        type: "string"
        example: "null"
        description: "Package information of application"
      resourceKey:
        type: "string"
        example: "null"
        description: "Resource key of application"
      lastUpdate:
        type: "integer"
        format: "int64"
        example: 1479921902171
        description: "Last update timestamp"
      statusLabel:
        type: "string"
        example: "Success"
        description: "Installation status label"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Installation status"
        enum:
        - "SUCCESS"
        - "FAILURE"
        - "PENDING"
        - "AVAILABLE"
    description: "Model for policy resource deploy state of a device"
  DeviceCoordinates:
    type: "object"
    properties:
      deviceCoordinateList:
        xml:
          name: "gpsCoordinates"
        $ref: "#/definitions/DeviceCoordinateList"
    description: "Device coordinates model"
  Enrollments:
    type: "object"
    properties:
      enrollments:
        type: "array"
        xml:
          name: "enrollmentList"
        description: "List of enrollment"
        items:
          $ref: "#/definitions/Enrollment"
      count:
        type: "integer"
        format: "int64"
        example: 2
        xml:
          name: "totalMatchedCount"
        description: "Total matched count"
      totalCount:
        type: "integer"
        format: "int64"
        example: 2
        description: "Total count"
    description: "Enrollment filter data"
    xml:
      name: "enrollments"
  ServerPropertiesGetResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      allEwProperties:
        type: "array"
        description: "List of server properties"
        items:
          $ref: "#/definitions/ServerPropertiesDto"
    description: "Server Properties Response Model"
  ApplicationListDataModel:
    type: "object"
    properties:
      totalMatchCount:
        type: "integer"
        format: "int32"
        example: 10
        description: "Count of total matched records after applying filters"
      totalCount:
        type: "integer"
        format: "int32"
        example: 100
        description: "Count of total records"
      appList:
        type: "array"
        xml:
          name: "list"
        description: "List of application data"
        items:
          $ref: "#/definitions/ApplicationContainer"
    description: "Application list response data"
  Workflow:
    type: "object"
    required:
    - "completionType"
    - "emailTplId"
    - "managerLevels"
    - "name"
    properties:
      name:
        type: "string"
        example: "workflow name"
        description: "Name of workflow"
      description:
        type: "string"
        example: "description of workflow"
        description: "Description of workflow"
      managerLevels:
        type: "integer"
        format: "int32"
        example: 1
        description: "Levels of manager approval. It could be up to 3 levels. 0 means\
          \ approval is not required"
      completionType:
        type: "integer"
        format: "int32"
        example: 2
        description: "Completion type of workflow"
      additionalApprovers:
        type: "array"
        description: "Additional approvers for workflow"
        items:
          $ref: "#/definitions/Approver"
      emailTplId:
        type: "integer"
        format: "int64"
        example: 22
        description: "Id of \"Appc Application Approval Email\" template"
    description: "Workflow data model"
  DeviceDeliveryGroupsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deliveryGroups:
        type: "array"
        xml:
          name: "result/deliveryGroups"
        description: "Delivery group deployed on the device"
        items:
          $ref: "#/definitions/deliveryGroups"
    description: "Response data for delivery groups associated with the device"
  LocalUser:
    type: "object"
    required:
    - "attributes"
    - "password"
    - "role"
    - "username"
    properties:
      userid:
        type: "integer"
        format: "int64"
        example: 8
        description: "Id of the user"
      username:
        type: "string"
        example: "admin"
        description: "Name of the user"
      password:
        type: "string"
        example: "password"
        description: "Password of the user"
      confirmPassword:
        type: "string"
        example: "password"
        description: "Password of the user(confirmation)"
      groups:
        type: "array"
        example: "['MSP']"
        description: "List of associated groups of user"
        items:
          type: "string"
      attributes:
        type: "object"
        example: "{'badpwdcount': '4', 'asuseremail': 'shankar.ganesh@citrix.com'\
          \ 'company': 'citrix', 'mobile': '4695837854'}"
        description: "Properties of the user"
        additionalProperties:
          type: "string"
      role:
        type: "string"
        example: "ADMIN"
        description: "Permission role for user"
      createdOn:
        type: "string"
        example: "1/10/15 11:42 AM"
        description: "User creation date and time"
      lastAuthenticated:
        type: "string"
        example: "1/10/15 11:42 AM"
        description: "User last authentication date and time"
      domainName:
        type: "string"
        example: "citrix.net"
        description: "Domain name of the user, would be 'local' in case of local user"
      adUser:
        type: "boolean"
        example: false
        description: "Flag to indicate if user is an active directory user"
        default: false
      vppUser:
        type: "boolean"
        example: false
        description: "Flag to indicate if user is associated with volume purchase\
          \ program"
        default: false
      cwcMapped:
        type: "boolean"
        example: false
        description: "Flag to indicate if it is a citrix workspace cloud user"
        default: false
      vppAccounts:
        type: "array"
        description: "VPP Accounts associated with the user"
        items:
          $ref: "#/definitions/VPPAccountParams"
      iconFileName:
        type: "string"
      newIconFile:
        type: "boolean"
        default: false
      iconContent:
        type: "array"
        items:
          type: "string"
          format: "byte"
          pattern: "^(?:[A-Za-z0-9+/]{4})*(?:[A-Za-z0-9+/]{2}==|[A-Za-z0-9+/]{3}=)?$"
      depAccountName:
        type: "string"
        example: "ASM DEP account"
        description: "DEP account name"
    description: "Local User Model"
  RoleNamesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      roleNames:
        type: "array"
        example: "['dg01','dg02']"
        xml:
          name: "names"
        description: "List of role names"
        items:
          type: "string"
    description: "Role names response data"
  DeviceNotifyResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      notificationRequests:
        $ref: "#/definitions/NotificationRequests"
    description: "Device notification response data"
  ClientPropertiesResponseData:
    type: "object"
    properties:
      displayName:
        type: "string"
        example: "Encrypt secrets using Passcode"
        description: "Display name of the client property"
      description:
        type: "string"
        example: "Encrypt secrets using WorxPin or AD password"
        description: "Description of the client property"
      key:
        type: "string"
        example: "ENCRYPT_SECRETS_USING_PASSCODE"
        description: "Client property key"
      value:
        type: "string"
        example: "false"
        description: "Value of the client property"
      preDefined:
        type: "boolean"
        example: false
        description: "Flag to indicate if property is pre-defined"
        default: false
    description: "Client Properties Response Data Model"
  SmsServer:
    type: "object"
    required:
    - "carrierGateway"
    - "country"
    - "https"
    - "key"
    - "name"
    - "secret"
    - "virtualPhoneNumber"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 2
        description: "Id of the server"
      active:
        type: "string"
        example: "true"
        description: "Flag to indicate if the server configuration is active"
      name:
        type: "string"
        example: "SMTP Server"
        description: "Name of the server configuration"
      server:
        type: "string"
        example: "10.199.242.111"
        description: "Notification server host name or IP address"
      serverType:
        type: "string"
        example: "SMS"
        description: "Type of the notification server. Can be SMTP or SMS"
      description:
        type: "string"
        example: "SMS server description"
        description: "Description for the sms server"
      key:
        type: "string"
        example: "123456"
        description: "Key of the SMS server"
      secret:
        type: "string"
        example: "secretKey"
        description: "SMS server secret key"
      virtualPhoneNumber:
        type: "string"
        example: "4086792222"
        description: "SMS server virtual phone number"
      https:
        type: "boolean"
        example: false
        description: "Flag to indicate if https is on"
        default: false
      country:
        type: "string"
        example: "+93"
        description: "Country code"
      carrierGateway:
        type: "boolean"
        example: true
        description: "Flag to indicate if Carrier Gateway option is enabled"
        default: false
    description: "Model for SMS server configuration data"
  LdapResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      result:
        type: "array"
        description: "Ldap configurations list"
        items:
          $ref: "#/definitions/LdapResponseDataModel"
    description: "LDAP configuration response data model"
  deliveryGroups:
    type: "object"
    properties:
      lastUpdate:
        type: "integer"
        format: "int64"
        example: 1479921911125
        description: "Timestamp of last update of delivery group"
      statusLabel:
        type: "string"
        example: "Success"
        description: "Status label of delivery group"
      linkey:
        type: "string"
        example: "Delivery Group 1"
        description: "Delivery group linkey. Would be same as delivery group name"
      name:
        type: "string"
        example: "Delivery Group 1"
        description: "Name of delivery group"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Status of delivery group"
        enum:
        - "SUCCESS"
        - "FAILURE"
        - "PENDING"
        - "AVAILABLE"
    description: "Operations for viewing, adding, updating, deleting, deploying and\
      \ enabling/disabling delivery groups"
  DeviceUsedProperties:
    type: "object"
    properties:
      deviceUsedPropertiesParameters:
        type: "array"
        xml:
          name: "usedProperties"
        description: "device used property parameters list"
        items:
          $ref: "#/definitions/DeviceUsedPropertyParameters"
    description: "Device used properties data model"
  SmtpServer:
    type: "object"
    required:
    - "authentication"
    - "fromEmail"
    - "fromName"
    - "msSecurePasswordAuth"
    - "name"
    - "password"
    - "port"
    - "secureChannelProtocol"
    - "server"
    - "username"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of the smtp server"
      active:
        type: "string"
        example: "true"
        description: "Flag to indicate if the server configuration is active"
      name:
        type: "string"
        example: "SMTP Config"
        description: "Unique name for the SMTP configuration"
      server:
        type: "string"
        example: "10.199.242.111"
        description: "Notification server host name or IP address"
      serverType:
        type: "string"
        example: "SMS"
        description: "Type of the notification server. Can be SMTP or SMS"
      description:
        type: "string"
        example: "Test SMTP configuration"
        description: "Description for the smtp server"
      secureChannelProtocol:
        type: "string"
        example: "SSL"
        description: "Secure channel protocol used for the SMTP server. Can be SSL,\
          \ TLS or NONE"
      port:
        type: "integer"
        format: "int32"
        example: 25
        description: "SMTP server port"
      authentication:
        type: "boolean"
        example: false
        description: "Flag to indicate if SMTP server authentication is required"
        default: false
      username:
        type: "string"
        example: "user"
        description: "User name for SMTP server authentication. Required if SMTP server\
          \ authentication is enabled"
      password:
        type: "string"
        example: "testPassword"
        description: "Password for SMTP server authentication. Required if SMTP server\
          \ authentication is enabled"
      msSecurePasswordAuth:
        type: "boolean"
        example: true
        description: "Flag to indicate if Microsoft Secure Password Authentication\
          \ (SPA) is enabled"
        default: false
      fromName:
        type: "string"
        example: "Test Account"
        description: "From Name"
      fromEmail:
        type: "string"
        example: "test@agsag.com"
        description: "From email"
      numOfRetries:
        type: "integer"
        format: "int32"
        example: 5
        description: "Number of SMTP retries"
      timeout:
        type: "integer"
        format: "int32"
        example: 30
        description: "SMTP Timeout"
      maxRecipients:
        type: "integer"
        format: "int32"
        example: 100
        description: "Maximum number of SMTP recipients"
    description: "Model for SMTP server configuration data"
  DeviceMdmStatus:
    type: "object"
    properties:
      deviceMdmStatusParameters:
        xml:
          name: "mdmStatus"
        $ref: "#/definitions/DeviceMdmStatusParameters"
    description: "Device MDM status data model"
  NotifyRecipientData:
    type: "object"
    required:
    - "serialNumber"
    properties:
      deviceId:
        type: "integer"
        format: "int32"
        example: 1
        description: "Numeric id of device"
      email:
        type: "string"
        example: "user@test.com"
        description: "Email address as SMTP Recipient, required for SMTP notification"
      osFamily:
        type: "string"
        example: "iOS"
        description: "OS Family of device"
      serialNumber:
        type: "string"
        example: "F7NLX6WDF196"
        description: "Serial Number of device for agent notification, required for\
          \ android device for agent notification"
      smsTo:
        type: "string"
        example: "+123456676"
        description: "Mobile number for SMS recipient, Required if you want to send\
          \ SMS notification"
      token:
        $ref: "#/definitions/NotifyTokenModel"
    description: "Model for capturing recipients of notification"
  VPPAccountParams:
    type: "object"
    required:
    - "country"
    - "id"
    - "name"
    - "stoken"
    - "suffix"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "ID of VPP account"
      name:
        type: "string"
        example: "name"
        description: "Name of VPP account"
      suffix:
        type: "string"
        example: "suffix"
        description: "Suffix of VPP account"
      country:
        type: "string"
        example: "Default"
        description: "Country of VPP account"
      stoken:
        type: "string"
        example: "joiQ0lUUk....U1GNTM3QjV3UT09In0="
        description: "VPP account sToken"
  DeviceUsedPropertiesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deviceUsedPropertiesList:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceUsedPropertiesList"
    description: "Device used properties response model"
  ResetPropertiesRequestData:
    type: "object"
    properties:
      names:
        type: "array"
        example: "['CONNECTION_TIMEOUT']"
        description: "List of keys of the server properties that we want to reset"
        items:
          type: "string"
    description: "Request data model for reset server properties"
  RoleDeployStatusResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      name:
        type: "string"
        example: "dg01"
        description: "Role name"
      nbSuccess:
        type: "integer"
        format: "int32"
        example: 1
        description: "Role success count"
      nbFailure:
        type: "integer"
        format: "int32"
        example: 0
        description: "Role failure count"
      nbPending:
        type: "integer"
        format: "int32"
        example: 0
        description: "Role pending count"
    description: "Response data for role deploy state"
  DeliveryGroupsFilterDataModel:
    type: "object"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Start index of result set. Default: 0 (Optional)"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Number of results to return. Default: 10 (Optional)"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "Sort order of result set. Default: ASC (Optional)"
        enum:
        - "ASC"
        - "DESC"
      search:
        type: "string"
        example: "search string"
        description: "Generic search term. Default: {empty} (Optional)"
      enableCount:
        type: "boolean"
        example: true
        description: "Return count of total records. Default: true (Optional)"
        default: false
      filterIds:
        type: "string"
        example: "[\"deliverygroup.action#actionName@_fn_@dg.action\", \"deliverygroup.application#appName@_fn_@dg.app\"\
          ]"
        description: "Special format for filtering results based on available filters.\
          \ Default: {empty} (Optional)"
      deliveryGroupSortColumn:
        type: "string"
        example: "id"
        description: "Column name on which result set needs to be sorted. Default:\
          \ id (Optional)"
        enum:
        - "id"
        - "name"
        - "lastUpdated"
    description: "Model for capturing delivery group's filter criteria"
  EnrollmentCreateResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      token:
        type: "string"
        example: "ep-802b9bd5-7eaa-4eb8-aecb-c21a8f9f8080"
        description: "Enrollment invitation token"
      url:
        type: "string"
        example: "https://10.20.30.40:8443/zdm/su?e=ep-802b9bd5-7eaa-4eb8-aecb-c21a8f9f8080"
        description: "Enrollment invitation url"
    description: "Enrollment invitation reponse data"
  AVPPTokenRecordParams:
    type: "object"
    required:
    - "deviceSerial"
    - "licenseId"
    - "user"
    - "vppUserId"
    properties:
      licenseId:
        type: "string"
        example: "8426782"
        description: "VPP license id"
      user:
        type: "string"
        example: "user"
        description: "User name associated with VPP token"
      vppUserId:
        type: "integer"
        format: "int32"
        example: 12
        description: "User ID associated with VPP token"
      deviceSerial:
        type: "string"
        example: "SERIAL-CCC1-1-71-1"
        description: "Device serial associated with VPP token"
  PublicStoreAppContainerRequest:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "name"
        description: "Name of application"
      description:
        type: "string"
        example: "description"
        description: "Description of application"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['dg01','dg02']"
        description: "List of roles associated with application"
        items:
          type: "string"
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      workflowTemplateName:
        type: "string"
        example: "WF"
        description: "Name of workflow template to be assigned to the app"
      iphone:
        $ref: "#/definitions/PublicStoreAppData"
      ipad:
        $ref: "#/definitions/PublicStoreAppData"
      android:
        $ref: "#/definitions/PublicStoreAppData"
      windows:
        $ref: "#/definitions/PublicStoreAppData"
      android_work:
        $ref: "#/definitions/PublicStoreAppData"
      windows_phone:
        $ref: "#/definitions/PublicStoreAppData"
    description: "Request for public store application"
  GeneratePinCode:
    type: "object"
    properties:
      answer:
        type: "string"
        example: "156797"
        xml:
          name: "stringAnswer/answer"
        description: "Pin code"
    description: "Pin code generate model"
  UserPropertyResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Model for storing the user property update response."
  LdapResponseDataModel:
    type: "object"
    required:
    - "domain"
    - "domainAlias"
    - "globalCatalogPort"
    - "groupBaseDN"
    - "lockoutLimit"
    - "lockoutTime"
    - "password"
    - "port"
    - "primaryHost"
    - "type"
    - "userBaseDN"
    - "userSearchBy"
    - "username"
    properties:
      domain:
        type: "string"
        example: "citrix.net"
        description: "LDAP domain name which should be unique from other configuration"
      userBaseDN:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "User base domain name"
      groupBaseDN:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "Group base domain name"
      password:
        type: "string"
        example: "password"
        description: "Password for LDAP server authentication"
      port:
        type: "integer"
        format: "int32"
        example: 3268
        description: "Port number"
      username:
        type: "string"
        example: "test@citrix.net"
        description: "Username for ldap authentication"
      primaryHost:
        type: "string"
        example: "10.20.30.40"
        description: "Primary server IP address / hostname"
      useSecure:
        type: "boolean"
        example: false
        description: "Flag to indicate if secure connection is used"
        default: false
      globalCatalogPort:
        type: "integer"
        format: "int32"
        example: 3268
        description: "Global Catalog TCP Port"
      secondaryHost:
        type: "string"
        example: " "
        description: "Secondary Host IP address"
      lockoutLimit:
        type: "integer"
        format: "int32"
        example: 0
        description: "XenMobile Lockout Limit"
      userSearchBy:
        type: "string"
        example: "upn"
        description: "User search method. Can be 'upn' or 'samaccountname'"
      gcRootContext:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "Global Catalog Root Context"
      lockoutTime:
        type: "integer"
        format: "int32"
        example: 1
        description: "XenMobile Lockout Time"
      domainAlias:
        type: "string"
        example: "citrix.net"
        description: "Domain name alias"
      name:
        type: "string"
        example: "activeDirectory1"
        description: "Unique identifier used to update or delete the config"
      type:
        type: "string"
        example: "activedirectory"
        description: "LDAP Type"
      defaultDomain:
        type: "boolean"
        example: true
        description: "Flag indicates whether this LDAP configuration is default"
        default: false
    description: "Ldap Response Data Model"
  EnrollmentUrlRequest:
    type: "object"
    required:
    - "otps"
    properties:
      otps:
        type: "array"
        example: "['ep-8f4748bd-2ce5-452a-b353-5d9011b7fc03','ep-8f4748bd-2ce5-452a-b353-5d9011b7fc04']"
        description: "List of enrollment tokens"
        items:
          type: "string"
    description: "Model for list of enrollment tokens"
  LoginData:
    type: "object"
    required:
    - "login"
    - "password"
    properties:
      login:
        type: "string"
        example: "administrator"
        description: "userName"
      password:
        type: "string"
        example: "password"
        description: "password"
    description: "Login request data container"
  DeviceCoordinate:
    type: "object"
    properties:
      latitude:
        type: "number"
        format: "double"
        example: 55.53280640362135756049610790796577930450439453125
        description: "Latitude of device location"
      longitude:
        type: "number"
        format: "double"
        example: 44.34457692161573305611454998143017292022705078125
        description: "Longitude of device location"
      accuracy:
        type: "number"
        format: "double"
        example: 165
        description: "Accuracy of device location"
      gpsTimestamp:
        type: "integer"
        format: "int64"
        example: 1479975748000
        xml:
          name: "timestamp"
        description: "GPS timestamp"
    description: "Device coordinates model to locate the device"
  MDXPolicy:
    type: "object"
    required:
    - "description"
    - "policyCategory"
    - "policyName"
    - "policyType"
    - "policyValue"
    - "title"
    properties:
      policyName:
        type: "string"
        example: "policy name"
        description: "Policy name"
      policyValue:
        type: "string"
        example: "true/string"
        description: "Policy value"
      policyType:
        type: "string"
        example: "Boolean/String"
        description: "Data type of policy value"
      policyCategory:
        type: "string"
        example: "Authentication"
        description: "Category of policy"
      title:
        type: "string"
        example: "App Passcode"
        description: "Title of policy"
      description:
        type: "string"
        example: "policy description"
        description: "Description of policy"
      units:
        type: "string"
        example: "units"
        description: "Policy units"
      explanation:
        type: "string"
        example: "explanation"
        description: "Explanation of policy"
  DeploymentSchedule:
    type: "object"
    required:
    - "deployInBackground"
    - "deploySchedule"
    - "deployScheduleCondition"
    - "enableDeployment"
    properties:
      enableDeployment:
        type: "boolean"
        example: true
        description: "Deployment is enabled or not"
        default: false
      deploySchedule:
        type: "string"
        example: "NOW"
        description: "Deployment schedule time"
        enum:
        - "NOW"
        - "LATER"
      deployScheduleCondition:
        type: "string"
        example: "EVERYTIME"
        description: "Deployment schedule condition"
        enum:
        - "EVERYTIME"
        - "ONPREVIOUSFAILED"
      deployDate:
        type: "string"
        example: "03/14/2015"
        description: "Scheduled deployment date"
      deployTime:
        type: "string"
        example: "17:44"
        description: "Scheduled deployment time"
      deployInBackground:
        type: "boolean"
        example: false
        description: "Whether to allow deployment in background or not"
        default: false
  DeployState:
    type: "object"
    required:
    - "date"
    - "packageId"
    - "packageName"
    - "status"
    - "statusLabel"
    properties:
      statusLabel:
        type: "string"
        example: "Success"
        description: "Status label of the deployment package"
      packageId:
        type: "integer"
        format: "int32"
        example: 14
        description: "Database Id for the deployment package"
      packageName:
        type: "string"
        example: "Delivery Group 2"
        description: "Name of the deployment package"
      date:
        type: "integer"
        format: "int64"
        example: 147992190212
        description: "Date for the deployment package"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Status the deployment package"
        enum:
        - "PENDING"
        - "SUCCESS"
        - "FAIL"
        - "NOT_APPLICABLE"
    description: "Deployment State for the delivery group"
  AppsFilterDataModel:
    type: "object"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Start index of result set. Default: 0 (Optional)"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Number of results to return. Default: 10 (Optional)"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "Sort order of result set. Default: ASC (Optional)"
        enum:
        - "ASC"
        - "DESC"
      search:
        type: "string"
        example: "search string"
        description: "Generic search term. Default: {empty} (Optional)"
      enableCount:
        type: "boolean"
        example: true
        description: "Return count of total records. Default: true (Optional)"
        default: false
      filterIds:
        type: "string"
        example: "[\"deliverygroup.action#actionName@_fn_@dg.action\", \"deliverygroup.application#appName@_fn_@dg.app\"\
          ]"
        description: "Special format for filtering results based on available filters.\
          \ Default: {empty} (Optional)"
      applicationSortColumn:
        type: "string"
        example: "id"
        description: "Column name on which result set needs to be sorted. Default:\
          \ id (Optional)"
        enum:
        - "id"
        - "name"
        - "appType"
        - "createdOn"
        - "lastUpdated"
        - "disabled"
        - "vppAccount"
    description: "Model for capturing application's filter criteria"
  NotificationTemplateMsg:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 12
        description: "Id for the notification template message"
      channel:
        type: "string"
        example: "AGENT"
        description: "Notification channel"
        enum:
        - "SMS"
        - "SMTP"
        - "AGENT"
        - "AGENT_SHTP"
        - "SMS_GATEWAY"
      from:
        type: "string"
        example: "TEST-XMS"
        description: "From address for notification"
      message:
        type: "string"
        example: "this is test message"
        description: "Notification message"
      subject:
        type: "string"
        example: "this is test subject"
        description: "Notification subject"
      to:
        type: "string"
        example: "abc@test.com"
        description: "recipient for notification"
      customProperties:
        type: "string"
        example: "null"
        description: "Custom properties"
      locale:
        type: "string"
        example: "US"
        description: "Locale"
    description: "Notification template message model"
    xml:
      name: "notificationTemplateMsg"
  Screenshot:
    type: "object"
    properties:
      data:
        type: "string"
        example: "iVBORw0KGgoAAAANSU...AAAElFTkSuQmCC"
        description: "Screenshot base64 encoded data"
      displayOrder:
        type: "integer"
        format: "int32"
        example: 1
        description: "Display order of screenshot"
  RoleBasedAccessGetAdGroupsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      adGroups:
        type: "array"
        description: "List of active directory groups"
        items:
          $ref: "#/definitions/AdGroup"
    description: "Role Based Access Get AdGroups Response Model"
  DeliveryGroupUser:
    type: "object"
    required:
    - "domainName"
    - "name"
    - "uniqueId"
    - "uniqueName"
    properties:
      uniqueName:
        type: "string"
        example: "localuser"
        xml:
          name: "uniquename"
        description: "Unique name of user"
      domainName:
        type: "string"
        example: "local"
        xml:
          name: "domainname"
        description: "Domain name of user"
      name:
        type: "string"
        example: "localuser"
        description: "User name"
      objectSid:
        type: "string"
        example: "0"
        description: "Object Sid of user"
      customProperties:
        type: "object"
        description: "Custom properties of user"
        additionalProperties:
          type: "string"
      uniqueId:
        type: "string"
        example: "localuser"
        description: "Unique id of user"
  LocalUserRequest:
    type: "object"
    required:
    - "attributes"
    - "password"
    - "role"
    - "username"
    properties:
      userid:
        type: "integer"
        format: "int64"
        example: 8
        description: "Id of the user"
      username:
        type: "string"
        example: "user1"
        description: "Name of the user"
      password:
        type: "string"
        example: "password"
        description: "Password of the user"
      confirmPassword:
        type: "string"
        example: "password"
        description: "Password of the user (confirmation)"
      groups:
        type: "array"
        example: "['MSP']"
        description: "List of associated groups of user"
        items:
          type: "string"
      attributes:
        type: "object"
        example: "{'badpwdcount': '4', 'asuseremail': 'testUser@citrix.com', 'company':\
          \ 'citrix', 'mobile': '4695837854'}"
        description: "Properties of the user"
        additionalProperties:
          type: "string"
      role:
        type: "string"
        example: "USER"
        description: "Permission role for user"
      createdOn:
        type: "string"
        example: "1/10/15 11:42 AM"
        description: "User creation date and time"
      lastAuthenticated:
        type: "string"
        example: "1/10/15 11:42 AM"
        description: "User last authentication date and time "
      domainName:
        type: "string"
        example: "citrix.net"
        description: "Domain name of the user, would be 'local' in case of local user"
      adUser:
        type: "boolean"
        example: false
        description: "Flag to indicate if user is an active directory user"
        default: false
      vppUser:
        type: "boolean"
        example: false
        description: "Flag to indicate if user is associated with volume purchase\
          \ program"
        default: false
      cwcMapped:
        type: "boolean"
        example: false
        description: "Flag to indicate if user is cwc mapped"
        default: false
    description: "Local User Request Model"
  DevicePropertyRequest:
    type: "object"
    required:
    - "name"
    - "value"
    properties:
      name:
        type: "string"
        example: "ACTIVE_ITUNES"
        description: "Property name"
      value:
        type: "string"
        example: "0"
        description: "Property value"
    description: "Model for capturing the device property add/update request"
  EnrollmentNotificationTemplate:
    type: "object"
    properties:
      name:
        type: "string"
        example: "Enrollment Invitation"
        description: "Name of the notification template.<br/>This should be provided\
          \ from the list of available notification templates for the specified category.<br/>Empty\
          \ value will disassociate the existing assigned notification template."
    description: "Model for enrollment notification category"
  LocalUserResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      user:
        $ref: "#/definitions/LocalUser"
    description: "Local User Response Model"
  WebApplicationContainer:
    type: "object"
    required:
    - "appType"
    - "application"
    - "categories"
    - "createdOn"
    - "description"
    - "disabled"
    - "iconData"
    - "id"
    - "lastUpdated"
    - "name"
    - "permitAsRequired"
    - "roles"
    - "schedule"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of container"
      name:
        type: "string"
        example: "container name"
        description: "Name of container"
      description:
        type: "string"
        example: "description of container"
        description: "Description of container"
      createdOn:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Creation date and time of container"
      lastUpdated:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Last modification date and time of container"
      disabled:
        type: "boolean"
        example: false
        description: "Identifies whether container is disabled or not"
        default: false
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      permitAsRequired:
        type: "boolean"
        example: true
        description: "Mark application container as required or not"
        default: false
      iconData:
        type: "string"
        example: "iVBORw0KGgoAAAANSU...AAAElFTkSuQmCC"
        description: "Icon data of application"
      appType:
        type: "string"
        example: "App Store App"
        description: "Type of application container. Expected types are:<br/>MDX,\
          \ Enterprise, App Store App, Web Link, Web & SaaS"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application container"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['AllUsers']"
        description: "List of delivery groups associated with application container"
        items:
          type: "string"
      workflow:
        $ref: "#/definitions/Workflow"
      vppAccount:
        type: "string"
        example: "name"
        description: "Name of VPP account"
      application:
        $ref: "#/definitions/Application"
    description: "Model for WebLink and Web SaaS application data"
  ProvisionStore:
    type: "object"
    required:
    - "loginName"
    - "password"
    properties:
      password:
        type: "string"
        description: "Password for provisioning store"
      loginName:
        type: "string"
        example: "username"
        xml:
          name: "login"
        description: "User login name for provisioning store"
    description: "Provision store data model"
  ActionResourceDeployState:
    type: "object"
    properties:
      resourceType:
        type: "string"
        example: "SMART_ACTION"
        description: "Resource type of policy "
        enum:
        - "APP_NATIVE"
        - "APP_MDMWEBLINK"
        - "APP_MDX"
        - "APP_WEBLINK"
        - "APP_SAAS"
        - "APP_FMD"
        - "TUNNEL"
        - "REGISTRY"
        - "SERVERGROUP"
        - "SOFTWARE_INVENTORY"
        - "SIGNING_CERTIFICATE"
        - "ENTERPRISE_HUB"
        - "CUSTOM_XML"
        - "DEVICE_HEALTH_ATTESTATION"
        - "FILE"
        - "WIFI"
        - "PROXY"
        - "CERTIFICATE"
        - "EMAIL"
        - "EXCHANGE"
        - "PASSWORD"
        - "VPN"
        - "HUB"
        - "SCHEDULING"
        - "RESTRICTIONS"
        - "LOCATIONSERVICES"
        - "APN"
        - "APPLOCK"
        - "XMOPTIONS"
        - "ROAMING"
        - "MDM_LICENSE_KEY"
        - "SIDELOADINGKEY"
        - "STORAGE"
        - "REMOTE_SUPPORT"
        - "CALENDAR_SUBSCRIPTION"
        - "AIRPLAY"
        - "OS_UPDATE"
        - "AIRPRINT"
        - "SSO_ACCOUNT"
        - "CELLULAR"
        - "PERSONAL_HOTSPOT"
        - "SCEP"
        - "WEB_CONTENT_FILTER"
        - "LDAP"
        - "CALDAV_ACCOUNT"
        - "CARDDAV_ACCOUNT"
        - "FONT"
        - "CREDENTIAL"
        - "MANAGED_DOMAINS"
        - "APP_RESTRICTIONS"
        - "MDM_OPTIONS"
        - "ORGANIZATION_INFO"
        - "BROWSER_OPTIONS"
        - "XEN_MOBILE_UNINSTALL"
        - "APP_ATTRIBUTES"
        - "APP_UNINSTALL_RESTRICTIONS"
        - "FIREWALL"
        - "APP_CONFIGURATION"
        - "IMPORT_PROFILE"
        - "KIOSK"
        - "APP_ACCESS"
        - "PROFILE_REMOVAL"
        - "TERMS_CONDITIONS"
        - "WORX_STORE"
        - "PROVISIONING"
        - "MDM_WEBLINK"
        - "DELETE_APPLICATION"
        - "SMART_ACTION"
        - "ENROLLMENT"
        - "APP_RESTRICTIONS_ANDROID_WORK"
        - "SEAMS"
        - "PROVISIONING_PROFILE"
        - "PROVISIONING_PROFILE_REMOVAL"
        - "CONNECTION_MANAGER"
        - "DELETE_FOLDER_FILE"
        - "DELETE_REGISTRY_KEY_VALUE"
        - "WINCE_PKI_CERTIFICATE"
        - "WIP"
        - "NETWORK_USAGE"
        - "WALLPAPER"
        - "DEVICE_NAME"
        - "DEFENDER"
        - "LAUNCHER_CONFIGURATION"
        - "HOMESCREEN_LAYOUT"
        - "UNCATEGORIZED"
        - "EDUCATION_CONFIGURATION"
        - "MEDIA_IBOOK"
      resourceTypeLabel:
        type: "string"
        example: "Smart Action"
        description: "Resource Label of policy"
      name:
        type: "string"
        example: "Smart Action 1"
        description: "Resource name of policy"
      packageInfo:
        type: "string"
        example: "null"
        description: "Package information of application"
      resourceKey:
        type: "string"
        example: "null"
        description: "Resource key of application"
      lastUpdate:
        type: "integer"
        format: "int64"
        example: 1479921902171
        description: "Last update timestamp"
      statusLabel:
        type: "string"
        example: "Success"
        description: "Installation status label"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Installation status"
        enum:
        - "SUCCESS"
        - "FAILURE"
        - "PENDING"
        - "AVAILABLE"
    description: "Model for smart action resource deploy state of a device"
  ClientPropertiesRequest:
    type: "object"
    required:
    - "description"
    - "displayName"
    - "value"
    properties:
      value:
        type: "string"
        example: "15"
        description: "Value of the client property"
      displayName:
        type: "string"
        example: "MyProperty"
        description: "Display name of the client property"
      description:
        type: "string"
        example: "MyProperty Description"
        description: "Description of the client property"
    description: "Client Properties Request Model"
  ServerPropertiesRequest:
    type: "object"
    required:
    - "displayName"
    - "name"
    - "value"
    properties:
      name:
        type: "string"
        example: "ag.client.cert.throttling.minutes"
        description: "Server property name"
      value:
        type: "string"
        example: "30"
        description: "Value of the server property"
      displayName:
        type: "string"
        example: "NetScaler Gateway Client Cert Issuing Throttling Interval"
        description: "Display name of the server property"
      description:
        type: "string"
        example: "Throttling interval for issuance of NetScaler Gateway client certificates."
        description: "Description of the server property"
      displayFlag:
        type: "boolean"
        example: false
        description: "Flag to indicate if server property should be visible in console"
        default: false
    description: "Request Data of the Server Properties Model"
  DeviceAction:
    type: "object"
    properties:
      actionType:
        type: "string"
        example: "WIPE"
        description: "Action type perform on device"
        enum:
        - "WIPE"
        - "CORPORATE_WIPE"
        - "SD_CARD_WIPE"
        - "REBOOT"
        - "LOCK"
        - "UNLOCK"
        - "LOCATE"
        - "ENABLE_TRACKING"
        - "DISABLE_TRACKING"
        - "CONTAINER_LOCK"
        - "CONTAINER_UNLOCK"
        - "CONTAINER_PWD_RESET"
        - "DEP_ACTIVATION_LOCK"
        - "ACTIVATION_LOCK_BYPASS"
        - "RING"
        - "ROAMING"
        - "CLEAR_RESTRICTIONS"
        - "APP_WIPE"
        - "APP_LOCK"
        - "REQUEST_MIRRORING"
        - "STOP_MIRRORING"
        - "ENABLE_LOST_MODE"
        - "DISABLE_LOST_MODE"
        - "GET_AVAILABLE_OS_UPDATE"
        - "INSTALL_AVAILABLE_OS_UPDATE"
        - "FORCE_INSTALL_OS_UPDATE"
        - "RESTART"
        - "SHUTDOWN"
      doneTime:
        type: "integer"
        format: "int64"
        example: 1479993483807
        description: "Action performed timestamp on device"
      failedTime:
        type: "integer"
        format: "int64"
        example: 1479993483807
        description: "Action failed timestamp on device"
      askedTime:
        type: "integer"
        format: "int64"
        example: 1478883483807
        description: "Action asked timestamp on device"
    description: "Device Action"
  PublicStoreAppContainer:
    type: "object"
    required:
    - "appType"
    - "categories"
    - "createdOn"
    - "description"
    - "disabled"
    - "iconData"
    - "id"
    - "lastUpdated"
    - "name"
    - "permitAsRequired"
    - "roles"
    - "schedule"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of container"
      name:
        type: "string"
        example: "container name"
        description: "Name of container"
      description:
        type: "string"
        example: "description of container"
        description: "Description of container"
      createdOn:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Creation date and time of container"
      lastUpdated:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Last modification date and time of container"
      disabled:
        type: "boolean"
        example: false
        description: "Identifies whether container is disabled or not"
        default: false
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      permitAsRequired:
        type: "boolean"
        example: true
        description: "Mark application container as required or not"
        default: false
      iconData:
        type: "string"
        example: "iVBORw0KGgoAAAANSU...AAAElFTkSuQmCC"
        description: "Icon data of application"
      appType:
        type: "string"
        example: "App Store App"
        description: "Type of application container. Expected types are:<br/>MDX,\
          \ Enterprise, App Store App, Web Link, Web & SaaS"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application container"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['AllUsers']"
        description: "List of delivery groups associated with application container"
        items:
          type: "string"
      workflow:
        $ref: "#/definitions/Workflow"
      vppAccount:
        type: "string"
        example: "name"
        description: "Name of VPP account"
      iphone:
        $ref: "#/definitions/PublicStoreAppPlatformData"
      ipad:
        $ref: "#/definitions/PublicStoreAppPlatformData"
      android:
        $ref: "#/definitions/PublicStoreAppPlatformData"
      windows:
        $ref: "#/definitions/PublicStoreAppPlatformData"
      android_work:
        $ref: "#/definitions/PublicStoreAppPlatformData"
      windows_phone:
        $ref: "#/definitions/PublicStoreAppPlatformData"
    description: "Model for public store application container data"
  Enrollment:
    type: "object"
    properties:
      token:
        type: "string"
        example: "ep-31ae1cb3-f96b-41dd-8d87-c245799a04af"
        description: "Enrollment token"
      type:
        type: "string"
        example: "iOS"
        description: "Enrollment platform type"
        enum:
        - "iOS"
        - "MACOSX"
        - "SHTP"
        - "WINPHONE"
      typeLabel:
        type: "string"
        example: "iOS"
        description: "Enrollment type label"
      mode:
        type: "string"
        example: "classic"
        description: "Enrollment mode"
      userName:
        type: "string"
        example: "local1"
        description: "User name"
      deviceBindingType:
        type: "string"
        example: "SERIALNUMBER"
        description: "Device binding type"
        enum:
        - "UDID"
        - "SERIALNUMBER"
        - "IMEI"
      deviceBindingTypeLabel:
        type: "string"
        example: "Serial Number"
        description: "Device binding type label"
      deviceBindingData:
        type: "string"
        example: "987654321"
        description: "Device binding data"
      secret:
        type: "string"
        example: "null"
        description: "Secret"
      createTime:
        type: "integer"
        format: "int64"
        example: 1476618383925
        description: "Url creation timestamp"
      validUntil:
        type: "integer"
        format: "int64"
        example: "null"
        description: "Validity until"
      status:
        type: "string"
        example: "PENDING"
        description: "Status of invitation url"
        enum:
        - "PENDING"
        - "REDEEMED"
        - "EXPIRED"
        - "FAILED"
      statusLabel:
        type: "string"
        example: "Pending"
        description: "Status label label for enrollment url"
      notificationTemplateCategories:
        type: "array"
        description: "Notification template list by category"
        items:
          $ref: "#/definitions/NotificationTemplateCategory"
    description: "Enrollment filter data model"
    xml:
      name: "enrollment"
  Approver:
    type: "object"
    required:
    - "displayName"
    - "distinguishedName"
    - "domain"
    - "email"
    - "samaccountName"
    - "userPrincipal"
    properties:
      displayName:
        type: "string"
        example: "User"
        description: "Display name of approver"
      domain:
        type: "string"
        example: "domain-name.net"
        description: "Domain name of approver"
      userPrincipal:
        type: "string"
        example: "User@domain-name.net"
        description: "User principal name of LDAP user"
      email:
        type: "string"
        example: "User@domain-name.net"
        description: "User email"
      distinguishedName:
        type: "string"
        example: "CN=USER,DC=domain,DC=net"
        description: "Distinguished name of approver"
      samaccountName:
        type: "string"
        example: "User"
        description: "SAM account name of LDAP user"
    description: "Approver data model"
  RoleBasedAccessGetRolesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      roles:
        type: "array"
        example: "['ADMIN' , 'DEVICE_PROVISIONING'  ,  'SUPPORT'  , 'USER']"
        description: "List of roles"
        items:
          type: "string"
      totalCount:
        type: "integer"
        format: "int32"
        example: 4
        description: "Total count of the roles"
    description: "Role-Based Access Control Response Data Model"
  NotificationRequests:
    type: "object"
    properties:
      smtpNotifRequestId:
        type: "integer"
        format: "int32"
        example: 1
        description: "SMTP notification request id"
      smsNotifRequestId:
        type: "integer"
        format: "int32"
        example: 2
        description: "SMS notification request id"
      smsGatewayNotifRequestId:
        type: "integer"
        format: "int32"
        example: -1
        description: "SMS gateway notification request id"
      apnsAgentNotifRequestId:
        type: "integer"
        format: "int32"
        example: 4
        description: "APNS agent notification request id"
      shtpAgentNotifRequestId:
        type: "integer"
        format: "int32"
        example: 5
        description: "SHTP agent notification request id"
    description: "Device notification request data"
  DeviceActionResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deviceActionMessages:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceActionMessages"
    description: "Response data for device action"
  DomainGroups:
    type: "object"
    properties:
      domain:
        type: "string"
        example: "local"
        description: "Name of the domain"
      groups:
        type: "array"
        example: "['MSP']"
        description: "list of groups"
        items:
          type: "string"
    description: "Domain groups information"
    xml:
      name: "domainGroups"
  LoginResponse:
    type: "object"
    properties:
      auth_token:
        type: "string"
        example: "q483409eu82mkfrcdiv90iv0gc:q483409eu82mkfrcdiv90iv0gc"
        description: "auth token for login"
    description: "Login response data container"
  GenericResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Generic response container, with code and message"
  ShareFileStorageZoneData:
    type: "object"
    required:
    - "userName"
    properties:
      id:
        type: "integer"
        format: "int64"
        example: 1
        description: "Id of sharefile storage zone"
      name:
        type: "string"
        example: "name"
        description: "Name of sharefile storage zone"
      fqdn:
        type: "string"
        example: "subdomain.sharefile.com"
        description: "FQDN of sharefile storage zone"
      port:
        type: "integer"
        format: "int32"
        example: 443
        description: "Port for sharefile storage zone"
      secure:
        type: "boolean"
        example: true
        description: "Sharefile storage zone secure flag"
        default: false
      userName:
        type: "string"
        example: "user"
        description: "User name of sharefile storage zone account"
    description: "Sharefile connector zone data"
  DeviceFilterRequest:
    type: "object"
    required:
    - "filterIds"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Start : Indicates the number of results to be excluded. 0 indicates\
          \ nothing is excluded from the results. Default : 0 (Optional)"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Limit : Indicates the number of results to be retrieved. Default\
          \ : 50 .(Optional)"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "SortOrder : Indicates sort order of the results. Default : ASC\
          \ (Optional)"
        enum:
        - "ASC"
        - "DESC"
      sortColumn:
        type: "string"
        example: "ID"
        description: "SortColumn : Indicates parameter on which the results need to\
          \ be sorted. Default : ID (Optional)"
      search:
        type: "string"
        example: "Any search term"
        description: "Search : Filters the results based on the search term (Optional)"
      enableCount:
        type: "boolean"
        example: false
        description: "EnableCount : Returns the total records, matched records, start,\
          \ limit with the results. Default : true (Optional)"
        default: false
      filterIds:
        type: "string"
        example: "['group#/group/ActiveDirectory/domain/net/Domain Users@_fn_@normal']"
        description: "Filter ID(s) string of the saved filters (Optional). The available\
          \ filters are obtained as part of the result. Alternatively, invoking the\
          \ getAvailable filters API would also return the list of available filters"
    description: "Model for capturing the device filter request"
  DeliveryGroupModel:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "dgDomainUsers"
        description: "Delivery group name"
      description:
        type: "string"
        example: "Delivery group for domain users"
        description: "Delivery group description"
      zoneId:
        type: "integer"
        format: "int64"
        example: 0
        description: "Sharefile zone id"
      zoneDomain:
        type: "string"
        example: "domain"
        description: "Sharefile zone domain"
      rules:
        type: "string"
        example: "{'AND':[{'values':{'stringOperator':'eq','value':'domain'},'ruleId':'001-restrictUserPropDomainName'}]}"
        description: "Associated deployment rules"
      disabled:
        type: "boolean"
        example: false
        description: "Is disabled delivery group"
        default: false
      lastUpdated:
        type: "string"
        format: "date-time"
        example: "2015-09-30T16:33:19.748-07:00"
        description: "Last update date of delivery group"
      anonymousUser:
        type: "boolean"
        example: false
        description: "Is anonymous deployment"
        default: false
      cwcManaged:
        type: "boolean"
        example: false
        description: "Is the delivery group managed by CWC"
        default: false
      roleDefinitionCount:
        type: "integer"
        format: "int32"
        example: 0
        description: "Count of associated users and groups"
      version:
        type: "integer"
        format: "int32"
        example: 2
        description: "Delivery group definition version"
      applications:
        type: "array"
        description: "List of applications"
        items:
          $ref: "#/definitions/DGApplication"
      media:
        type: "array"
        description: "List of media"
        items:
          $ref: "#/definitions/DGMedium"
      devicePolicies:
        type: "array"
        description: "List of device policies"
        items:
          $ref: "#/definitions/DGResource"
      smartActions:
        type: "array"
        description: "List of smart actions"
        items:
          $ref: "#/definitions/DGResource"
      connectors:
        type: "array"
        description: "List of sharefile connectors"
        items:
          $ref: "#/definitions/DGConnector"
      nbSuccess:
        type: "integer"
        format: "int32"
        example: 0
        description: "Count of successful deployments"
      nbFailure:
        type: "integer"
        format: "int32"
        example: 0
        description: "Count of failed deployments"
      nbPending:
        type: "integer"
        format: "int32"
        example: 0
        description: "Count of pending deployments"
      groups:
        type: "array"
        description: "List of user groups"
        items:
          $ref: "#/definitions/CPGroup"
      users:
        type: "array"
        description: "List of users"
        items:
          $ref: "#/definitions/DeliveryGroupUser"
      enrollmentProfileId:
        type: "integer"
        format: "int64"
      enrollmentProfileName:
        type: "string"
        example: "Global"
        description: "Name of enrollment profile"
    description: "Model containing information of delivery group"
  CurrentFilter:
    type: "object"
    properties:
      detail:
        type: "array"
        xml:
          name: "filters"
        description: "Filter node list"
        items:
          $ref: "#/definitions/FilterNode"
      selectedFilters:
        type: "array"
        example: "['filter1.name', 'filter2.name']"
        description: "Selected filters list"
        items:
          type: "string"
    description: "Enrollment current filter data"
    xml:
      name: "currentFilter"
  DevicesActionParameters:
    type: "object"
    properties:
      messageList:
        type: "array"
        description: "Device action parameters message"
        items:
          $ref: "#/definitions/DeviceActionParameters"
      description:
        type: "string"
        example: "Action failure"
        description: "Device action parameter description"
    description: "Devices action parameters message model"
  NotificationTemplate:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 5
        description: "Id of notification template"
      agent:
        type: "boolean"
        example: false
        description: "A flag to determine if template includes agent notification"
        default: false
      automatic:
        type: "boolean"
        example: false
        description: "A flag to determine if template should send automatic"
        default: false
      description:
        type: "string"
        example: "null"
        description: "Description of notification template"
      name:
        type: "string"
        example: "Enrollment Invitation"
        description: "Name of notification template"
      eventType:
        type: "string"
        example: "ZDM_NOTIFICATION_ENROLLMENT_INVITATION"
        description: "Event type for notification template"
      sms:
        type: "boolean"
        example: false
        description: "A flag to determine if template includes sms notification"
        default: false
      smtp:
        type: "boolean"
        example: false
        description: "A flag to determine if template includes smtp notification"
        default: false
      systemNoDelete:
        type: "boolean"
        example: false
        description: "A flag to determine if templete is not deleteable"
        default: false
      classifications:
        type: "string"
        example: "null"
        description: "Notification template classifications"
      msg:
        type: "array"
        description: "List of messages for the notification template, each for different\
          \ notification channel"
        items:
          $ref: "#/definitions/NotificationTemplateMsg"
    description: "Notification template data model"
    xml:
      name: "notificationTemplate"
  ConnectorResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      connector:
        xml:
          name: "result"
        $ref: "#/definitions/Connector"
    description: "Connectors response data"
  Connector:
    type: "object"
    properties:
      singleInstanceOnly:
        type: "boolean"
        example: false
        description: "Single instance connector"
        default: false
      iconPath:
        type: "string"
        example: "Salesforce_SAML_SP"
        description: "Connector icon path"
      description:
        type: "string"
        example: "description"
        description: "Connector description"
      ssoStoreData:
        $ref: "#/definitions/SSOStore"
      connectorType:
        type: "integer"
        format: "int32"
        example: 1
        description: "Connector type"
      provisioningSupported:
        type: "boolean"
        example: true
        description: "Connector provisioning supported"
        default: false
      name:
        type: "string"
        example: "Salesforce_SAML_SP"
        description: "Connector name"
      ssoSupported:
        type: "boolean"
        example: true
        description: "Connector SSO supported"
        default: false
    description: "Model for storing connector data"
  DeviceFilterNode:
    type: "object"
    properties:
      nodes:
        type: "array"
        description: "child filter nodes"
        items:
          $ref: "#/definitions/DeviceFilterNode"
      checked:
        type: "boolean"
        example: true
        description: "A flag to determine the filter check"
        default: false
      leafNode:
        type: "boolean"
        example: true
        description: "A flag to determine the leaf node"
        default: false
      name:
        type: "string"
        example: "group#/group/ActiveDirectory"
        description: "Name of device filter"
      value:
        type: "integer"
        format: "int64"
        example: -1
        description: "Value of device filter"
      displayName:
        type: "string"
        example: "Active Directory"
        description: "Display name of device filter"
      level:
        type: "integer"
        format: "int32"
        example: 0
        description: "Level of device filter"
    description: "Filter node for devices"
  RoleBasedAccessGetRoleDefResponse:
    type: "object"
    required:
    - "name"
    - "permissions"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      permissions:
        type: "array"
        description: "List of permissions included in this role"
        items:
          $ref: "#/definitions/RolePermission"
      name:
        type: "string"
        example: "DEVICE_PROVISIONING"
        description: "Name of the role"
      adGroups:
        type: "array"
        description: "List of active directory groups associated with this role"
        items:
          $ref: "#/definitions/AdGroup"
    description: "Role-Based Access Get Role Definition Response Model"
  Rating:
    type: "object"
    required:
    - "rating"
    - "reviewerCount"
    properties:
      rating:
        type: "number"
        format: "double"
        example: 4.5
        description: "Collective average rating of application"
      reviewerCount:
        type: "integer"
        format: "int64"
        example: 10
        description: "Number of reviewers"
  ExceptionContainer:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      errorCode:
        type: "string"
        example: "Consists of a number between 1000 and 9999"
        description: "The error code for the failure"
      errorMessage:
        type: "string"
        example: "Consists of the description of the error"
        description: "The error message for the failure"
    description: "Consists of the error code and the error message"
  EnrollFilter:
    type: "object"
    properties:
      currentFilter:
        $ref: "#/definitions/CurrentFilter"
      enrollmentList:
        $ref: "#/definitions/Enrollments"
    description: "Enrollment filter data"
    xml:
      name: "enrollFilter"
  AdGroup:
    type: "object"
    required:
    - "domainName"
    - "uniqueName"
    properties:
      primaryGroupToken:
        type: "integer"
        format: "int32"
        example: 545
        description: "Primary token of the group"
      uniqueName:
        type: "string"
        example: "Users"
        description: "Unique name of the group"
      domainName:
        type: "string"
        example: "agsag.com"
        description: "Domain name of the group"
  MobileAppPlatformData:
    type: "object"
    required:
    - "appType"
    - "appVersion"
    - "associateToDevice"
    - "canAssociateToDevice"
    - "changeManagementState"
    - "description"
    - "displayName"
    - "excludedDevices"
    - "id"
    - "maxOsVersion"
    - "minOsVersion"
    - "paid"
    - "preventBackup"
    - "removeWithMdm"
    - "rules"
    - "store"
    - "uuid"
    properties:
      displayName:
        type: "string"
        example: "WorxNotes"
        description: "Display name of application"
      description:
        type: "string"
        example: "description"
        description: "Description of application"
      paid:
        type: "boolean"
        example: false
        description: "Identifies whether application is paid or free"
        default: false
      removeWithMdm:
        type: "boolean"
        example: true
        description: "Remove application when MDM profile is uninstalled"
        default: false
      preventBackup:
        type: "boolean"
        example: true
        description: "Prevent application backup data"
        default: false
      changeManagementState:
        type: "boolean"
        example: true
        description: "Automatically manage installed application"
        default: false
      associateToDevice:
        type: "boolean"
        example: true
        description: "Device license association"
        default: false
      canAssociateToDevice:
        type: "boolean"
        example: true
        description: "Identifies whether \"Device license association\" is available\
          \ or not"
        default: false
      appVersion:
        type: "string"
        example: "5.2.0"
        description: "Application version"
      minOsVersion:
        type: "string"
        example: "3.5"
        description: "Minimum device OS version supported"
      maxOsVersion:
        type: "string"
        example: "9.0"
        description: "Maximum device OS version supported"
      excludedDevices:
        type: "string"
        example: "iPad Pro, Samsung Galaxy S"
        description: "List of excluded devices"
      store:
        $ref: "#/definitions/Store"
      policies:
        type: "array"
        description: "List of MDX policies"
        items:
          $ref: "#/definitions/MDXPolicy"
      avppParams:
        $ref: "#/definitions/AVPPParams"
      avppTokenParams:
        $ref: "#/definitions/AVPPTokenParams"
      rules:
        type: "string"
        example: "{\"AND\":[{\"values\":{\"withOrWithout\":\"eq\",\"devices\":\"iPhone\"\
          },\"ruleId\":\"000-restrictDeviceIph\"}]}"
        description: "Deployment rules for application"
      appType:
        type: "string"
        example: "mobile_ios"
        description: "Type of application. Possible values are:<br/>\"mobile_ios\"\
          \ for \"iOS App\"<br/>\"mobile_android\" for \"Android App\"<br/>\"mobile_android_knox\"\
          \ for \"Android KNOX App\"<br/>\"mobile_android_work\" for \"Android Work\
          \ App\"<br/>\"mobile_windows\" for \"Windows App\"<br/>\"mobile_windows8\"\
          \ for \"Windows Tablet App\"<br/>\"mobile_windows_ce\" for \"Windows CE\
          \ App\"<br/>\"web_link\" for \"Web Link\"<br/>\"sas\" for \"Web & SaaS App\"\
          <br/>\"fmd\" for \"ShareFile\"<br/>\"sas_ent\" for \"Enterprise SaaS App\"\
          <br/>\"mobile_link\" for \"App Store App\""
      uuid:
        type: "string"
        example: "de305d54-75b4-431b-adb2-eb6b9e546014"
        description: "Application UUID"
      id:
        type: "integer"
        format: "int32"
        example: 2
        description: "Application Id"
    description: "Mobile application platform response data"
  NotificationTemplatesCategory:
    type: "object"
    properties:
      category:
        type: "string"
        example: "ENROLLMENT_URL"
        description: "Category for enrollment template"
        enum:
        - "ENROLLMENT_AGENT"
        - "ENROLLMENT_URL"
        - "ENROLLMENT_PIN"
        - "ENROLLMENT_CONFIRMATION"
      notificationTemplate:
        type: "array"
        description: "notification template list for category"
        items:
          $ref: "#/definitions/NotificationTemplate"
    description: "Model for notification template category"
    xml:
      name: "notificationtemplatesCategory"
  AppResourceDeployState:
    type: "object"
    properties:
      resourceKey:
        type: "string"
        example: "MobileApp2"
        description: "Get the Resource key"
      resourceType:
        type: "string"
        example: "APP_MDMWEBLINK"
        description: "Resource type of policy "
        enum:
        - "APP_NATIVE"
        - "APP_MDMWEBLINK"
        - "APP_MDX"
        - "APP_WEBLINK"
        - "APP_SAAS"
        - "APP_FMD"
        - "TUNNEL"
        - "REGISTRY"
        - "SERVERGROUP"
        - "SOFTWARE_INVENTORY"
        - "SIGNING_CERTIFICATE"
        - "ENTERPRISE_HUB"
        - "CUSTOM_XML"
        - "DEVICE_HEALTH_ATTESTATION"
        - "FILE"
        - "WIFI"
        - "PROXY"
        - "CERTIFICATE"
        - "EMAIL"
        - "EXCHANGE"
        - "PASSWORD"
        - "VPN"
        - "HUB"
        - "SCHEDULING"
        - "RESTRICTIONS"
        - "LOCATIONSERVICES"
        - "APN"
        - "APPLOCK"
        - "XMOPTIONS"
        - "ROAMING"
        - "MDM_LICENSE_KEY"
        - "SIDELOADINGKEY"
        - "STORAGE"
        - "REMOTE_SUPPORT"
        - "CALENDAR_SUBSCRIPTION"
        - "AIRPLAY"
        - "OS_UPDATE"
        - "AIRPRINT"
        - "SSO_ACCOUNT"
        - "CELLULAR"
        - "PERSONAL_HOTSPOT"
        - "SCEP"
        - "WEB_CONTENT_FILTER"
        - "LDAP"
        - "CALDAV_ACCOUNT"
        - "CARDDAV_ACCOUNT"
        - "FONT"
        - "CREDENTIAL"
        - "MANAGED_DOMAINS"
        - "APP_RESTRICTIONS"
        - "MDM_OPTIONS"
        - "ORGANIZATION_INFO"
        - "BROWSER_OPTIONS"
        - "XEN_MOBILE_UNINSTALL"
        - "APP_ATTRIBUTES"
        - "APP_UNINSTALL_RESTRICTIONS"
        - "FIREWALL"
        - "APP_CONFIGURATION"
        - "IMPORT_PROFILE"
        - "KIOSK"
        - "APP_ACCESS"
        - "PROFILE_REMOVAL"
        - "TERMS_CONDITIONS"
        - "WORX_STORE"
        - "PROVISIONING"
        - "MDM_WEBLINK"
        - "DELETE_APPLICATION"
        - "SMART_ACTION"
        - "ENROLLMENT"
        - "APP_RESTRICTIONS_ANDROID_WORK"
        - "SEAMS"
        - "PROVISIONING_PROFILE"
        - "PROVISIONING_PROFILE_REMOVAL"
        - "CONNECTION_MANAGER"
        - "DELETE_FOLDER_FILE"
        - "DELETE_REGISTRY_KEY_VALUE"
        - "WINCE_PKI_CERTIFICATE"
        - "WIP"
        - "NETWORK_USAGE"
        - "WALLPAPER"
        - "DEVICE_NAME"
        - "DEFENDER"
        - "LAUNCHER_CONFIGURATION"
        - "HOMESCREEN_LAYOUT"
        - "UNCATEGORIZED"
        - "EDUCATION_CONFIGURATION"
        - "MEDIA_IBOOK"
      resourceTypeLabel:
        type: "string"
        example: "Public App Store"
        description: "Resource Label of policy"
      packageInfo:
        type: "string"
        example: "com.rovio.baba"
        description: "Package information of application"
      name:
        type: "string"
        example: "Angry Bird"
        description: "Resource name of policy"
      lastUpdate:
        type: "integer"
        format: "int64"
        example: 1479921902171
        description: "Last update timestamp"
      statusLabel:
        type: "string"
        example: "Success"
        description: "Installation status label"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Installation status"
        enum:
        - "SUCCESS"
        - "FAILURE"
        - "PENDING"
        - "AVAILABLE"
    description: "Model for app resource deploy state of a device"
  DeviceCoordinatesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deviceCoordinates:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceCoordinates"
    description: "Response data for device GPS Coordinates"
  AVPPParams:
    type: "object"
    required:
    - "avpcRecords"
    - "orderNumber"
    - "productName"
    - "purchasedLicences"
    - "purchaser"
    - "remainingLicences"
    properties:
      productName:
        type: "string"
        example: "WorxNotes"
        description: "VPP application name"
      purchasedLicences:
        type: "integer"
        format: "int32"
        example: 5
        description: "Purchased license count"
      remainingLicences:
        type: "integer"
        format: "int32"
        example: 4
        description: "Remaining license count"
      orderNumber:
        type: "string"
        example: "XXXXXXXXX"
        description: "Order number assigned by App Store"
      purchaser:
        type: "string"
        example: "XYZ"
        description: "VPP purchaser name"
      avpcRecords:
        type: "array"
        description: "List of licenses"
        items:
          $ref: "#/definitions/AVPCRecordParams"
  WebSaasAppProvisionData:
    type: "object"
    properties:
      userAcctNameRule:
        type: "string"
        example: "data"
        description: "User account name rule for webSaas application provisioning"
      deprovisionOperation:
        type: "string"
        example: "disable"
        description: "Deprovision operation for webSaas application provisioning"
      provisionStoreData:
        $ref: "#/definitions/ProvisionStore"
      passwordRule:
        $ref: "#/definitions/PasswordRule"
    description: "Model for storing webSaas application provisioning data"
  DeviceActionsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      actions:
        type: "array"
        description: "List of smart actions deployed on the device"
        items:
          $ref: "#/definitions/ActionResourceDeployState"
    description: "Response data for smart actions associated with the device"
  DevicePoliciesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      policies:
        type: "array"
        description: "List of policies deployed on the device"
        items:
          $ref: "#/definitions/PolicyResourceDeployState"
    description: "Response data for policies associated with the device"
  ClientPropertiesGetResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      allClientProperties:
        type: "array"
        description: "List of client properties"
        items:
          $ref: "#/definitions/ClientPropertiesResponseData"
    description: "Client Properties Response Model"
  ConnectorsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      connectors:
        type: "array"
        xml:
          name: "result"
        description: "List of WebSaas connectors"
        items:
          $ref: "#/definitions/Connector"
    description: "Connectors response data"
  EnrollmentFilterResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      enrollmentFilterResponse:
        $ref: "#/definitions/EnrollFilter"
    description: "Enrollment filter response data"
  NotificationTemplateCategory:
    type: "object"
    properties:
      category:
        type: "string"
        example: "ENROLLMENT_URL"
        description: "Category template for enrollment"
        enum:
        - "ENROLLMENT_AGENT"
        - "ENROLLMENT_URL"
        - "ENROLLMENT_PIN"
        - "ENROLLMENT_CONFIRMATION"
      categoryLabel:
        type: "string"
        example: "Template For Enrollment URL"
        description: "Category label"
      notificationTemplate:
        $ref: "#/definitions/NotificationTemplate"
    description: "Notification template data model"
    xml:
      name: "notificationtemplateCategory"
  EnrollmentUrlResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      enrollmentUrls:
        type: "array"
        example: "['https://10.20.30.40:8443/zdm/su?e=ep-802b9bd5-7eaa-4eb8-aecb-c21a8f9f8080','https://10.20.30.40:8443/zdm/su?e=ep-1ff7e6af-b7b4-4341-89e8-7b098a577205']"
        description: "List of enrollment urls"
        items:
          type: "string"
    description: "Enrollment urls response data"
  AVPCRecordParams:
    type: "object"
    required:
    - "code"
    - "country"
    - "device"
    - "redeemLink"
    - "status"
    - "user"
    properties:
      code:
        type: "string"
        example: "XXXXXX"
        description: "License code"
      status:
        type: "string"
        example: "AVPC_RECORD_STATUS_UNUSED"
        description: "VPP license status. Possible values are:<br/>\"APP_WIZARD_VPP_LICENSE_USED\"\
          \ for \"Used\"<br/>\"AVPC_RECORD_STATUS_UNUSED\" for \"Unused\"<br/>\"AVPC_RECORD_STATUS_REDEEMED\"\
          \ for \"Redeemed\"<br/>\"AVPC_RECORD_STATUS_REDEEMED_3RD_PARTY\" for \"\
          Used by 3rd party\"<br/>\"AVPC_RECORD_STATUS_B2B_CODE_SENT\" for \"Code\
          \ sent by mail or SMS\"<br/>\"AVPC_RECORD_STATUS_RESERVED\" for \"Pending\"\
          <br/>\"AVPC_RECORD_STATUS_INVALID_CODE\" for \"Invalid\""
      redeemLink:
        type: "string"
        example: "https://phobos.apple.com/WebObjects/MZFinance.woa/wa/freeProductCodeWizard?code=XXXXXXXXXXXXXXXXXXXXXXXXX"
        description: "Redeemed link for license"
      country:
        type: "string"
        example: "Default"
        description: "Country of VPP license"
      device:
        type: "string"
        example: "SERIAL-C007-1-1111"
        description: "Device serial associated with VPP license"
      user:
        type: "string"
        example: "user"
        description: "User name associated with VPP license"
  GetDgResponseDataModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      dgListData:
        $ref: "#/definitions/DeliveryGroupListDataModel"
    description: "Model for delivery group response data"
  CPGroup:
    type: "object"
    required:
    - "name"
    properties:
      id:
        type: "integer"
        format: "int64"
        example: 1
        description: "Id of the group"
      userListId:
        type: "integer"
        format: "int64"
        example: 1
        description: "userListId"
      name:
        type: "string"
        example: "MSP"
        description: "Group name"
      uniqueName:
        type: "string"
        example: "MSP"
        xml:
          name: "uniquename"
        description: "Unique name of user group"
      uniqueId:
        type: "string"
        example: "MSP"
        description: "Unique id of user group"
      domainName:
        type: "string"
        example: "local"
        xml:
          name: "domainname"
        description: "Domain name of user group"
      primaryToken:
        type: "integer"
        format: "int32"
        example: 0
        xml:
          name: "primaryGroupToken"
        description: "Primary token of user group"
      objectSid:
        type: "string"
        example: "0"
        description: "Object Sid of user group"
      customProperties:
        type: "object"
        description: "Custom properties of user group"
        additionalProperties:
          type: "string"
  ShareFileStorageZoneResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      shareFileStorageZone:
        $ref: "#/definitions/ShareFileStorageZoneData"
    description: "Response data for sharefile storage zone"
  Faq:
    type: "object"
    required:
    - "answer"
    - "displayOrder"
    - "question"
    properties:
      question:
        type: "string"
        example: "Question?"
        description: "Question"
      answer:
        type: "string"
        example: "Answer"
        description: "Answer"
      displayOrder:
        type: "integer"
        format: "int32"
        example: 1
        description: "Display order"
  PublicStoreAppData:
    type: "object"
    required:
    - "storeUrl"
    properties:
      storeUrl:
        type: "string"
        example: "https://itunes.apple.com/us/app/gotomeeting-previous-version/id424104128"
        description: "Application Store URL. This is required while adding app. In\
          \ case of update this parameters gets ignored"
      removeWithMdm:
        type: "boolean"
        example: true
        description: "Remove application when MDM profile is uninstalled"
        default: false
      preventBackup:
        type: "boolean"
        example: true
        description: "Prevent application backup data"
        default: false
      changeManagementState:
        type: "boolean"
        example: true
        description: "Automatically manage installed application"
        default: false
      displayName:
        type: "string"
        example: "WorxNotes"
        description: "Display name of application"
      description:
        type: "string"
        example: "description"
        description: "Application description"
      faqs:
        type: "array"
        description: "List of frequently asked questions to be displayed on SecureHub\
          \ store"
        items:
          $ref: "#/definitions/Faq"
      storeSettings:
        $ref: "#/definitions/StoreSettings"
      checkForUpdate:
        type: "boolean"
        default: false
    description: "Public store application data"
  DevicesPropertyParameters:
    type: "object"
    required:
    - "id"
    properties:
      b64:
        type: "boolean"
        example: false
        description: "A flag to determine if the value of property is base 64 encoded"
        default: false
      name:
        type: "string"
        example: "SYSTEM_OS_VERSION"
        description: "Name of device property"
      value:
        type: "string"
        example: "9.2"
        description: "Property value"
      id:
        type: "integer"
        format: "int32"
        example: 58
        description: "Database Id for device property"
      displayName:
        type: "string"
        example: "Operating system version"
        description: "Display name of device property"
      group:
        type: "string"
        example: "System information"
        description: "Group of the property"
    description: "Devices property parameters"
  DeviceFilterResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      currentFilter:
        $ref: "#/definitions/DeviceCurrentFilter"
      filteredDevicesDataList:
        type: "array"
        description: "List of filtered devices"
        items:
          $ref: "#/definitions/FilteredDevicesData"
      totalCount:
        type: "integer"
        format: "int32"
        example: 50
        description: "Total record count"
      matchedRecords:
        type: "integer"
        format: "int32"
        example: 10
        description: "Matched records count"
    description: "Response data for devices filters"
  ClientPropertiesResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Client Properties Response Model"
  DeviceUsedPropertiesList:
    type: "object"
    properties:
      deviceUsedProperties:
        xml:
          name: "usedProperties"
        $ref: "#/definitions/DeviceUsedProperties"
    description: "Device used properties list data model"
  PolicyEnumValueModel:
    type: "object"
    properties:
      policyEnumValueId:
        type: "string"
        example: "UntilFirstUnlock"
        description: "Policy enum id"
      policyEnumValueString:
        $ref: "#/definitions/MobileAppPolicyStringModel"
    description: "Model for policy enum value"
  DGConnector:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "resName"
        description: "Resource name"
      priority:
        type: "integer"
        format: "int32"
        example: 0
        description: "Resource priority"
      required:
        type: "boolean"
        example: true
        description: "Is required/optional sharefile connector"
        default: false
  ShareFileEnterpriseData:
    type: "object"
    properties:
      domain:
        type: "string"
        example: "subdomain.sharefile.com"
        description: "Domain of enterprise sharefile connector"
      accountProvisioning:
        type: "boolean"
        example: true
        description: "Account provisioning for enterprise sharefile connector"
        default: false
      userName:
        type: "string"
        example: "test@xyz.com"
        description: "User name for enterprise sharefile connector"
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of enterprise sharefile connector"
      roles:
        type: "array"
        example: "['dg01', 'dg02']"
        description: "List of associated delivery groups with enterprise sharefile\
          \ connector"
        items:
          type: "string"
    description: "Data model for enterprise sharefile configuration"
  RoleDefinitionUpdateRequest:
    type: "object"
    required:
    - "permissions"
    properties:
      adGroups:
        type: "array"
        description: "List of active directory groups associated with this role"
        items:
          $ref: "#/definitions/AdGroup"
      permissions:
        type: "array"
        description: "List of permissions included in this role"
        items:
          $ref: "#/definitions/RolePermission"
  ListResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      list:
        type: "array"
        xml:
          name: "result"
          wrapped: true
        description: "List of all the SMS and SMTP servers"
        items:
          type: "object"
          properties: {}
      details:
        type: "object"
        xml:
          name: "result"
          wrapped: true
        description: "Details of server"
        properties: {}
    description: "Notification Servers List Response Data"
  MobileAppPolicy:
    type: "object"
    required:
    - "category"
    - "description"
    - "explanation"
    - "policyCategory"
    - "policyName"
    - "policyType"
    - "policyValue"
    - "title"
    - "units"
    - "valueModified"
    properties:
      policyName:
        type: "string"
        example: "BlockJailbrokenDevices"
        description: "Mobile application policy name. Possible values are:<br/>\"\
          BlockJailbrokenDevices\", \"WifiOnly\", \"RequireInternalNetwork\" and \"\
          InternalWifiNetworks\""
      policyValue:
        type: "string"
        example: "true"
        description: "Mobile application policy value"
      policyType:
        type: "string"
        example: "string/boolean"
        description: "Data type of policy value"
      policyCategory:
        type: "string"
        example: "Device Security"
        description: "Category of mobile application policy.<br/>It could be \"Network\
          \ Requirement\" or \"Device Security\""
      policyHidden:
        type: "boolean"
        example: false
        description: "Identifies whether policy is hidden"
        default: false
      valueModified:
        type: "boolean"
        example: false
        description: "Indicate if policy value is ever modified by Admin"
        default: false
      enumValue:
        type: "array"
        description: "List of policy enum values"
        items:
          $ref: "#/definitions/PolicyEnumValueModel"
      title:
        $ref: "#/definitions/MobileAppPolicyStringModel"
      description:
        $ref: "#/definitions/MobileAppPolicyStringModel"
      units:
        $ref: "#/definitions/MobileAppPolicyStringModel"
      explanation:
        $ref: "#/definitions/MobileAppPolicyStringModel"
      category:
        $ref: "#/definitions/MobileAppPolicyStringModel"
  MediaResourceDeployState:
    type: "object"
    properties:
      resourceType:
        type: "string"
        example: "MEDIA_IBOOK"
        description: "Resource type of media "
        enum:
        - "APP_NATIVE"
        - "APP_MDMWEBLINK"
        - "APP_MDX"
        - "APP_WEBLINK"
        - "APP_SAAS"
        - "APP_FMD"
        - "TUNNEL"
        - "REGISTRY"
        - "SERVERGROUP"
        - "SOFTWARE_INVENTORY"
        - "SIGNING_CERTIFICATE"
        - "ENTERPRISE_HUB"
        - "CUSTOM_XML"
        - "DEVICE_HEALTH_ATTESTATION"
        - "FILE"
        - "WIFI"
        - "PROXY"
        - "CERTIFICATE"
        - "EMAIL"
        - "EXCHANGE"
        - "PASSWORD"
        - "VPN"
        - "HUB"
        - "SCHEDULING"
        - "RESTRICTIONS"
        - "LOCATIONSERVICES"
        - "APN"
        - "APPLOCK"
        - "XMOPTIONS"
        - "ROAMING"
        - "MDM_LICENSE_KEY"
        - "SIDELOADINGKEY"
        - "STORAGE"
        - "REMOTE_SUPPORT"
        - "CALENDAR_SUBSCRIPTION"
        - "AIRPLAY"
        - "OS_UPDATE"
        - "AIRPRINT"
        - "SSO_ACCOUNT"
        - "CELLULAR"
        - "PERSONAL_HOTSPOT"
        - "SCEP"
        - "WEB_CONTENT_FILTER"
        - "LDAP"
        - "CALDAV_ACCOUNT"
        - "CARDDAV_ACCOUNT"
        - "FONT"
        - "CREDENTIAL"
        - "MANAGED_DOMAINS"
        - "APP_RESTRICTIONS"
        - "MDM_OPTIONS"
        - "ORGANIZATION_INFO"
        - "BROWSER_OPTIONS"
        - "XEN_MOBILE_UNINSTALL"
        - "APP_ATTRIBUTES"
        - "APP_UNINSTALL_RESTRICTIONS"
        - "FIREWALL"
        - "APP_CONFIGURATION"
        - "IMPORT_PROFILE"
        - "KIOSK"
        - "APP_ACCESS"
        - "PROFILE_REMOVAL"
        - "TERMS_CONDITIONS"
        - "WORX_STORE"
        - "PROVISIONING"
        - "MDM_WEBLINK"
        - "DELETE_APPLICATION"
        - "SMART_ACTION"
        - "ENROLLMENT"
        - "APP_RESTRICTIONS_ANDROID_WORK"
        - "SEAMS"
        - "PROVISIONING_PROFILE"
        - "PROVISIONING_PROFILE_REMOVAL"
        - "CONNECTION_MANAGER"
        - "DELETE_FOLDER_FILE"
        - "DELETE_REGISTRY_KEY_VALUE"
        - "WINCE_PKI_CERTIFICATE"
        - "WIP"
        - "NETWORK_USAGE"
        - "WALLPAPER"
        - "DEVICE_NAME"
        - "DEFENDER"
        - "LAUNCHER_CONFIGURATION"
        - "HOMESCREEN_LAYOUT"
        - "UNCATEGORIZED"
        - "EDUCATION_CONFIGURATION"
        - "MEDIA_IBOOK"
      resourceTypeLabel:
        type: "string"
        example: "Apple iBook"
        description: "Resource Label of media"
      name:
        type: "string"
        example: "Science Fiction Stories"
        description: "Resource name of media"
      packageInfo:
        type: "string"
        example: "null"
        description: "Package information of application"
      resourceKey:
        type: "string"
        example: "null"
        description: "Resource key of application"
      lastUpdate:
        type: "integer"
        format: "int64"
        example: 1479921902171
        description: "Last update timestamp"
      statusLabel:
        type: "string"
        example: "Success"
        description: "Installation status label"
      status:
        type: "string"
        example: "SUCCESS"
        description: "Installation status"
        enum:
        - "SUCCESS"
        - "FAILURE"
        - "PENDING"
        - "AVAILABLE"
    description: "Model for media resource deploy state of a device"
  DeviceNotifyRequest:
    type: "object"
    required:
    - "agent"
    - "sms"
    - "smtp"
    - "smtpMessage"
    - "to"
    properties:
      smtpFrom:
        type: "string"
        example: "Test"
        description: "From name for SMTP notification to be sent as from in Email,\
          \ Required for SMTP notification"
      to:
        type: "array"
        description: "List of recipients(smsTo, email, token, serial Number)"
        items:
          $ref: "#/definitions/NotifyRecipientData"
      smtpSubject:
        type: "string"
        example: "this is test subject"
        description: "Notification subject for Email, required for SMTP notification"
      smtpMessage:
        type: "string"
        example: "this is test message"
        description: "Notification message to be sent as Email, required for SMTP\
          \ notification"
      smsMessage:
        type: "string"
        example: "this is test message"
        description: "Notification message to be sent as SMS, required for SMS notification,\
          \ if longer than 160 characters multiple messages are delivered to device"
      agentMessage:
        type: "string"
        example: "this is test message"
        description: "Notification message for agent, required for agent notification"
      sendAsBCC:
        type: "string"
        example: "true"
        description: "Do not disclose recipients, put recipient list in BCC field.\
          \ Default is the To field"
      smtp:
        type: "boolean"
        example: true
        description: "A flag for indicating that notification should be sent via SMTP\
          \ or not"
        default: false
      sms:
        type: "boolean"
        example: true
        description: "A flag for indicating that notification should be sent via sms\
          \ or not"
        default: false
      agent:
        type: "boolean"
        example: true
        description: "A flag for indicating that notification should be sent to agent\
          \ or not"
        default: false
      templateId:
        type: "integer"
        format: "int32"
        example: -1
        description: "Notification template ID"
      agentCustomProps:
        $ref: "#/definitions/NotifyAgentCustomProperties"
    description: "Model for capturing the device notify request"
  RoleBasedAccessTreeChildren:
    type: "object"
    properties:
      text:
        type: "string"
        example: "Dashboard"
        description: "Text of the node of role definition tree"
      id:
        type: "string"
        example: "perm-feature-DASHBOARD-"
        description: "Id of the node of role definition tree"
      leaf:
        type: "boolean"
        example: false
        description: "Flag to indicate if this node is a leaf node in permission tree"
        default: false
      children:
        type: "array"
        description: "children of the node in the permission tree"
        items:
          $ref: "#/definitions/RoleBasedAccessTreeChildren"
    description: "Role Based Access Tree Children Model"
  DeviceMdmStatusResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deviceMdmStatus:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceMdmStatus"
    description: "Model for storing the response message and status"
  DeviceCertificate:
    type: "object"
    properties:
      credentialProviderId:
        type: "string"
        example: "11"
        description: "Credential provider Id"
      revoked:
        type: "boolean"
        example: false
        description: "A flag to determine certificate is revoked"
        default: false
      startDate:
        type: "integer"
        format: "int64"
        example: 1479832127000
        description: "Certificate start date"
      endDate:
        type: "integer"
        format: "int64"
        example: 1542990527000
        description: "Certificate end date"
      issuerName:
        type: "string"
        example: "CN=Devices Certificate Authority"
        description: "Certificate issuer name"
      daysToExpire:
        type: "integer"
        format: "int32"
        example: 729
        description: "Number of days to expire certificate"
      certificateNumber:
        type: "string"
        example: "12"
        description: "Certificate number"
      type:
        type: "string"
        example: "iOS agent"
        description: "Type of the certificate"
    description: "Certificate for the authentication of the device"
  DeviceMdmStatusParameters:
    type: "object"
    properties:
      pushState:
        type: "string"
        example: "INACTIVE"
        description: "Push state"
        enum:
        - "ENQUEUED"
        - "PENDING"
        - "ACTIVE"
        - "INACTIVE"
      lastPushDate:
        type: "integer"
        format: "int64"
        example: 1479992413299
        description: "Last push date"
      lastSentNotification:
        type: "integer"
        format: "int64"
        example: 1479992413308
        description: "Last sent notification date"
      lastRepliedNotification:
        type: "integer"
        format: "int64"
        example: 1479992421250
        description: "Last replied notification date"
      pushStateLabel:
        type: "string"
        example: "Inactive"
        description: "Push state label"
    description: "Device MDM Status parameters model"
  WebApplicationContainerResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      container:
        $ref: "#/definitions/WebApplicationContainer"
    description: "Saas application response data"
  DGMedium:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "resName"
        description: "Resource name"
      priority:
        type: "integer"
        format: "int32"
        example: 0
        description: "Resource priority"
      required:
        type: "boolean"
        example: true
        description: "Is required/optional media"
        default: false
  DevicePropertiesList:
    type: "object"
    properties:
      deviceProperties:
        xml:
          name: "properties"
        $ref: "#/definitions/DeviceProperties"
    description: "Device properties data list model"
  SoftwareInventory:
    type: "object"
    properties:
      packageInfo:
        type: "string"
        example: "com.sharefile.mobile"
        description: "App Id of the application"
      blacklistCompliant:
        type: "boolean"
        example: true
        description: "A flag to indicate if the application is blacklist complaint"
        default: false
      suggestedListCompliant:
        type: "boolean"
        example: true
        description: "A flag to indicate if the application is suggested list complaint"
        default: false
      author:
        type: "string"
        example: "com.sharefile"
        description: "Author of application"
      installTimeStamp:
        type: "integer"
        format: "int64"
        example: 1479993483807
        description: "Application installation timestamp"
      installCount:
        type: "integer"
        format: "int32"
        example: -1
        description: "Installation count for application"
      version:
        type: "string"
        example: "764"
        description: "Version of the application"
      container:
        type: "integer"
        format: "int32"
        example: 1
        description: "Container Id for application. For managed apps the value would\
          \ be app container Id. For user apps value would be -1"
      name:
        type: "string"
        example: "ShareFile"
        description: "Name of the application"
      size:
        type: "integer"
        format: "int64"
        example: 56303616
        description: "Application size in bytes"
    description: "Device software inventory data model"
  RoleNameResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      roleName:
        type: "string"
        example: "dg01"
        xml:
          name: "name"
        description: "Role name"
    description: "Role name response"
  EnrollmentCreateRequest:
    type: "object"
    required:
    - "carrier"
    - "deviceBindingData"
    - "deviceBindingType"
    - "deviceOwnership"
    - "domainName"
    - "groupName"
    - "mode"
    - "notificationTemplateCategories"
    - "notifyNow"
    - "phoneNumber"
    - "platform"
    - "userName"
    properties:
      platform:
        type: "string"
        example: "iOS"
        description: "Device platform"
        enum:
        - "iOS"
        - "MACOSX"
        - "SHTP"
        - "WINPHONE"
      deviceOwnership:
        type: "string"
        example: "CORPORATE"
        description: "Device ownership"
        enum:
        - "NO_BINDING"
        - "CORPORATE"
        - "BYOD"
      mode:
        $ref: "#/definitions/EnrollmentModeData"
      userName:
        type: "string"
        example: "user"
        description: "Username to bind the enrollment invitation with"
      domainName:
        type: "string"
        example: "domain"
        description: "Domain name to bind the enrollment invitation with"
      groupName:
        type: "string"
        example: "group"
        description: "Group name to bind the enrollment invitation with"
      notificationTemplateCategories:
        type: "array"
        description: "List of notification template categories"
        items:
          $ref: "#/definitions/EnrollmentNotificationTemplateCategory"
      phoneNumber:
        type: "string"
        example: "+1 (111) 111-1111"
        description: "Phone number of the user"
      carrier:
        type: "string"
        example: "AllTel"
        description: "Carrier network name of user device"
      deviceBindingType:
        type: "string"
        example: "SERIALNUMBER"
        description: "Device binding type. Value can be SERIALNUMBER, UDID, IMEI"
        enum:
        - "UDID"
        - "SERIALNUMBER"
        - "IMEI"
      deviceBindingData:
        type: "string"
        example: "987654321"
        description: "Device binding data for the selected binding type"
      notifyNow:
        type: "boolean"
        example: true
        description: "Notify user of enrollment invitation"
        default: false
    description: "Model for creating enrollment invitation"
  StoreSettings:
    type: "object"
    required:
    - "rate"
    - "review"
    properties:
      rate:
        type: "boolean"
        example: false
        description: "Identifies whether user can rate application in Worx Store or\
          \ not"
        default: false
      review:
        type: "boolean"
        example: false
        description: "Identifies whether user can write a review for application in\
          \ Worx Store or not"
        default: false
  TouchdownProperty:
    type: "object"
    properties:
      name:
        type: "string"
        example: "Touchdown_Property_Name"
        description: "Name of touch down property"
      value:
        type: "string"
        example: "Touchdown_Property_Value"
        description: "Value of touch down property"
      category:
        type: "string"
        example: "emailPolicies"
        description: "Category of touch down property"
    description: "Touchdown property"
  DeliveryGroupRequestDataModel:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "dgDomainUsers"
        description: "Delivery group name"
      description:
        type: "string"
        example: "Delivery group for domain users"
        description: "Delivery group description"
      groups:
        type: "array"
        description: "List of user groups on which delivery group will be deployed"
        items:
          $ref: "#/definitions/CPGroup"
      users:
        type: "array"
        description: "List of users on which delivery group will be deployed"
        items:
          $ref: "#/definitions/DeliveryGroupUser"
      zoneId:
        type: "integer"
        format: "int64"
        example: 2
        description: "Sharefile zone id"
      zoneDomain:
        type: "string"
        example: "domain"
        description: "Sharefile zone domain"
      disabled:
        type: "boolean"
        example: false
        description: "Is disabled delivery group"
        default: false
      anonymousUser:
        type: "boolean"
        example: true
        description: "Is anonymous deployment"
        default: false
      cwcManaged:
        type: "boolean"
        description: "Is the delivery group managed by CWC"
        default: false
      applications:
        type: "array"
        description: "List of applications"
        items:
          $ref: "#/definitions/DGApplication"
      devicePolicies:
        type: "array"
        description: "List of device policies"
        items:
          $ref: "#/definitions/DGResource"
      smartActions:
        type: "array"
        description: "List of smart actions"
        items:
          $ref: "#/definitions/DGResource"
      connectors:
        type: "array"
        description: "List of sharefile connectors"
        items:
          $ref: "#/definitions/DGConnector"
      enrollmentProfileId:
        type: "integer"
        format: "int64"
        description: "ID of the enrollment profile that is associated with this delivery\
          \ group"
      roledefLangVersionId:
        type: "integer"
        format: "int32"
        example: 2
        xml:
          name: "version"
        description: "Delivery group definition version"
    description: "Model for capturing delivery group request information"
  PublicStoreAppPlatformData:
    type: "object"
    required:
    - "appKey"
    - "appType"
    - "appVersion"
    - "associateToDevice"
    - "avppParams"
    - "avppTokenParams"
    - "b2B"
    - "canAssociateToDevice"
    - "canDissociateVPP"
    - "changeManagementState"
    - "displayName"
    - "iconPath"
    - "iconUrl"
    - "id"
    - "name"
    - "paid"
    - "preventBackup"
    - "removeWithMdm"
    - "rules"
    - "store"
    - "storeUrl"
    - "uuid"
    properties:
      name:
        type: "string"
        example: "MobileApp"
        description: "System generated unique application name"
      displayName:
        type: "string"
        example: "WorxNotes"
        description: "Display name of application"
      description:
        type: "string"
        example: "description"
        description: "Application description"
      paid:
        type: "boolean"
        example: true
        description: "Identifies whether application is paid or free"
        default: false
      removeWithMdm:
        type: "boolean"
        example: true
        description: "Remove application when MDM profile is uninstalled"
        default: false
      preventBackup:
        type: "boolean"
        example: true
        description: "Prevent application backup data"
        default: false
      changeManagementState:
        type: "boolean"
        example: true
        description: "Automatically manage installed application"
        default: false
      associateToDevice:
        type: "boolean"
        example: true
        description: "License association to device"
        default: false
      canAssociateToDevice:
        type: "boolean"
        example: true
        description: "Identifies whether \"License association to device\" option\
          \ is available or not"
        default: false
      canDissociateVPP:
        type: "boolean"
        example: true
        description: "Can dissociate VPP license association from device"
        default: false
      appVersion:
        type: "string"
        example: "10.5.4"
        description: "Application version"
      store:
        $ref: "#/definitions/Store"
      avppParams:
        $ref: "#/definitions/AVPPParams"
      avppTokenParams:
        $ref: "#/definitions/AVPPTokenParams"
      rules:
        type: "string"
        example: "{\"AND\":[{\"values\":{\"withOrWithout\":\"eq\",\"devices\":\"iPhone\"\
          },\"ruleId\":\"000-restrictDeviceIph\"}]}"
        description: "Deployment rules for application"
      appType:
        type: "string"
        example: "mobile_ios"
        description: "Type of application. Possible values are:<br/>\"mobile_ios\"\
          \ for \"iOS App\"<br/>\"mobile_android\" for \"Android App\"<br/>\"mobile_android_knox\"\
          \ for \"Android KNOX App\"<br/>\"mobile_android_work\" for \"Android Work\
          \ App\"<br/>\"mobile_windows\" for \"Windows App\"<br/>\"mobile_windows8\"\
          \ for \"Windows Tablet App\"<br/>\"mobile_windows_ce\" for \"Windows CE\
          \ App\"<br/>\"web_link\" for \"Web Link\"<br/>\"sas\" for \"Web & SaaS App\"\
          <br/>\"fmd\" for \"ShareFile\"<br/>\"sas_ent\" for \"Enterprise SaaS App\"\
          <br/>\"mobile_link\" for \"App Store App\""
      uuid:
        type: "string"
        example: "f2bb2b8d-2c7c-4546-83e2-4931cb515be2"
        description: "UUID of application"
      id:
        type: "integer"
        format: "int32"
        example: 2
        description: "Application Id"
      vppAccount:
        type: "integer"
        format: "int32"
        example: 862
        description: "VPP account id"
      iconPath:
        type: "string"
        example: "/9j/4AAQSkZJRg.....ABA2wBDAAYEBQY"
        description: "Application icon data"
      iconUrl:
        type: "string"
        example: "http://is3.mzstatic.com/image/thumb/Purple69/v4/af/d8/34/afd83483-9d32-36f4-6ee7-62d9cc4c95ca/Icon-Production.png/0x0ss-85.jpg"
        description: "Application icon url"
      bundleId:
        type: "string"
        example: "com.test.app"
        description: "Application bundle ID"
      appId:
        type: "string"
        example: "424104128"
        description: "Application ID"
      appKey:
        type: "string"
        example: "VPP App"
        description: "Application key for VPP Apps"
      storeUrl:
        type: "string"
        example: "https://itunes.apple.com/us/app/gotomeeting-previous-version/id424104128"
        description: "Application Store URL"
      b2B:
        type: "boolean"
        example: false
        description: "Identifies whether application is B2B application or not"
        default: false
    description: "Public store application data"
  Application:
    type: "object"
    required:
    - "autoProvisionEnabled"
    - "displayName"
    - "name"
    - "passwordRule"
    - "policies"
    - "provisioningEnabled"
    - "provisioningSupported"
    - "ssoEnabled"
    - "ssoStoreData"
    - "store"
    - "uuid"
    properties:
      name:
        type: "string"
        example: "MobileApp"
        description: "System generated unique application name"
      displayName:
        type: "string"
        example: "WorxNotes"
        description: "Display name of application"
      domainName:
        type: "string"
        example: "domain"
        description: "Domain name of application"
      connectorName:
        type: "string"
        example: "EchoSign_SAML"
        description: "Application connector name"
      deprovisionOperation:
        type: "string"
        example: "IGNORE"
        description: "Deprovision operation for user account when user entitlement\
          \ ends.<br/>Possible operations are IGNORE, DISABLE, DELETE or RESETPASSWORD"
      iconPath:
        type: "string"
        example: "iconPath"
        description: "Application icon path"
      autoProvisionEnabled:
        type: "boolean"
        example: true
        description: "Automatic provisioning is enabled or not"
        default: false
      mblStoreData:
        $ref: "#/definitions/MobileStore"
      provisionStoreData:
        $ref: "#/definitions/ProvisionStore"
      ssoStoreData:
        $ref: "#/definitions/SSOStore"
      userAcctNameRule:
        type: "string"
        example: "$EMAIL"
        description: "User account rule"
      provisioningEnabled:
        type: "boolean"
        example: true
        description: "User account provisioning is enabled or not"
        default: false
      provisioningSupported:
        type: "boolean"
        example: true
        description: "Identifies whether user account provisioning is supported or\
          \ not"
        default: false
      ssoEnabled:
        type: "boolean"
        example: true
        description: "Single sign-on is enabled or not"
        default: false
      passwordRule:
        $ref: "#/definitions/PasswordRule"
      uuid:
        type: "string"
        example: "f2bb2b8d-2c7c-4546-83e2-4931cb515be2"
        description: "UUID of application"
      vpn:
        type: "boolean"
        example: false
        description: "Identifies whether application is hosted in internal network\
          \ or not"
        default: false
      required:
        type: "boolean"
        example: false
        description: "Identifies whether application installation is required or not"
        default: false
      store:
        $ref: "#/definitions/Store"
      policies:
        type: "array"
        description: "List of mobile application policies"
        items:
          $ref: "#/definitions/MobileAppPolicy"
    description: "Model for application data"
  EnrollmentNotificationTemplateCategory:
    type: "object"
    required:
    - "category"
    - "notificationTemplate"
    properties:
      category:
        type: "string"
        example: "ENROLLMENT_URL"
        description: "Category of notification template."
        enum:
        - "ENROLLMENT_AGENT"
        - "ENROLLMENT_URL"
        - "ENROLLMENT_PIN"
        - "ENROLLMENT_CONFIRMATION"
      notificationTemplate:
        $ref: "#/definitions/EnrollmentNotificationTemplate"
    description: "Model for enrollment notification category"
  ClientBrandingResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Client Branding Response Model"
  ShareFileConnectorFetchRequest:
    type: "object"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Indicates the number of results to be excluded from start of\
          \ result set. 0 indicates nothing is excluded from the results. Default:\
          \ 0"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Indicates the number of results to be retrieved. Default: 10"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "Indicates sort order of the results. Default: ASC"
        enum:
        - "ASC"
        - "DESC"
      sortColumn:
        type: "string"
        example: "ID"
        description: "Indicates the column on which sorting will be applied. Default:\
          \ ID"
        enum:
        - "ID"
        - "NAME"
        - "TYPE"
        - "STORAGEZONE"
        - "LOCATION"
      search:
        type: "string"
        example: "search"
        description: "Text to be treated as the search term"
      enableCount:
        type: "boolean"
        example: true
        description: "Enable count for total records, matched records, start and limit.\
          \ Default: true"
        default: false
      filterIds:
        type: "string"
        example: "[\"sharefile_connectors.dg#AllUsers@_fn_@sharefile_connectors.dg.list\"\
          ]"
        description: "List of filter ids. Filters are obtained as part of the result"
    description: "Model for fetching sharefile connector with filters"
  EnrollmentFilterRequest:
    type: "object"
    required:
    - "filterIds"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Indicates the number of results to be excluded. 0 indicates\
          \ nothing is excluded from the results. Default : 0 (Optional)"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Indicates the number of results to be retrieved. Default : 50\
          \ .(Optional)"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "Indicates sort order of the results. Default : ASC (Optional)"
        enum:
        - "ASC"
        - "DESC"
      sortColumn:
        type: "string"
        example: "ID"
        description: "Indicates parameter on which the results need to be sorted.\
          \ Default : ID (Optional)"
      search:
        type: "string"
        example: "Any search term"
        description: "Filters the results based on the search term (Optional)"
      enableCount:
        type: "boolean"
        example: true
        description: "Returns the total records, matched records, start, limit with\
          \ the results. Default : true (Optional)"
        default: false
      filterIds:
        type: "string"
        example: "['group#/group/MSP@_fn_@normal']"
        description: "Filter ID(s) string of the saved filters (Optional). The available\
          \ filters are obtained as part of the result. Alternatively, invoking the\
          \ getAvailable filters API would also return the list of available filters"
    description: "Enrollment filter request data"
  ServerPropertiesResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Server Properties Response Model"
  ShareFileStorageZonesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      shareFileStorageZones:
        type: "array"
        description: "List of sharefile storage zones"
        items:
          $ref: "#/definitions/ShareFileStorageZoneData"
    description: "Response data for sharefile storage zones"
  UserGroupResponse:
    type: "object"
    required:
    - "group"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      group:
        $ref: "#/definitions/UserGroupDto"
    description: "User Group Response Model"
  BaseResponseModel:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      roles:
        type: "array"
        xml:
          name: "result"
        items:
          $ref: "#/definitions/DeliveryGroupModel"
    description: "Model for storing the response message and status"
  LdapRequest:
    type: "object"
    required:
    - "domain"
    - "domainAlias"
    - "globalCatalogPort"
    - "groupBaseDN"
    - "lockoutLimit"
    - "lockoutTime"
    - "password"
    - "port"
    - "primaryHost"
    - "userBaseDN"
    - "userSearchBy"
    - "username"
    properties:
      domain:
        type: "string"
        example: "citrix.net"
        description: "LDAP domain name which should be unique from other configuration"
      userBaseDN:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "User base domain name"
      groupBaseDN:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "Group base domain name"
      password:
        type: "string"
        example: "password"
        description: "Password for LDAP server authentication"
      port:
        type: "integer"
        format: "int32"
        example: 3268
        description: "Port number"
      username:
        type: "string"
        example: "test@citrix.net"
        description: "Username for ldap authentication"
      primaryHost:
        type: "string"
        example: "10.20.30.40"
        description: "Primary server IP address / hostname"
      useSecure:
        type: "boolean"
        example: false
        description: "Flag to indicate if secure connection is used"
        default: false
      globalCatalogPort:
        type: "integer"
        format: "int32"
        example: 3268
        description: "Global Catalog TCP Port"
      secondaryHost:
        type: "string"
        example: " "
        description: "Secondary Host IP address"
      lockoutLimit:
        type: "integer"
        format: "int32"
        example: 0
        description: "XenMobile Lockout Limit"
      userSearchBy:
        type: "string"
        example: "upn"
        description: "User search method. Can be 'upn' or 'samaccountname'"
      gcRootContext:
        type: "string"
        example: "dc=citrix,dc=net"
        description: "Global Catalog Root Context"
      lockoutTime:
        type: "integer"
        format: "int32"
        example: 1
        description: "XenMobile Lockout Time"
      domainAlias:
        type: "string"
        example: "citrix.net"
        description: "Domain name alias"
    description: "LDAP Request Model"
  DeviceActionMessages:
    type: "object"
    properties:
      devicesActionParameters:
        xml:
          name: "messages"
        $ref: "#/definitions/DevicesActionParameters"
    description: "Device action messages model"
  IOSProvisioningProfileInventory:
    type: "object"
    properties:
      uuid:
        type: "string"
        example: "8e69d397-48bb-4f29-a95c-dd7b16665c1c"
        description: "Unique Identifier"
      managed:
        type: "boolean"
        example: false
        description: "A flag to determine profile is managed"
        default: false
      expiryDate:
        type: "integer"
        format: "int64"
        example: 1480579200000
        description: "IOS provisioning profile expiry date"
      name:
        type: "string"
        example: "XenMobile CA"
        description: "IOS provisioning profile name"
    description: "IOS Provisioning Profile Inventory Model"
  ShareFileConnectorResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      shareFileConnector:
        $ref: "#/definitions/ShareFileConnectorData"
    description: "Response data for sharefile connector"
  MobileStore:
    type: "object"
    properties:
      binLocation:
        type: "string"
        example: "/location/App.ext"
        description: "Path of mobile application on server"
      deviceType:
        type: "string"
        example: "iPhone"
        description: "Device type for application"
      osType:
        type: "string"
        example: "application/ios"
        description: "Type of device operating system"
    description: "Mobile store data model"
  AVPPTokenParams:
    type: "object"
    required:
    - "avppTokenRecordParams"
    - "totalLicenses"
    - "vppAccountParams"
    properties:
      vppAccountParams:
        $ref: "#/definitions/VPPAccountParams"
      totalLicenses:
        type: "integer"
        format: "int32"
        example: 5
        description: "Total number of VPP licenses"
      avppTokenRecordParams:
        type: "array"
        description: "List of VPP record parameters"
        items:
          $ref: "#/definitions/AVPPTokenRecordParams"
  UserPropertyRequest:
    type: "object"
    required:
    - "name"
    - "value"
    properties:
      name:
        type: "string"
        example: "PROPERTY_NAME"
        description: "Name: property name"
      value:
        type: "string"
        example: "PROPERTY_VALUE"
        description: "Value: property value"
    description: "Model for capturing the user property add/update request"
  ServerPropertiesFilterData:
    type: "object"
    required:
    - "limit"
    properties:
      start:
        type: "integer"
        format: "int32"
        example: 0
        description: "Start index of result set"
      limit:
        type: "integer"
        format: "int32"
        example: 10
        description: "Number of results to return"
      orderBy:
        type: "string"
        example: "name"
        description: "Column name on which result set needs to be sorted"
      sortOrder:
        type: "string"
        example: "ASC"
        description: "Sort order of result set. Can be ASC or DESC"
      searchStr:
        type: "string"
        example: "search string"
        description: "Generic search term"
    description: "Server Properties Filter Data Model"
  Property:
    type: "object"
    properties:
      b64:
        type: "boolean"
        example: false
        description: "A flag to determine if the value of property is base 64 encoded"
        default: false
      name:
        type: "string"
        example: "PROPERTY_NAME"
        description: "Name of the property"
      value:
        type: "string"
        example: "1"
        description: "Value of the property"
      id:
        type: "integer"
        format: "int32"
        example: 11
        description: "Property ID"
      displayName:
        type: "string"
        example: "Property display name"
        description: "Display name of the property"
      group:
        type: "string"
        example: "Property Group Name"
        description: "Group of the property"
    description: "User Property"
  FilteredDevicesData:
    type: "object"
    required:
    - "activeSyncId"
    - "bluetoothMacAddress"
    - "depRegistered"
    - "deployFailed"
    - "deployPending"
    - "deploySuccess"
    - "deviceModel"
    - "deviceName"
    - "devicePlatform"
    - "deviceType"
    - "gatewayBlocked"
    - "id"
    - "imeiOrMeid"
    - "inactivityDays"
    - "jailBroken"
    - "lastAccess"
    - "mamKnown"
    - "mamRegistered"
    - "managed"
    - "mdmKnown"
    - "osVersion"
    - "platform"
    - "productName"
    - "serialNumber"
    - "shareable"
    - "sharedStatus"
    - "userName"
    - "wifiMacAddress"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 11
        description: "ID of the device"
      jailBroken:
        type: "boolean"
        example: false
        description: "Flag indicating if the device is jailbroken"
        default: false
      managed:
        type: "boolean"
        example: true
        description: "Flag indicating if the device is managed"
        default: false
      gatewayBlocked:
        type: "boolean"
        example: false
        description: "Flag indicating if the device gateway is blocked"
        default: false
      deployFailed:
        type: "integer"
        format: "int32"
        example: 0
        description: "Number of failed deployments"
      deployPending:
        type: "integer"
        format: "int32"
        example: 0
        description: "Number of pending deployments"
      deploySuccess:
        type: "integer"
        format: "int32"
        example: 1
        description: "Number of successful deployments"
      mdmKnown:
        type: "boolean"
        example: true
        description: "Flag indicating if device is in MDM mode"
        default: false
      mamRegistered:
        type: "boolean"
        example: true
        description: "Flag indicating if device is registered in MAM mode"
        default: false
      mamKnown:
        type: "boolean"
        example: true
        description: "Flag indicating if device is in MAM mode"
        default: false
      userName:
        type: "string"
        example: "abc@domain.net \"abc\""
        description: "Username of the last user who accessed this device"
      serialNumber:
        type: "string"
        example: "G7NLCDEQF146"
        description: "Serial number of the device"
      imeiOrMeid:
        type: "string"
        example: "null"
        description: "IMEI or MEID number of the device"
      activeSyncId:
        type: "string"
        example: "HS4ML5821324T11CFEM9D2442S"
        description: "Active sync ID of the device"
      wifiMacAddress:
        type: "string"
        example: "8C:7C:92:66:9B:D4"
        description: "WiFi MAC address of the device"
      bluetoothMacAddress:
        type: "string"
        example: "8C:7C:84:44:A3:D3"
        description: "Bluetooth MAC address of the device"
      devicePlatform:
        type: "string"
        example: "null"
        description: "Device platform"
      osVersion:
        type: "string"
        example: "9.2"
        description: "Operating system version of the device"
      deviceModel:
        type: "string"
        example: "iPad"
        description: "Device model information"
      lastAccess:
        type: "string"
        example: "11/23/16 8:32 AM"
        description: "Timestamp when the device was last accessed"
      inactivityDays:
        type: "string"
        example: "0"
        description: "Number of days device has been inactive"
      shareable:
        type: "boolean"
        example: false
        description: "Flag indicating if the device is shareable"
        default: false
      sharedStatus:
        type: "string"
        example: "INACTIVE"
        description: "Get shareable status of the device"
      depRegistered:
        type: "boolean"
        example: false
        description: "Flag indicating if the device is DEP registered"
        default: false
      deviceName:
        type: "string"
        example: "Dev's iPad"
        description: "Name of the device"
      deviceType:
        type: "string"
        example: "iPad"
        description: "Type of the device"
      productName:
        type: "string"
        example: "iPad2,5"
        description: "Product name"
      platform:
        type: "string"
        example: "iOS"
        description: "Platform of the device"
      properties:
        type: "array"
        description: "Returns list of DeviceProperties containing name and value of\
          \ device property"
        items:
          $ref: "#/definitions/Property"
    description: "Model for collecting get devices by filter response"
  CallbackModel:
    type: "object"
    required:
    - "callbackUrl"
    - "ip"
    properties:
      callbackUrl:
        type: "string"
        example: "http://ag.com"
        description: "Callback URL of the Netscalar gateway"
      ip:
        type: "string"
        example: "10.20.30.40"
        description: "Virtual IP address"
    description: "Model for callback URL for netscalar gateway"
  DevicePropertyResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Device property response Model"
  LogoutData:
    type: "object"
    required:
    - "login"
    properties:
      login:
        type: "string"
        example: "administrator"
        description: "userName"
    description: "Logout request data container"
  NotifyTokenModel:
    type: "object"
    required:
    - "type"
    - "value"
    properties:
      type:
        type: "string"
        example: "apns"
        description: "Type of token"
      value:
        type: "string"
        example: "dfb2fb351a4fb068e40858ecad572e317e6c39b4fa7de6fb29ea1ad7e2254499"
        description: "token value"
    description: "Model for capturing token for agent notification"
  RoleResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      role:
        xml:
          name: "result"
        $ref: "#/definitions/DeliveryGroupModel"
    description: "Role response data"
  IOSProfileInventory:
    type: "object"
    properties:
      managed:
        type: "boolean"
        example: false
        description: "A flag to determine iOS profile is managed"
        default: false
      organization:
        type: "string"
        example: "XenMobile"
        description: "Name of organization"
      identifier:
        type: "string"
        example: "com.zenprise.zdm.ca"
        description: "iOS profile identifier"
      receivedDate:
        type: "integer"
        format: "int64"
        example: 1479993483807
        description: "Received date of iOS profile"
      encrypted:
        type: "boolean"
        example: false
        description: "A flag to determine iOS profile is encrypted"
        default: false
      iosConfigInventories:
        type: "array"
        xml:
          name: "iosConfigInventory"
          wrapped: true
        description: "IOS configuration inventory"
        items:
          $ref: "#/definitions/IOSConfigInventory"
      description:
        type: "string"
        example: "XenMobile Authorities"
        description: "Description of iOS profile"
      name:
        type: "string"
        example: "XenMobile CA"
        description: "Name of iOS profile"
    description: "Simple User Information"
  DeviceKnownProperties:
    type: "object"
    properties:
      knownProperties:
        $ref: "#/definitions/DeviceKnownPropertiesList"
    description: "Device known properties model"
  DeviceCoordinateList:
    type: "object"
    properties:
      deviceCoordinateList:
        type: "array"
        xml:
          name: "gpsCoordinateList"
        description: "device GPS coordinates list"
        items:
          $ref: "#/definitions/DeviceCoordinate"
      startDate:
        type: "integer"
        format: "int64"
        example: 1479975747000
        description: "device GPS coordinate filter start date"
      endDate:
        type: "integer"
        format: "int64"
        example: 1479975749000
        description: "device GPS coordinate filter end date"
    description: "Device coordinates model to locate the device"
  DeviceAppsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      applications:
        type: "array"
        description: "List of apps deployed on the device"
        items:
          $ref: "#/definitions/AppResourceDeployState"
    description: "Response data for apps associated with the device"
  DeviceSoftwareInventoryResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      softwareInventories:
        type: "array"
        description: "Collection of software inventories deployed on the device"
        items:
          $ref: "#/definitions/SoftwareInventory"
    description: "Device software inventories response data"
  NotifyAgentCustomProperties:
    type: "object"
    required:
    - "sound"
    properties:
      sound:
        type: "string"
        example: "Casino.wav"
        description: "Sound for notification for agent"
    description: "Model for capturing agent custom properties for notify"
  LocalUsersResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      users:
        type: "array"
        description: "List of users"
        items:
          $ref: "#/definitions/LocalUser"
    description: "Local Users Response Model"
  PublicStoreAppContainerResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      container:
        $ref: "#/definitions/PublicStoreAppContainer"
    description: "Response object for containing data for public store application"
  NSGRequest:
    type: "object"
    required:
    - "logonType"
    - "name"
    - "passwordRequired"
    - "url"
    properties:
      name:
        type: "string"
        example: "displayName"
        description: "Unique name for the Netscalar gateway configuration"
      alias:
        type: "string"
        example: " "
        description: "NetScalar Gateway alias"
      url:
        type: "string"
        example: "https://externalURl.com"
        description: "Publicly accessible url for netscalar gateway"
      passwordRequired:
        type: "boolean"
        example: false
        description: "Flag to indicate if password is required"
        default: false
      logonType:
        type: "string"
        example: "domain"
        description: "NetScalar Gateway logon type"
      callback:
        type: "array"
        description: "list of callback"
        items:
          $ref: "#/definitions/CallbackModel"
      id:
        type: "string"
        example: " "
        description: "Id for netscalar gateway configuration which can be used for\
          \ editing, deleting and setting a default config"
      default:
        type: "boolean"
        example: false
        description: "Flag to indicate if this configuration is default NSG config.\
          \ Default false"
        default: false
    description: "Netscalar Gateway Request Model"
  FilterNode:
    type: "object"
    properties:
      displayName:
        type: "string"
        example: "Filter Display Name"
        description: "Filter node display name"
      name:
        type: "string"
        example: "filter.name"
        description: "Filter node name"
      value:
        type: "integer"
        format: "int64"
        example: -1
        description: "Filter node value"
      level:
        type: "integer"
        format: "int32"
        example: 1
        description: "Filter node level"
      checked:
        type: "boolean"
        example: false
        description: "A flag to determine filter node is checked"
        default: false
      leafNode:
        type: "boolean"
        example: false
        description: "A flag to determine leaf filter node"
        default: false
      nodes:
        type: "array"
        description: "List of child nodes"
        items:
          $ref: "#/definitions/FilterNode"
    description: "Enrollment filter node data"
    xml:
      name: "node"
  WebSaasAppData:
    type: "object"
    required:
    - "connectorName"
    - "description"
    - "loginUrl"
    - "name"
    properties:
      name:
        type: "string"
        example: "name"
        description: "Name of application"
      description:
        type: "string"
        example: "description"
        description: "Description of application"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['dg01','dg02']"
        description: "List of roles associated with application"
        items:
          type: "string"
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      loginUrl:
        type: "string"
        example: "http://login.url.com"
        description: "Login url of web application"
      vpn:
        type: "boolean"
        example: false
        description: "Is web application on vpn"
        default: false
      faqs:
        type: "array"
        description: "List of frequently asked questions to be displayed on SecureHub\
          \ store"
        items:
          $ref: "#/definitions/Faq"
      storeSettings:
        $ref: "#/definitions/StoreSettings"
      connectorName:
        type: "string"
        example: "Salesforce_SAML"
        description: "Connector name of webSaas application"
      workflowTemplateName:
        type: "string"
        example: "workflow.tpl"
        description: "Workflow template name of webSaas application"
      domainName:
        type: "string"
        example: "domain.net"
        description: "Domain name of webSaas application"
      enterpriseAttrs:
        type: "object"
        example: "{\"AcsUrl\":\"\"}"
        description: "Map of enterprise attributes for webSaas application"
        additionalProperties:
          type: "string"
      provisioningEnabled:
        type: "boolean"
        example: false
        description: "Provisioning enabled for webSaas application"
        default: false
      provisioning:
        $ref: "#/definitions/WebSaasAppProvisionData"
    description: "Model for storing webSaas application data"
  NSGResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      agList:
        type: "array"
        description: "List of all the added netscaler gateway configurations"
        items:
          $ref: "#/definitions/NSGRequest"
    description: "NetScaler Gateway Response Model"
  ShareFileEnterpriseResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      shareFileEnterpriseData:
        $ref: "#/definitions/ShareFileEnterpriseData"
    description: "Response data for enterprise sharefile connector"
  ApplicationContainer:
    type: "object"
    required:
    - "appType"
    - "categories"
    - "createdOn"
    - "description"
    - "disabled"
    - "iconData"
    - "id"
    - "lastUpdated"
    - "name"
    - "permitAsRequired"
    - "roles"
    - "schedule"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of container"
      name:
        type: "string"
        example: "container name"
        description: "Name of container"
      description:
        type: "string"
        example: "description of container"
        description: "Description of container"
      createdOn:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Creation date and time of container"
      lastUpdated:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Last modification date and time of container"
      disabled:
        type: "boolean"
        example: false
        description: "Identifies whether container is disabled or not"
        default: false
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      permitAsRequired:
        type: "boolean"
        example: true
        description: "Mark application container as required or not"
        default: false
      iconData:
        type: "string"
        example: "iVBORw0KGgoAAAANSU...AAAElFTkSuQmCC"
        description: "Icon data of application"
      appType:
        type: "string"
        example: "App Store App"
        description: "Type of application container. Expected types are:<br/>MDX,\
          \ Enterprise, App Store App, Web Link, Web & SaaS"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application container"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['AllUsers']"
        description: "List of delivery groups associated with application container"
        items:
          type: "string"
      workflow:
        $ref: "#/definitions/Workflow"
      vppAccount:
        type: "string"
        example: "name"
        description: "Name of VPP account"
    description: "Model for filtering applications"
  ShareFileConnectorData:
    type: "object"
    properties:
      byPathData:
        type: "string"
        example: "path"
        description: "Path data of sharefile connector"
      name:
        type: "string"
        example: "name"
        description: "Name of sharefile connector"
      description:
        type: "string"
        example: "description"
        description: "Description of sharefile connector"
      type:
        type: "string"
        example: "SharePoint"
        description: "Type of sharefile connector"
      location:
        type: "string"
        example: "location"
        description: "Location of sharefile connector"
      deliveryGroups:
        type: "array"
        example: "['dg01','dg02']"
        description: "List of delivery groups associated with sharefile connector"
        items:
          type: "string"
      createdOn:
        type: "string"
        format: "date-time"
        example: "2016-03-10T16:14:41.143+05:00"
        description: "Creation date of sharefile connector"
      updatedOn:
        type: "string"
        format: "date-time"
        example: "2016-03-10T16:14:41.143+05:00"
        description: "Modified date of sharefile connector"
      storageZoneId:
        type: "string"
        example: "zone01"
        description: "Storage zone id of sharefile connector"
      storageZoneName:
        type: "string"
        example: "zonename"
        description: "Storage zone of sharefile connector"
      containerId:
        type: "integer"
        format: "int32"
        example: 1
        description: "Container id of sharefile connector"
    description: "Sharefile connector data"
  WebAppData:
    type: "object"
    required:
    - "description"
    - "loginUrl"
    - "name"
    properties:
      name:
        type: "string"
        example: "name"
        description: "Name of application"
      description:
        type: "string"
        example: "description"
        description: "Description of application"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['dg01','dg02']"
        description: "List of roles associated with application"
        items:
          type: "string"
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      loginUrl:
        type: "string"
        example: "http://login.url.com"
        description: "Login url of web application"
      vpn:
        type: "boolean"
        example: false
        description: "Is web application on vpn"
        default: false
      faqs:
        type: "array"
        description: "List of frequently asked questions to be displayed on SecureHub\
          \ store"
        items:
          $ref: "#/definitions/Faq"
      storeSettings:
        $ref: "#/definitions/StoreSettings"
    description: "Model for storing web application data"
  DeviceResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      device:
        $ref: "#/definitions/Device"
    description: "Device response data"
  MobileAppPolicyStringModel:
    type: "object"
    properties:
      getpStrResId:
        type: "string"
        example: "STRING_UNTIL_FIRST_UNLOCK"
        description: "Policy resource id"
      getsValue:
        type: "string"
        example: "Until first unlock"
        description: "Policy resource value"
    description: "Model for mobile app policy value"
  MobileAppContainer:
    type: "object"
    required:
    - "appType"
    - "categories"
    - "createdOn"
    - "description"
    - "disabled"
    - "iconData"
    - "id"
    - "lastUpdated"
    - "name"
    - "permitAsRequired"
    - "roles"
    - "schedule"
    properties:
      id:
        type: "integer"
        format: "int32"
        example: 1
        description: "Id of container"
      name:
        type: "string"
        example: "container name"
        description: "Name of container"
      description:
        type: "string"
        example: "description of container"
        description: "Description of container"
      createdOn:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Creation date and time of container"
      lastUpdated:
        type: "string"
        example: "03/14/15 05:44 PM"
        description: "Last modification date and time of container"
      disabled:
        type: "boolean"
        example: false
        description: "Identifies whether container is disabled or not"
        default: false
      schedule:
        $ref: "#/definitions/DeploymentSchedule"
      permitAsRequired:
        type: "boolean"
        example: true
        description: "Mark application container as required or not"
        default: false
      iconData:
        type: "string"
        example: "iVBORw0KGgoAAAANSU...AAAElFTkSuQmCC"
        description: "Icon data of application"
      appType:
        type: "string"
        example: "App Store App"
        description: "Type of application container. Expected types are:<br/>MDX,\
          \ Enterprise, App Store App, Web Link, Web & SaaS"
      categories:
        type: "array"
        example: "['Default']"
        description: "List of categories associated with application container"
        items:
          type: "string"
      roles:
        type: "array"
        example: "['AllUsers']"
        description: "List of delivery groups associated with application container"
        items:
          type: "string"
      workflow:
        $ref: "#/definitions/Workflow"
      vppAccount:
        type: "string"
        example: "name"
        description: "Name of VPP account"
      ios:
        $ref: "#/definitions/MobileAppPlatformData"
      android:
        $ref: "#/definitions/MobileAppPlatformData"
      android_knox:
        $ref: "#/definitions/MobileAppPlatformData"
      android_work:
        $ref: "#/definitions/MobileAppPlatformData"
      windows:
        $ref: "#/definitions/MobileAppPlatformData"
      windows_tab:
        $ref: "#/definitions/MobileAppPlatformData"
    description: "Model for mobile application container data"
  DeviceProperties:
    type: "object"
    properties:
      startIndex:
        type: "integer"
        format: "int32"
        example: 0
        description: "Device start index"
      devicePropertyParameters:
        type: "array"
        xml:
          name: "property"
        description: "Device property parameters"
        items:
          $ref: "#/definitions/DevicesPropertyParameters"
      totalCount:
        type: "integer"
        format: "int32"
        example: 10
        description: "Total count"
    description: "Device properties"
  EnrollmentModeData:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "classic"
        description: "Name of user enrollment mode.<br/>Allowed values are:<br/>\"\
          classic\" for \"User name + Password\"<br/>\"high_security\" for \"High\
          \ Security\"<br/>\"invitation\" for \"Invitation URL\"<br/>\"invitation_pin\"\
          \ for \"Invitation URL + PIN\"<br/>\"invitation_pwd\" for \"Invitation URL\
          \ + Password\"<br/>\"two_factor\" for \"Two Factor\"<br/>\"username_pin\"\
          \ for \"User name + PIN\""
    description: "Model for storing the user enrollment mode request."
  Device:
    type: "object"
    required:
    - "id"
    - "serialNumber"
    properties:
      applications:
        type: "array"
        items:
          $ref: "#/definitions/AppResourceDeployState"
      media:
        type: "array"
        items:
          $ref: "#/definitions/MediaResourceDeployState"
      smartActions:
        type: "array"
        description: "Smart Actions deployed on the device"
        items:
          $ref: "#/definitions/ActionResourceDeployState"
      lastActivity:
        type: "integer"
        format: "int64"
        example: 1479921911405
        description: "Device last activity date"
      imei:
        type: "string"
        example: "351853073566405"
        description: "Device IMEI Number"
      strongId:
        type: "string"
        example: "Q6HIJUFD"
        description: "Strong Id for device"
      lastSoftwareInventoryTime:
        type: "integer"
        format: "int64"
        example: 1479921911108
        description: "Device Last software inventory sync timestamp"
      firstConnectionDate:
        type: "integer"
        format: "int64"
        example: 1479918533653
        description: "Device first time connection date"
      lastAuthDate:
        type: "integer"
        format: "int64"
        example: 1479921911405
        description: "Device last online authentication date"
      lastIOSProfileInventoryTime:
        type: "integer"
        format: "int64"
        example: 1479921911493
        description: "Device Last IOS profile inventory sync timestamp"
      lastUsername:
        type: "string"
        example: "abc@domain.net \"abc\""
        description: "Device last username"
      lastUser:
        $ref: "#/definitions/SimpleUser"
      blacklistCompliant:
        type: "boolean"
        example: true
        description: "A flag to determine device is black list complaint"
        default: false
      suggestedListCompliant:
        type: "boolean"
        example: true
        description: "A flag to determine device is suggested list complaint"
        default: false
      requiredListCompliant:
        type: "boolean"
        example: true
        description: "A flag to determine device is required list complaint"
        default: false
      devicePropertiesTimestamp:
        type: "integer"
        format: "int64"
        example: 1479918557673
        description: "Device Properties last sync timestamp"
      revoked:
        type: "boolean"
        example: false
        description: "A flag to determine if the device is revoked"
        default: false
      managedSoftwareInventory:
        type: "array"
        description: "Device managed software inventory list"
        items:
          $ref: "#/definitions/SoftwareInventory"
      mamDeviceId:
        type: "string"
        example: "JQhdgzlC6ObIE98H/54RcK3z1EozSwXulRIWqIL6gsA="
        description: "MAM Device Id"
      deviceToken:
        type: "string"
        example: "40EB3812-D6DB-4872-A14B-A5203A3B8C25"
        description: "Device token"
      deviceType:
        type: "string"
        example: "iPad"
        description: "Type of the device"
      typeInst:
        type: "integer"
        format: "int32"
        example: 0
        description: "Device type instance number"
      appLock:
        type: "boolean"
        example: false
        description: "A flag to indicate if app lock action has been performed on\
          \ device"
        default: false
      appWipe:
        type: "boolean"
        example: false
        description: "A flag to indicate if app wipe action has been performed on\
          \ device"
        default: false
      mamReady:
        type: "boolean"
        example: false
        description: "A flag to determine if device is MAM ready"
        default: false
      enrollmentMode:
        type: "string"
        example: "null"
        description: "Device enrollment mode"
      deliveryGroups:
        type: "array"
        xml:
          name: "deliveryGroup"
          wrapped: true
        description: "Delivery groups list associated with device"
        items:
          $ref: "#/definitions/deliveryGroups"
      xmlId:
        type: "string"
        example: "11"
        description: "Device XML ID"
      sharedStatus:
        type: "string"
        example: "INACTIVE"
        description: "Device shared status"
        enum:
        - "INACTIVE"
        - "CHECKED_OUT"
        - "CHECK_IN_PENDING"
        - "CHECKED_IN"
        - "CHECK_OUT_PENDING"
        - "CHECK_IN_FAILED"
        - "CHECK_OUT_FAILED"
      managed:
        type: "boolean"
        example: true
        description: "A flag to determine if device is managed."
        default: false
      smgStatus:
        type: "string"
        example: "NONE"
        description: "Device secure mobile gateway status "
        enum:
        - "ACCESS_ALLOWED"
        - "ACCESS_DENIED"
        - "NONE"
      nbFailure:
        type: "integer"
        format: "int32"
        example: 0
        description: "Failed deployments count"
      nbPending:
        type: "integer"
        format: "int32"
        example: 0
        description: "Pending deployments count"
      nbSuccess:
        type: "integer"
        format: "int32"
        example: 1
        description: "Successful deployments count"
      mdmKnown:
        type: "boolean"
        example: true
        description: "A flag to determine if device is MDM known"
        default: false
      mamKnown:
        type: "boolean"
        example: true
        description: "A flag to determine if device is MAM known"
        default: false
      mamRegistered:
        type: "boolean"
        example: true
        description: "A flag to determine if device is MAM registered"
        default: false
      activesyncid:
        type: "string"
        example: "HS4ML5821324T11CFEM9D2442S"
        description: "Activesync Id for device"
      wifimac:
        type: "string"
        example: "8C:7C:92:66:9B:D4"
        description: "Wifi MAC address for the device "
      bluetoothmac:
        type: "string"
        example: "8C:7C:84:44:A3:D3"
        description: "Bluetooth MAC address for the device"
      platform:
        type: "string"
        example: "iOS"
        description: "Device platform"
      inactivityDays:
        type: "integer"
        format: "int32"
        example: 0
        description: "Device inactivity days"
      shareable:
        type: "boolean"
        example: false
        description: "A flag to determine if device is shareable"
        default: false
      bulkProfileStatus:
        type: "string"
        example: "NO_BULK"
        description: "Bulk profile status"
        enum:
        - "NO_BULK"
        - "EMPTY"
        - "ASSIGNED"
        - "PUSHED"
        - "REMOVED"
        - "PREPARED"
      softwareInventory:
        type: "array"
        xml:
          name: "softwareInventoryList"
          wrapped: true
        description: "Device software inventory list"
        items:
          $ref: "#/definitions/SoftwareInventory"
      deviceActions:
        type: "array"
        xml:
          name: "deviceAction"
          wrapped: true
        description: "Device actions list"
        items:
          $ref: "#/definitions/DeviceAction"
      policies:
        type: "array"
        description: "Policies deployed on the device"
        items:
          $ref: "#/definitions/PolicyResourceDeployState"
      active:
        type: "boolean"
        example: true
        description: "A flag to determine if the device is active"
        default: false
      osFamily:
        type: "string"
        example: "iOS"
        description: "Device OS family"
        enum:
        - "WINDOWS"
        - "iOS"
        - "ANDROID"
        - "SYMBIAN"
        - "RIM"
        - "UNKNOWN"
        - "WINPHONE"
        - "WINPC"
        - "WINRT"
        - "WINDOWS8"
        - "MACOSX"
      containerLockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device container lock action is enabled\
          \ for the device"
        default: false
      resetPinCode:
        type: "boolean"
        example: false
        description: "A flag to determine if reset pin code action is enabled for\
          \ the device"
        default: false
      restartEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if device restart action is enabled for\
          \ the device"
        default: false
      cancelUnlockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device cancel unlock action is enabled\
          \ for the device"
        default: false
      appWipeEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if application wipe action is enabled for\
          \ the device"
        default: false
      cancelRingEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel ring action is enabled for the\
          \ device"
        default: false
      iosprovisioningProfileInventory:
        type: "array"
        xml:
          name: "iosProvisioningProfileInventory"
          wrapped: true
        description: "ios provisioning profile inventory list"
        items:
          $ref: "#/definitions/IOSProvisioningProfileInventory"
      wipeEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if wipe action is enabled for device"
        default: false
      disownEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if disown action is enabled for the device"
        default: false
      locateEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if locate action is enabled for the device"
        default: false
      rebootEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if reboot action is enabled on windows 10\
          \ devices"
        default: false
      depActivationLockEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if device enrollment program activation lock\
          \ action is enabled for the device "
        default: false
      iosprofileInventory:
        type: "array"
        xml:
          name: "iosProfileInventory"
          wrapped: true
        description: "iOS profile inventory list"
        items:
          $ref: "#/definitions/IOSProfileInventory"
      lockMessage:
        type: "string"
        example: "Device lock due to no passcode policy"
        description: "Current lock message of the device, set through device lock\
          \ action"
      erasedMemoryCard:
        type: "boolean"
        example: false
        description: "A flag to determine if memory card erased action has been performed\
          \ on device"
        default: false
      lostModeFootnote:
        type: "string"
        example: "lost mode footnote message"
        description: "Lost mode foot note, set by enable lost mode action"
      appUnwipeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if application unwipe action is enabled\
          \ for the device"
        default: false
      appLockEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if application lock action is enabled for\
          \ the device"
        default: false
      gpsCoordinates:
        type: "array"
        xml:
          name: "gpsCoordinate"
          wrapped: true
        description: "Device GPS coordinates list"
        items:
          $ref: "#/definitions/DeviceCoordinate"
      pushState:
        type: "string"
        example: "INACTIVE"
        description: "Push state of device"
        enum:
        - "ENQUEUED"
        - "PENDING"
        - "ACTIVE"
        - "INACTIVE"
      lastPushDate:
        type: "integer"
        format: "int64"
        example: 1479921892416
        description: "Last push date for device"
      lastSentNotification:
        type: "integer"
        format: "int64"
        example: 1479921893435
        description: "Last sent notification timestamp"
      lastRepliedNotification:
        type: "integer"
        format: "int64"
        example: 1479921907294
        description: "Last replied notification timestamp"
      lastGpsCoordinate:
        $ref: "#/definitions/DeviceCoordinate"
      gpsFilterStartDate:
        type: "integer"
        format: "int64"
        example: 1479888000838
        description: "GPS coordinate list filter start date"
      gpsFilterEndDate:
        type: "integer"
        format: "int64"
        example: 1479974399838
        description: "GPS coordinate list filter end date"
      revokeEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if device revoked action is enabled for\
          \ the device"
        default: false
      lockEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if device lock action is enabled for the\
          \ device"
        default: false
      cancelLockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device cancel lock action is enabled\
          \ for the device"
        default: false
      unlockEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if device unlock action is enabled for the\
          \ device"
        default: false
      corpWipeEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if corporate wipe action is enabled for\
          \ the device"
        default: false
      cancelCorpWipeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel corporate wipe action is enabled\
          \ for the device"
        default: false
      enableTrackingEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if tracking action is enabled for the device"
        default: false
      disableTrackingEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if disable tracking action is enabled for\
          \ the device"
        default: false
      cancelWipeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel wipe action is enabled for the\
          \ device"
        default: false
      requestMirroringEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if request airplay mirroring action is enabled\
          \ on device"
        default: false
      wipePinCode:
        type: "string"
        example: "1234"
        description: "Wipe pin code for the device"
      cancelLocateEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel locate action is enabled for the\
          \ device"
        default: false
      dstDevIdUsed:
        type: "boolean"
        example: true
        description: "A flag to indicate if destination device ID is being used for\
          \ airplay mirroring, set by mirroring action"
        default: false
      cancelSdCardWipeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel SD card wipe action is enabled\
          \ for the device"
        default: false
      mediaFailure:
        type: "boolean"
        example: false
        description: "A flag to indicate media failure on device"
        default: false
      hasContainer:
        type: "boolean"
        example: false
        description: "A flag to determine if device has app container"
        default: false
      screenSharingPwd:
        type: "string"
        example: "null"
        description: "Screen sharing password of the device, set by mirroring action"
      applicationsFailure:
        type: "boolean"
        example: false
        description: "A flag to indicate application failure on device"
        default: false
      lockPhoneNumber:
        type: "string"
        example: "5417543010"
        description: "Phone number currently shown on locked device, set through lock\
          \ action"
      dstValue:
        type: "string"
        example: "null"
        description: "Destination value for airplay mirroring, set by mirroring action"
      scanTime:
        type: "string"
        example: "30"
        description: "Scan time for airplay mirroring, set by mirroring action"
      lostModeMessage:
        type: "string"
        example: "This device has been lost.."
        description: "Device lost mode message, set by enable lost mode action"
      lostModePhoneNumber:
        type: "string"
        example: "+123456789"
        description: "Lost mode phone number, set by enable lost mode action"
      smartActionsFailure:
        type: "boolean"
        example: false
        description: "A flag to indicate smart actions failure on device"
        default: false
      policiesFailure:
        type: "boolean"
        example: false
        description: "A flag to indicate policies failure on device"
        default: false
      touchdownProperties:
        type: "array"
        description: "Touchdown properties list"
        items:
          $ref: "#/definitions/TouchdownProperty"
      enableLostModeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if action for enabling lost mode is available\
          \ for the device"
        default: false
      cancelEnableLostModeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if action for cancel enabling lost mode\
          \ is available for the device"
        default: false
      disableLostModeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if action for disabling lost mode is available\
          \ for the device"
        default: false
      cancelDisableLostModeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if action for cancel disabling lost mode\
          \ is available for the device"
        default: false
      htcMdm:
        type: "boolean"
        example: false
        xml:
          name: "isHtcMdm"
        description: "A flag to determine if device is htc MDM"
        default: false
      newPinCode:
        type: "string"
        example: "1111"
        description: "Device new pin code"
      oldPinCode:
        type: "string"
        example: "1234"
        description: "Device old pin code"
      cancelRebootEnabled:
        type: "boolean"
        default: false
      packageStates:
        type: "array"
        xml:
          name: "packageState"
          wrapped: true
        description: "Deployment States list"
        items:
          $ref: "#/definitions/DeployState"
      deviceUsers:
        type: "array"
        xml:
          name: "deviceUser"
          wrapped: true
        description: "Device users list"
        items:
          $ref: "#/definitions/DeviceUser"
      sdCardWipeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if SD card wipe action is enabled for the\
          \ device"
        default: false
      shutdownEnabled:
        type: "boolean"
        example: true
        description: "A flag to determine if device shutdown action is enabled for\
          \ the device"
        default: false
      cancelShutdownEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device cancel shutdown action is enabled\
          \ for the device"
        default: false
      authorizeEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device authorize action is enabled for\
          \ the device"
        default: false
      ringEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if ring action is enabled for the device"
        default: false
      pushStateLabel:
        type: "string"
        example: "INACTIVE"
        description: "Device push state label"
      stopMirroringEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if stop airplay mirroring action is enabled\
          \ on the device"
        default: false
      cancelRequestMirroringEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if cancel request airplay mirroring action\
          \ is enabled on the device"
        default: false
      cancelStopMirroringEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if cancel stop airplay mirroring action is\
          \ enabled on the device"
        default: false
      lockDeviceFlag:
        type: "boolean"
        example: false
        description: "A flag to determine if device lock action has been performed\
          \ on the device"
        default: false
      managedByZMSP:
        type: "boolean"
        example: false
        description: "A flag to determine if ActiveSync device is known by MSP"
        default: false
      wipeDeviceFlag:
        type: "boolean"
        example: false
        description: "A flag to determine if wipe action has been performed on the\
          \ device"
        default: false
      cancelRestartEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device cancel restart action is enabled\
          \ for the device"
        default: false
      knownByZMSP:
        type: "boolean"
        example: false
        description: "A flag to determine if ActiveSync device is known by MSP"
        default: false
      nbAvailable:
        type: "integer"
        format: "int32"
        example: "null"
        description: "Available deployments count"
      cancelClearRestrictionsEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel clear restrictions action is enabled\
          \ for the device"
        default: false
      clearRestrictionsEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if clear restrictions action is enabled\
          \ for the device"
        default: false
      appUnlockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if application unlock action is enabled\
          \ for the device"
        default: false
      cancelContainerPwdResetEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel container password reset action\
          \ is enabled for the device"
        default: false
      bulkEnrolled:
        type: "boolean"
        example: false
        description: "A flag to indicate if device is DEP enrolled"
        default: false
      revokedCertificates:
        type: "array"
        xml:
          name: "revokedCertificateList"
        description: "Revoked certificate list on the device"
        items:
          $ref: "#/definitions/DeviceCertificate"
      validCertificates:
        type: "array"
        xml:
          name: "validCertificateList"
        description: "Valid certificate list on the device"
        items:
          $ref: "#/definitions/DeviceCertificate"
      activationLockBypassEnabled:
        type: "boolean"
        example: false
        description: "A flag to indicate if device enrollment program activation lock\
          \ bypass action is enabled for the device "
        default: false
      containerPwdResetEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if container password reset action is enabled\
          \ for the device"
        default: false
      containerUnlockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device container unlock action is enabled\
          \ for the device"
        default: false
      cancelContainerUnlockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if cancel container unlock action is enabled\
          \ for the device"
        default: false
      cancelContainerLockEnabled:
        type: "boolean"
        example: false
        description: "A flag to determine if device cancel container lock action is\
          \ enabled for the device"
        default: false
      connected:
        type: "boolean"
        example: false
        description: "A flag to determine if the device is connected"
        default: false
      serialNumber:
        type: "string"
        example: "G7NLCDEQF146"
        description: "Serial number of the device"
      properties:
        type: "array"
        xml:
          name: "property"
          wrapped: true
        description: "Device properties list"
        items:
          $ref: "#/definitions/Property"
      id:
        type: "integer"
        format: "int32"
        example: 11
        description: "Database Id of the device"
    description: "Device Information"
  EnrollmentStoresInfo:
    type: "object"
    properties:
      enrollmentModes:
        type: "array"
        description: "list of enrollment modes"
        items:
          $ref: "#/definitions/EnrollmentMode"
      notificationTemplatesCategories:
        type: "array"
        items:
          $ref: "#/definitions/NotificationTemplatesCategory"
      domainGroupsList:
        type: "array"
        description: "List of domain groups"
        items:
          $ref: "#/definitions/DomainGroups"
      carriers:
        type: "array"
        example: "['Verizon', 'AT&T']"
        description: "Carriers list"
        items:
          type: "string"
    description: "Enrollment store information data model"
    xml:
      name: "enrollmentStoresInfo"
  DeviceCurrentFilter:
    type: "object"
    properties:
      detail:
        type: "array"
        xml:
          name: "filters"
        description: "Filter node detail"
        items:
          $ref: "#/definitions/DeviceFilterNode"
      selectedFilters:
        type: "array"
        example: "['group#/group/ActiveDirectory/domain/net/Domain Users@_fn_@normal']"
        description: "Selected Filters"
        items:
          type: "string"
    description: "Current filter for devices"
  GeneratePinCodeResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      pinCode:
        xml:
          name: "result"
        $ref: "#/definitions/GeneratePinCode"
    description: "Pin code generate response model"
  RoleDefinitionTreeResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      roleBasedAccessTreeChildren:
        $ref: "#/definitions/RoleBasedAccessTreeChildren"
    description: "Role Definition Tree Response Model"
  DevicePropertiesRequest:
    type: "object"
    required:
    - "properties"
    properties:
      properties:
        type: "array"
        xml:
          name: "property"
        description: "List of DeviceProperties containing name and value of device\
          \ property"
        items:
          $ref: "#/definitions/DevicePropertyRequest"
    description: "Model for capturing the device properties save request"
  DGResource:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "resName"
        description: "Resource name"
      priority:
        type: "integer"
        format: "int32"
        example: 0
        description: "Resource priority"
  DeliveryGroupUpdateRequest:
    type: "object"
    required:
    - "id"
    - "name"
    properties:
      name:
        type: "string"
        example: "dgDomainUsers"
        description: "Delivery group name"
      description:
        type: "string"
        example: "Delivery group for domain users"
        description: "Delivery group description"
      groups:
        type: "array"
        description: "List of user groups on which delivery group will be deployed"
        items:
          $ref: "#/definitions/CPGroup"
      users:
        type: "array"
        description: "List of users on which delivery group will be deployed"
        items:
          $ref: "#/definitions/DeliveryGroupUser"
      zoneId:
        type: "integer"
        format: "int64"
        example: 2
        description: "Sharefile zone id"
      zoneDomain:
        type: "string"
        example: "domain"
        description: "Sharefile zone domain"
      disabled:
        type: "boolean"
        example: false
        description: "Is disabled delivery group"
        default: false
      anonymousUser:
        type: "boolean"
        example: true
        description: "Is anonymous deployment"
        default: false
      cwcManaged:
        type: "boolean"
        description: "Is the delivery group managed by CWC"
        default: false
      applications:
        type: "array"
        description: "List of applications"
        items:
          $ref: "#/definitions/DGApplication"
      devicePolicies:
        type: "array"
        description: "List of device policies"
        items:
          $ref: "#/definitions/DGResource"
      smartActions:
        type: "array"
        description: "List of smart actions"
        items:
          $ref: "#/definitions/DGResource"
      connectors:
        type: "array"
        description: "List of sharefile connectors"
        items:
          $ref: "#/definitions/DGConnector"
      enrollmentProfileId:
        type: "integer"
        format: "int64"
        description: "ID of the enrollment profile that is associated with this delivery\
          \ group"
      roledefLangVersionId:
        type: "integer"
        format: "int32"
        example: 2
        xml:
          name: "version"
        description: "Delivery group definition version"
      id:
        type: "integer"
        format: "int64"
        example: 2
        description: "Delivery Group Id"
    description: "Model for capturing delivery group update request information"
  DevicePropertiesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      devicePropertiesList:
        xml:
          name: "result"
        $ref: "#/definitions/DevicePropertiesList"
    description: "Device properties response model"
  ClientPropertiesAddRequest:
    type: "object"
    required:
    - "description"
    - "displayName"
    - "key"
    - "value"
    properties:
      value:
        type: "string"
        example: "15"
        description: "Value of the client property"
      displayName:
        type: "string"
        example: "MyProperty"
        description: "Display name of the client property"
      description:
        type: "string"
        example: "MyProperty Description"
        description: "Description of the client property"
      key:
        type: "string"
        example: "CP_KEY"
        description: "Key of the client property"
    description: "Client Properties Add Request Model"
  DeviceKnownPropertyParameters:
    type: "object"
    properties:
      groupLabel:
        type: "string"
        example: "System information"
        description: "Group label of the property"
      type:
        type: "string"
        example: "STRING"
        description: "Property data structure type"
        enum:
        - "STRING"
        - "INTEGER"
        - "INTEGER_PERCENT"
        - "INTEGER_DATA_SIZE"
        - "INTEGER_SPEED_FREQUENCY"
        - "INTEGER_PIXEL"
        - "INTEGER_PPI"
        - "DECIMAL_INCH"
        - "INTEGER_LEVEL_ENCRYPTION"
        - "INTEGER_MCC"
        - "INTEGER_CELLULAR_TECHNOLOGY"
        - "DATE"
        - "BOOLEAN"
        - "BOOLEAN_CORPORATE_EMPLOYEE"
        - "BOOLEAN_YES_NO"
        - "BOOLEAN_PASSED_FAILED"
        - "OS_FAMILIY"
        - "STRING_AFW_INSTALL_TYPE"
      name:
        type: "string"
        example: "SYSTEM_PLATFORM"
        description: "Property name"
      displayName:
        type: "string"
        example: "Platform"
        description: "Property display name"
      group:
        type: "string"
        example: "SYSTEM"
        description: "Group name of the property"
        enum:
        - "EVERYWAN"
        - "SYSTEM"
        - "NETWORK"
        - "SECURITY"
        - "MEMORY_RAM"
        - "MEMORY_DISK"
        - "OTHER"
        - "SCREEN"
        - "BATTERY"
        - "GPS"
        - "GPS_FROM_CELLULAR"
        - "NOTIFICATION"
        - "GOOGLE_AW"
        - "WINDOWS_HAS"
    description: "Device known property data model"
  PasswordRule:
    type: "object"
    required:
    - "firstRemainderMail"
    - "isAutoResetpwdRequired"
    - "isCapitalLetterRequired"
    - "isSpecialCharacterRequired"
    - "isUsernameOK"
    - "minLength"
    - "pwdValidity"
    properties:
      minLength:
        type: "integer"
        format: "int32"
        example: 8
        description: "Minimum password length"
      maxLength:
        type: "integer"
        format: "int32"
        example: 20
        description: "Maximum password length"
      isUsernameOK:
        type: "boolean"
        example: false
        description: "Identifies whether user name is allowed to set as a password\
          \ or not"
        default: false
      isSpecialCharacterRequired:
        type: "boolean"
        example: true
        description: "Identifies whether a special character is mandatory for password\
          \ or not"
        default: false
      isCapitalLetterRequired:
        type: "boolean"
        example: true
        description: "Identifies whether a capital letter is mandatory for password\
          \ or not"
        default: false
      firstRemainderMail:
        type: "integer"
        format: "int32"
        example: 90
        description: "Days for receiving first reminder email"
      pwdValidity:
        type: "integer"
        format: "int32"
        example: 90
        description: "Password validity period in days"
      isAutoResetpwdRequired:
        type: "boolean"
        example: false
        description: "Automatically reset password after it expires"
        default: false
    description: "Workflow data model"
  EnrollmentMode:
    type: "object"
    properties:
      name:
        type: "string"
        example: "invitation_pin"
        description: "Enrollment mode name"
      modeDisplayName:
        type: "string"
        example: "Invitation URL + PIN"
        description: "Enrollment mode display name"
      validDurationMillis:
        type: "integer"
        format: "int64"
        example: 86400000
        description: "Mode valid duration settings, After the amount enrolment will\
          \ be considered as expired"
      maxTry:
        type: "integer"
        format: "int32"
        example: 3
        description: "Maximum allowed tries"
      secretLength:
        type: "integer"
        format: "int32"
        example: 8
        description: "Secret length"
      secretGenerator:
        type: "string"
        example: "NUMERIC"
        description: "Secret generator"
        enum:
        - "NUMERIC"
        - "ALPHANUMERIC_LO"
        - "ALPHANUMERIC_UP"
        - "ALPHANUMERIC_MIXED"
      notificationTemplateCategories:
        type: "array"
        description: "List of notification template category"
        items:
          $ref: "#/definitions/NotificationTemplateCategory"
      requiringSecret:
        type: "boolean"
        example: true
        xml:
          name: "isRequiringSecret"
        description: "A flag to determine if mode requires secret"
        default: false
      shpMode:
        type: "boolean"
        example: false
        xml:
          name: "isShpMode"
        description: "A flag to indicate if the mode can be used as SHP"
        default: false
      defaultable:
        type: "boolean"
        example: false
        xml:
          name: "isDefaultable"
        description: "A flag to indicate if the mode can be set as default"
        default: false
      requiringIdentification:
        type: "boolean"
        example: false
        xml:
          name: "isRequiringIdentification"
        description: "A flag to determine if mode requires identification"
        default: false
      requiringAuthentication:
        type: "boolean"
        example: false
        xml:
          name: "isRequiringAuthentication"
        description: "A flag to determine if mode requires authentication"
        default: false
      requiringToken:
        type: "boolean"
        example: true
        xml:
          name: "isRequiringToken"
        description: "A flag to indicate if mode requires token"
        default: false
      requiringCertificate:
        type: "boolean"
        example: false
        xml:
          name: "isRequiringCertificate"
        description: "A flag to determine if mode requires certificate"
        default: false
      default:
        type: "boolean"
        example: false
        xml:
          name: "isDefault"
        description: "A flag to indicate if the mode is set as default"
        default: false
      enabled:
        type: "boolean"
        example: true
        xml:
          name: "isEnabled"
        description: "A flag to indicate if the mode is enabled"
        default: false
    description: "Enrollment mode info"
    xml:
      name: "enrollmentMode"
  SimpleUser:
    type: "object"
    required:
    - "id"
    - "xmlId"
    properties:
      xmlId:
        type: "string"
        example: "13"
        description: "Xml Id in the database"
      properties:
        type: "array"
        xml:
          name: "property"
          wrapped: true
        description: "Properties of simple user"
        items:
          $ref: "#/definitions/Property"
      id:
        type: "integer"
        format: "int64"
        example: 13
        description: "User Id"
      displayName:
        type: "string"
        example: "abc@domain.net"
        description: "Display name of simple user"
    description: "Simple User Information"
  DeviceKnownPropertiesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      knownProperties:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceKnownProperties"
    description: "Device known properties model"
  DeviceCoordinateResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      deviceCoordinate:
        xml:
          name: "result"
        $ref: "#/definitions/DeviceCoordinate"
    description: "Device coordinates response model"
  DeviceKnownPropertiesList:
    type: "object"
    properties:
      knownPropertyList:
        type: "array"
        description: "Device known property parameters list"
        items:
          $ref: "#/definitions/DeviceKnownPropertyParameters"
    description: "Device known properties model list"
  RoleDefinitionAddRequest:
    type: "object"
    required:
    - "name"
    - "permissions"
    properties:
      adGroups:
        type: "array"
        description: "List of active directory groups associated with this role"
        items:
          $ref: "#/definitions/AdGroup"
      permissions:
        type: "array"
        description: "List of permissions included in this role"
        items:
          $ref: "#/definitions/RolePermission"
      name:
        type: "string"
        example: "ADMIN_11"
        description: "Name of the role"
    description: "Role Definition Add Request Model"
  UserGroupDto:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int64"
        example: 1
        description: "Id of the group"
      userListId:
        type: "integer"
        format: "int64"
        example: 1
        description: "User list id"
      name:
        type: "string"
        example: "MSP"
        description: "Group name"
      uniqueName:
        type: "string"
        example: "MSP"
        description: "Unique name of the group"
      uniqueId:
        type: "string"
        example: "MSP"
        description: "Unique id of the group"
      domainName:
        type: "string"
        example: "local"
        description: "Domain name of the group"
      primaryToken:
        type: "integer"
        format: "int32"
        example: 0
        description: "Primary Token of the group"
  UserGroupsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      userGroups:
        type: "array"
        description: "List of user groups"
        items:
          $ref: "#/definitions/UserGroupDto"
    description: "User Groups Response Model"
  RoleBasedAccessResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
    description: "Role  Based Access Response Model"
  IOSConfigInventory:
    type: "object"
    properties:
      organization:
        type: "string"
        example: "XenMobile"
        description: "Name of organization"
      identifier:
        type: "string"
        example: "com.zenprise.zdm.ca.digitalSignature#0"
        description: "iOS profile identifier"
      description:
        type: "string"
        example: "XenMobile Digital Signing Intermediate Authority #0"
        description: "Description of iOS profile"
      type:
        type: "string"
        example: "com.apple.security.pkcs1"
        description: "Type of configuration"
      name:
        type: "string"
        example: "XenMobile Digital Signing Intermediate Authority #0"
        description: "Name of iOS profile"
    description: "iOS configuration inventory"
  EnrollmentInfoResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      enrollmentInfo:
        $ref: "#/definitions/EnrollmentStoresInfo"
    description: "Enrollment store information response data"
  DeviceSwInventoryResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      softwareInventory:
        type: "array"
        description: "Collection of software inventories deployed on the device"
        items:
          $ref: "#/definitions/SoftwareInventory"
    description: "Device software inventories response data"
  DGApplication:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        example: "resName"
        description: "Resource name"
      priority:
        type: "integer"
        format: "int32"
        example: 0
        description: "Resource priority"
      required:
        type: "boolean"
        example: true
        description: "Is required/optional application"
        default: false
  ServerPropertiesDto:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int64"
        example: 1
        description: "Id of the server property"
      name:
        type: "string"
        example: "webservices.enable"
        description: "Key of the server property"
      value:
        type: "string"
        example: "true"
        description: "Value of the server property"
      displayName:
        type: "string"
        example: "REST Web Services"
        description: "Display name of the server property"
      description:
        type: "string"
        example: "REST web service enable or disable."
        description: "Description of the server property"
      defaultValue:
        type: "string"
        example: "true"
        description: "Default value of the server property"
    description: "Server properties model"
  ShareFileConnectorCreateRequest:
    type: "object"
    required:
    - "deliveryGroups"
    - "description"
    - "location"
    - "name"
    - "storageZoneId"
    - "storageZoneName"
    - "type"
    properties:
      name:
        type: "string"
        example: "Connector1"
        description: "Name of sharefile connector"
      type:
        type: "string"
        example: "NetworkFile"
        description: "Type of sharefile connector: supported values are SharePoint,\
          \ NetworkFile"
      location:
        type: "string"
        example: "//sz/test"
        description: "Location of sharefile connector"
      storageZoneId:
        type: "string"
        example: "1"
        description: "Id of storage zone"
      storageZoneName:
        type: "string"
        example: "StorageZone1"
        description: "Name of storage zone"
      deliveryGroups:
        type: "array"
        example: "['dg01','dg02']"
        description: "List of associated delivery groups with sharefile connector"
        items:
          type: "string"
      description:
        type: "string"
        example: "description"
        description: "Description of sharefile connector"
    description: "Model for creating sharefile connector"
  EnrollmentModesResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      enrollmentModes:
        $ref: "#/definitions/EnrollmentModes"
    description: "Enrollment modes response data model"
  ShareFileConnectorsResponse:
    type: "object"
    properties:
      status:
        type: "integer"
        format: "int32"
        example: 0
        description: "Status code of the request. Would be 0 in case of success and\
          \ in case of error it would be an error code"
      message:
        type: "string"
        example: "Success"
        description: "Status message of the request"
      shareFileConnectors:
        type: "array"
        description: "List of sharefile connectors"
        items:
          $ref: "#/definitions/ShareFileConnectorData"
    description: "Response data for sharefile connector"
  RolePermission:
    type: "object"
    required:
    - "permission"
    properties:
      permission:
        type: "string"
        example: "perm-feature-REPORT-"
        description: "Permission name"
      granted:
        type: "boolean"
        example: true
        description: "Flag to indicate if permission is granted"
        default: false
  ShareFileEnterpriseRequest:
    type: "object"
    required:
    - "accountProvisioning"
    - "domain"
    - "password"
    - "roles"
    - "userName"
    properties:
      domain:
        type: "string"
        example: "subdomain.sharefile.com"
        description: "Setting sharefile enterprise domain name"
      accountProvisioning:
        type: "boolean"
        example: true
        description: "Setting sharefile enterprise user account provisioning"
        default: false
      password:
        type: "string"
        example: "password"
        description: "Setting sharefile enterprise administrator account password"
      userName:
        type: "string"
        example: "test@xyz.com"
        description: "Setting sharefile enterprise administrator account user"
      roles:
        type: "array"
        example: "['dg01','dg02']"
        description: "Setting sharefile enterprise list of delivery groups association"
        items:
          type: "string"
    description: "Model for sharefile enterprise settings"
  EnrollmentModes:
    type: "object"
    properties:
      enrollmentModes:
        type: "array"
        xml:
          name: "enrollmentModeList"
        description: "List of enrollment mode"
        items:
          $ref: "#/definitions/EnrollmentMode"
    description: "Enrollment mode info"
    xml:
      name: "enrollmentModes"
---

In this example swagger description is directly embedded in the page. See
[source file](https://raw.githubusercontent.com/jexhson/jekyll-swagger/gh-pages/example-1.md)
