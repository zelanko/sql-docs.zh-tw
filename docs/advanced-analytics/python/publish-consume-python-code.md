---
title: "發佈和取用的 Python 程式碼的 SQL Server 機器學習伺服器 （獨立） |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 9a7e56d5f2726b627381d24e3cfd8e50ade325f6
ms.sourcegitcommit: 657d18fc805512c9574b2fe7451310601b9d78cb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/12/2018
---
# <a name="publish-and-consume-python-web-services"></a>發佈和取用 Python web 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您可以將部署工作使用實施功能的 web 服務的 Python 方案[SQL Server 機器學習伺服器 （獨立）](../r/r-server-standalone.md)執行個體。 這篇文章描述要成功發行，然後再執行您方案的步驟。

目標對象為想要了解如何將 Python 程式碼或模型發行至 Server 的機器學習，以及如何使用程式碼或自訂應用程式中的模型的資料科學家。 

本文假設您已精通 Python。 您也應該擁有獨立伺服器，它會安裝獨立於其他 SQL Server 功能。 您的伺服器必須是[設定實施](../operationalization-with-mrsdeploy.md)若要啟用 web 服務裝載。 

## <a name="overview-of-workflow"></a>工作流程的概觀

從發行工作流程使用 Python web 服務可以摘要如下：

1. 請確認您有使用 Python Server 機器學習的獨立伺服器安裝。
2. 滿足[必要條件](#prereq)從核心 API Swagger 文件中產生 Python 用戶端程式庫。
3. 將驗證和標頭邏輯加入至您的 Python 指令碼。
4. 建立 Python 工作階段、 準備環境，以及建立要保留環境的快照集。
5. 發佈 web 服務，並將內嵌此快照集。
6. 使用您的工作階段中，嘗試 web 服務。
7. 管理這些服務。

![Swagger 工作流程](./media/data-scientist-python-workflow.png)

這篇文章討論的工作流程，每個步驟，並包括使用光圈資料集的範例 Python 程式碼。

## <a name="sample-code"></a>範例程式碼

此範例程式碼假設您擁有[產生必要的 Python 用戶端程式庫](#prereq)Swagger，從您已經使用 Autorest。 已實施針對設定 SQL Server 機器學習伺服器 （獨立） 執行個體上執行此程式碼。

若要瀏覽這個程式碼的深度，跳到[逐步解說](#walkthrough)如需詳細說明的完整程序。

> [!IMPORTANT]
> 這個範例會使用本機`admin`帳戶進行驗證。 不過，您應使用的認證和[驗證方法](#python-auth)系統管理員設定。

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 

import deployrclient

# This example is intended for use with Microsoft R Server 9.0.1. 
# If you are using a newer version of Machine Learning Server, 
# use the mrs_server library instead.

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")
# To use ML Server, replace with mrs_server.MRSServer()

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in all requests!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in all method calls to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list snapshots to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

<a name="walkthrough"></a>

## <a name="walkthrough"></a>逐步解說

本節說明程式碼更詳細的運作方式。


### <a name="prereq"></a> 步驟 1。 建立必要的用戶端程式庫

您可以開始發佈您的 Python 程式碼和模型，透過機器學習伺服器之前，您必須產生使用 Swagger 文件提供此版本的用戶端程式庫。

1. Swagger 程式碼產生器安裝在本機電腦上，讓自己熟悉如何使用它。 您將使用它來產生以 Python 應用程式開發介面的用戶端程式庫。 常用的工具包括[Azure AutoRest](https://github.com/Azure/autorest) （需要 Node.js） 和[Swagger Codegen](https://github.com/swagger-api/swagger-codegen)。 

2. 下載包含您的機器學習 Server 版本的核心 Api 之 Swagger 檔案。 此檔案包含 Swagger 範本定義的 REST 資源以及這些資源可呼叫的作業清單。 您可以找到此檔案在`https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`，其中`<version>`是 3 位數 R 伺服器版本號碼。 

   例如，R 伺服器 9.1 您會從下載： https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. 產生以靜態方式產生的用戶端程式庫，藉由傳遞`rserver-swagger-<version>.json`Swagger 程式碼產生器的檔案，並指定語言您想要。 在此情況下，您應該指定 Python。  

    例如，如果您使用 AutoRest 產生 Python 用戶端程式庫時，它可能會看起來像這樣，其中 3 位數的數字代表 R 伺服器版本號碼：
    
    `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`

4. 您也可以提供某些自訂標頭，並進行其他變更，再使用產生的用戶端程式庫虛設常式。 請參閱[命令列介面](https://github.com/Azure/autorest/blob/master/docs/user/cli.md)GitHub 上的文件集，如需詳細資訊，關於不同的設定選項和喜好設定，例如重新命名的命名空間。
   
5. 瀏覽以查看您可以進行各種 API 呼叫的核心用戶端程式庫。 

    在本例中，Autorest 產生某些目錄和 Python 用戶端程式庫的本機系統上的檔案。 根據預設，命名空間 （和目錄） 是`deployrclient`且看起來可能像這樣：
   
   ![Autorest 輸出路徑](./media/data-scientist-python-autorest.png)

    此預設命名空間中，會呼叫用戶端程式庫本身`deploy_rclient.py`。 如果您在您的 IDE，例如 Visual Studio 中開啟這個檔案，您會看到類似這樣：
   
   ![Python 用戶端程式庫](./media/data-scientist-python-client-library.png)


### <a name="step-2-add-authentication-and-header-logic"></a>步驟 2： 加入驗證和標頭邏輯

請記住，所有 Api 都要求驗證，因此，所有的使用者必須進行驗證進行 API 呼叫使用`POST /login`應用程式開發介面或透過 Azure Active Directory (AAD)。 

為了簡化這個程序，以便使用者不需要針對每個呼叫提供其認證，會發出持有人的存取權杖。  此持有人權杖是輕巧型的安全性權杖，將受保護資源的 「 持有者 」 存取權授與： 在此情況下，在機器學習伺服器的應用程式開發介面。 使用者通過驗證之後，應用程式必須驗證使用者的持有人權杖，以確定驗證成功的預定的合作對象。 若要深入瞭解如何管理這些語彙基元，請參閱[安全性的存取權杖](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)。

您與核心應用程式開發介面互動之前，先完成驗證時，取得所持有人的存取語彙基元使用[驗證方法](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication)設定您的系統管理員，然後將它包含在每個標頭，針對每個後續的要求：

1. 開始匯入以使它能在您慣用的 Python 程式碼編輯器 中的，例如 Jupyter、 Visual Studio，VS Code 或 iPython 用戶端程式庫。

   指定用戶端程式庫的父目錄。 在本例中，Autorest 產生的用戶端程式庫低於`C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. 將驗證邏輯加入至您的應用程式定義機器學習伺服器從本機電腦的連接、 提供認證，擷取存取權杖，將該語彙基元加入至標頭。 然後，您會使用該標頭的所有後續要求。  使用您的系統管理員所定義的驗證方法： 基本的系統管理員帳戶、 Active Directory/LDAP (AD/LDAP) 或 Azure Active Directory (AAD)。

   **AD/LDAP 或`admin`帳戶驗證**

   呼叫`POST /login`才能驗證的應用程式開發介面。 傳入`username`和`password`的本機系統管理員，或如果已啟用 Active Directory，傳遞 LDAP 帳戶資訊。 依次機器學習伺服器發出的承載/存取權杖。 通過驗證之後，使用者不再需要提供認證，只要語彙基元仍然有效，而且每個要求送出標頭。 如果您不知道您的連線設定，請連絡您的系統管理員。

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Azure Active Directory (AAD) 驗證**

   傳遞的 AAD 認證、 授權和用戶端識別碼。 AAD 接著發出[持有人的存取權杖](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)。 通過驗證之後，使用者不再需要提供認證，只要語彙基元仍然有效，而且每個要求送出標頭。 如果您不知道您的連線設定，請連絡您的系統管理員。

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. 新增`Bearer`存取語彙基元和機器學習的伺服器目前執行的檢查。  在驗證期間傳回此語彙基元和**必須包含在每個後續的要求標頭**。 這個範例會使用 Autorest 所產生的用戶端程式庫。

   > [!IMPORTANT]
   > 每個 API 呼叫必須經過驗證。 因此，請記住，包含與權杖給每個單一要求的標頭。

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>步驟 3： 準備工作階段和程式碼

在驗證之後，您可以啟動 Python 的工作階段，並建立發行更新版本的模型。 您可以在 web 服務中包含任何的 Python 程式碼或模型。 一旦您已設定您的工作階段的環境，您可以甚至將它儲存當做快照集以便為您擁有該之前，您可以重新載入您的工作階段。 

> [!IMPORTANT]
> 請記得以`headers`中每個要求。

1. R 伺服器上建立 Python 工作階段。 請確認指定的名稱和 Python 語言 (`runtime_type="Python"`)。  如果您不要設 Python 執行階段類型，則預設為。

   這是範例的持續的使用 Autorest 所產生的用戶端程式庫:

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. 建立或在您將資料發佈為 web 服務的 Python 中呼叫模型

   在此範例中，我們來定型 SciKit-了解支援向量機器 (SVM) 模型的機器學習服務伺服器的遠端執行個體上的光圈資料集上。  此資料集可以使用從[scikit-了解站台](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html)。

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. 建立快照集的這個 Python，才能在 web 服務中儲存以及在重現此環境的工作階段耗用時間。 當您需要包含特定文件庫、 物件、 模型、 檔案和成品的已備妥的環境時，快照集是很有用。 快照集儲存的整個工作區和工作目錄。 不過，發行時，您可以使用您已建立的快照。

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list snapshots to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

  > [!NOTE] 
   > 雖然發行環境相依性的 web 服務時，也可以使用快照集，它可能會影響耗用時間的效能。  為了達到最佳效能，請仔細考慮快照集的大小，請務必確保只有工作區中的物件，清除其他。 在工作階段，您可以使用 Python`del`函式或[ `deleteWorkspaceObject` API 要求](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object)移除不必要的物件。 

### <a name="step-4-publish-the-model"></a>步驟 4： 發行模型 

已產生您的用戶端程式庫，且您的驗證邏輯建立至您的應用程式之後，您可以與核心 Api 來建立 Python 工作階段、 建立模型，並再發佈 web 服務使用該模型進行互動。

要記得的一些事項：

+ 在進行任何應用程式開發介面呼叫之前，您必須進行驗證。 因此，包含`headers`中的所有要求。
+ 若要確保 web 服務會註冊為 Python 服務，請務必指定`runtime_type="Python"`。 如果您不要設 Python 執行階段類型，則預設為。
+ 計分需要具有 sepal 長度、 sepal 寬度、 瓣花瓣長度和瓣花瓣寬度的向量

下列程式碼為 Python web 服務發佈 SVM 模型。 此 web 服務會產生預測的類別，根據傳遞給它的值。

```python
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>步驟 5： 使用 web 服務

本節示範如何建立所在的相同工作階段中取用的服務。

1. 在相同的工作階段取得服務之服務控股和中繼資料。

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. 檢查服務持有資產，並準備取用。 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Include the request.Session object in the authentication headers.
   #By doing so, you don't need to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific Swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #You can download a service-specific Swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or, you can print just what you need from the Swagger file. 
   #This example gets the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #You can also print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. 藉由提供一些取用的服務輸入及取得光圈指定。 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>管理服務

既然您已建立 web 服務，您可以更新、 刪除或重新發行該服務。 您也可以列出使用 R 伺服器 （或 Server 機器學習） 所裝載的所有 web 服務。

### <a name="update-a-web-service"></a>更新 web 服務

 在此範例中，我們可以更新服務可能會耗用此服務的人員新增有用的描述。

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

您可以更新變更程式碼、 模型、 描述、 輸入、 輸出和多個 web 服務。

### <a name="publish-another-version"></a>發行另一個版本

在此範例中，服務現在會傳回光圈指定為字串的清單而不是字串。

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

若要發行相同的 web 服務的多個版本，您可以使用此模式。 

### <a name="list-services"></a>列出服務

這個範例會取得一份所有 web 服務，包括建立其他使用者，或在不同的語言。

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>刪除服務

在此範例中，我們會刪除我們剛發行的第二個 web 服務版本。

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

您可以刪除任何您所建立的服務。 只有當您指派給具有適當的權限的角色，您可以刪除其他服務。