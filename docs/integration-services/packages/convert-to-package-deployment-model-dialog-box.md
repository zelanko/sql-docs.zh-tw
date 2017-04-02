---
title: "轉換成封裝部署模型對話方塊 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.bids.converttolegacydeployment.f1"
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 轉換成封裝部署模型對話方塊
  **[轉換成封裝部署模型]** 命令可讓您在檢查專案和專案中的每個封裝是否與該模型相容之後，將封裝轉換成封裝部署模型。 如果某個封裝使用專案部署模型獨有的功能 (例如參數)，則無法轉換該封裝。  
  
## 工作清單  
 將封裝轉換成封裝部署模型需要兩個步驟。  
  
1.  當您從 **[專案]** 功能表選取 **[轉換成封裝部署模型]** 命令時，會檢查專案和每個封裝是否與此模型相容。 結果會顯示在 **[結果]** 資料表中。  
  
     如果專案或封裝無法通過相容性測試，按一下 **[結果]** 資料行中的 **[失敗]** ，可取得詳細資訊。 按一下 **[儲存報表]** ，將此資訊的副本儲存到文字檔中。  
  
2.  如果專案和所有封裝通過相容性測試，則按一下 **[確定]** 以轉換封裝。  
  
> **注意：**若要將專案轉換為專案部署模型，請使用 [Integration Services 專案轉換精靈]。 如需相關資訊，請參閱 [Integration Services Project Conversion Wizard](https://msdn.microsoft.com/library/hh213290.aspx)。  
  
## 另請參閱  
 [舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Integration Services 專案轉換精靈](../../integration-services/packages/integration-services-project-conversion-wizard.md)  
  
  