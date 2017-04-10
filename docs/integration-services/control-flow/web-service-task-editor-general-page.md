---
title: "Web 服務工作編輯器 (一般頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.webservicestask.general.f1"
helpviewer_keywords: 
  - "Web 服務工作編輯器"
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# Web 服務工作編輯器 (一般頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [一般] 頁面，來指定 HTTP 連接管理員、指定 Web 服務工作使用的 Web 服務描述語言 (WSDL) 檔案的位置、描述 Web 服務工作，以及下載 WSDL 檔案。  
  
 如需這項工作的詳細資訊，請參閱 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)。  
  
## 選項。  
 **HTTPConnection**  
 在清單中選取連接管理員，或按一下 [\<新增連接…>]，即可建立新的連接管理員。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 **相關主題：**[HTTP 連接管理員](../../integration-services/connection-manager/http-connection-manager.md)、[HTTP 連接管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 輸入本機電腦的 WSDL 檔案完整路徑，或按一下瀏覽按鈕 **(…)** 以找出此檔案。  
  
 如果您已經將 WSDL 檔案手動下載到電腦中，請選取該檔案。 如果尚未下載 WSDL 檔案，則請執行下列步驟：  
  
-   建立副檔名為 ".wsdl" 的空白檔案。  
  
-   在 [WSDLFile] 選項中選取此空白檔案。  
  
-   將 **OverwriteWSDLFile** 的值設為 [True]，讓實際的 WSDL 檔案可以覆寫此空白檔案。  
  
-   按一下 [下載 WSDL]，下載實際的 WSDL 檔案並覆寫空白檔案。  
  
    > [!NOTE]  
    >  您必須先在 [WSDLFile] 方塊中提供現有的本機檔案名稱，才能啟用 [下載 WSDL] 選項。  
  
 **OverwriteWSDLFile**  
 指出是否可以覆寫 Web 服務工作的 WSDL 檔案。  
  
 如果您想要使用 [下載 WSDL] 按鈕來下載 WSDL檔案，請將此值設為 [True]。  
  
 **名稱**  
 為 Web 服務工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 Web 服務工作的描述。  
  
 **下載 WSDL**  
 下載 WSDL 檔案。  
  
 您必須先在 [WSDLFile] 方塊中提供現有的本機檔案名稱，才能啟用此按鈕。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Web 服務工作編輯器 &#40;輸入頁面&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Web 服務工作編輯器 &#40;輸出頁面&#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  