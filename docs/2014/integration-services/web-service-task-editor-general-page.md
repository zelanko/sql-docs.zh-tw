---
title: Web 服務工作編輯器（一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c642c100e41574a525578c3392aedbc82ac419a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439845"
---
# <a name="web-service-task-editor-general-page"></a>Web 服務工作編輯器 (一般頁面)
  使用 [Web 服務工作編輯器]**** 對話方塊的 [一般]**** 頁面，來指定 HTTP 連接管理員、指定 Web 服務工作使用的 Web 服務描述語言 (WSDL) 檔案的位置、描述 Web 服務工作，以及下載 WSDL 檔案。  
  
 如需這項工作的詳細資訊，請參閱 [Web 服務工作](control-flow/web-service-task.md)。  
  
## <a name="options"></a>選項  
 **HTTPConnection**  
 在清單中選取連接管理員，或按一下 \<**New connection...**> 以建立新的連線管理員。  
  
> [!IMPORTANT]  
>  HTTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 **相關主題：**  [HTTP 連接管理員](connection-manager/http-connection-manager.md)、[HTTP 連接管理員編輯器 &#40;伺服器頁面&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 輸入本機電腦的 WSDL 檔案完整路徑，或按一下瀏覽按鈕 **（...）** ，然後找出此檔案。  
  
 如果您已經將 WSDL 檔案手動下載到電腦中，請選取該檔案。 如果尚未下載 WSDL 檔案，則請執行下列步驟：  
  
-   建立副檔名為 ".wsdl" 的空白檔案。  
  
-   在 [WSDLFile]**** 選項中選取此空白檔案。  
  
-   將**OverwriteWSDLFile**的值設定為 `True` ，即可讓空的檔案以實際的 WSDL 檔案覆寫。  
  
-   按一下 [下載 WSDL]****，下載實際的 WSDL 檔案並覆寫空白檔案。  
  
    > [!NOTE]  
    >  您必須先在 [WSDLFile]**** 方塊中提供現有的本機檔案名稱，才能啟用 [下載 WSDL]**** 選項。  
  
 **OverwriteWSDLFile**  
 指出是否可以覆寫 Web 服務工作的 WSDL 檔案。  
  
 如果您想要使用 [**下載 wsdl** ] 按鈕來下載 wsdl 檔案，請將此值設定為 `True` 。  
  
 **名稱**  
 為 Web 服務工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 Web 服務工作的描述。  
  
 **下載 WSDL**  
 下載 WSDL 檔案。  
  
 您必須先在 [WSDLFile]**** 方塊中提供現有的本機檔案名稱，才能啟用此按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Web 服務工作編輯器 &#40;輸入頁面&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [[Web 服務工作編輯器] &#40;[輸出] 頁面&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
