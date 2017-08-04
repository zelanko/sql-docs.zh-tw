---
title: "Analysis Server 屬性 （服務索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8dbe4bc5-6aa9-48ee-857e-0b4ea764b9cb
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b8d2da25a920e0d5e25f9b7fa72ce48529fa6686
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="analysis-server-properties-service-tab"></a>Analysis Server 屬性 (服務索引標籤)
  這個服務是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 必須執行此服務， [!INCLUDE[ssAS](../../includes/ssas-md.md)] 才能正常運作。 淺灰色的屬性值不得以此應用程式加以變更。  
  
## <a name="options"></a>選項。  
 **二進位路徑**  
 顯示這個服務使用之程式檔案的位置。  
  
 **錯誤控制**  
 1 表示 `SERVICE_ERROR_NORMAL`。 如果在電腦啟動過程中，服務無法啟動，啟動程式就會記錄錯誤並顯示快顯訊息方塊，但是仍會繼續啟動作業。 這項值不能被改變。  
  
 **結束碼**  
 發生錯誤時，錯誤號碼會在這個方塊中顯示。 請使用這個號碼進行疑難排解，方法是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫中搜尋該號碼，或者將號碼提供給技術支援人員。  
  
 **Host Name**  
 顯示執行 [!INCLUDE[ssAS](../../includes/ssas-md.md)]之電腦或叢集的名稱。  
  
 **名稱**  
 表示服務的顯示名稱。  
  
 **處理序識別碼**  
 顯示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 用來追蹤此程式之處理序的編號。  
  
 **SQL 服務類型**  
 顯示為呼叫處理序所提供的服務類型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會安裝數個服務。  
  
 **啟動模式**  
 將這個服務設定為下列選擇：  
  
-   手動：電腦啟動時，這項服務不會自動啟動。 您必須使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」或其他工具來啟動服務。  
  
-   自動：這部電腦啟動時，這項服務會嘗試啟動。  
  
-   停用：這項服務無法啟動。  
  
 **State**  
 表示這項服務為執行中、已停止或已停用。  
  
  
