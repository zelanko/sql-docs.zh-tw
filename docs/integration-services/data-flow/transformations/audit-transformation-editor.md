---
title: "稽核轉換編輯器 | Microsoft Docs"
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
  - "sql13.dts.designer.audittransformation.f1"
helpviewer_keywords: 
  - "稽核轉換編輯器"
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# 稽核轉換編輯器
  稽核轉換可讓封裝中的資料流程包含有關封裝執行的環境資料。 例如，可以將封裝、電腦與操作員的名稱加入資料流程。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括提供此資訊的系統變數。  
  
 若要深入了解稽核轉換，請參閱＜ [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md)＞。  
  
## 選項。  
 **輸出資料行名稱**  
 提供包含稽核資訊之新輸出資料行的名稱。  
  
 **稽核類型**  
 選取可用的系統變數以提供稽核資訊。  
  
|Value|說明|  
|-----------|-----------------|  
|**執行執行個體 GUID**|插入唯一識別封裝之執行執行個體的 GUID。|  
|**封裝識別碼**|插入唯一識別封裝的 GUID。|  
|**封裝名稱**|插入封裝名稱。|  
|**版本識別碼**|插入唯一識別封裝版本的 GUID。|  
|**執行開始時間**|插入封裝開始執行的時間。|  
|**電腦名稱**|插入啟動封裝的電腦名稱。|  
|**使用者名稱**|插入啟動封裝之使用者的登入名稱。|  
|**工作名稱**|插入與稽核轉換相關聯之資料流程工作的名稱。|  
|**工作識別碼**|插入唯一識別與稽核轉換相關聯之資料流程工作的 GUID。|  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  