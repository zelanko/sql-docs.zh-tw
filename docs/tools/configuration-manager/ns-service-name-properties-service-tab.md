---
title: NS$&lt;服務名稱&gt;屬性 （服務索引標籤） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57c6b791-1663-4a01-9de2-cf1bdd8adb2c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6c59ff68ccee2fb2655badb0ac98ca782fa641a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nsltservice-namegt-properties-service-tab"></a>NS$&lt;屬性名稱&gt; 屬性 ([服務] 索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  這個服務是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNS](../../includes/ssns-md.md)] 服務。 淺灰色的屬性值不得以此應用程式加以變更。  
  
## <a name="options"></a>選項。  
 **二進位路徑**  
 顯示這個服務使用之程式檔案的位置。  
  
 **錯誤控制**  
 1 表示 `SERVICE_ERROR_NORMAL`。 如果在電腦啟動過程中，服務無法啟動，啟動程式就會記錄錯誤並顯示快顯訊息方塊，但是仍會繼續啟動作業。 這項值不能被改變。  
  
 **結束碼**  
 發生錯誤時，錯誤號碼會在這個方塊中顯示。 請使用這個號碼進行疑難排解，方法是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫中搜尋該號碼，或者將號碼提供給技術支援人員。  
  
 **Host Name**  
 顯示執行全文檢索搜尋之電腦或叢集的名稱。  
  
 **名稱**  
 表示服務的顯示名稱。  
  
 **處理序識別碼**  
 顯示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 處理序識別碼。  
  
 **SQL 服務類型**  
 為呼叫處理序所提供的服務類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝數個服務。  
  
 **啟動模式**  
 將這個服務設定為下列選擇：  
  
-   手動：電腦啟動時，這項服務不會自動啟動。 您必須使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」或其他工具來啟動服務。  
  
-   自動：這部電腦啟動時，這項服務會嘗試啟動。  
  
-   停用：這項服務無法啟動。  
  
 **State**  
 表示這項服務為執行中、已停止或已停用。  
  
  
