---
title: SQL Server Agent 屬性 (服務索引標籤)
description: 了解 [SQL Server 代理程式屬性] 對話方塊中 [服務] 索引標籤上的選項，例如二進位路徑、處理序識別碼與啟動模式。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 452857fb-be1b-4e1e-851c-dd2216640f35
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 744391bc955f22c1a21144e90c68c26f289b8ced
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481659"
---
# <a name="sql-server-agent-properties-service-tab"></a>SQL Server Agent 屬性 (服務索引標籤)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  此服務為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 淺灰色的屬性值不得以此應用程式加以變更。  
  
## <a name="options"></a>選項。  
 **二進位路徑**  
 顯示這個服務使用之程式檔案的位置。  
  
 **錯誤控制**  
 1 表示 `SERVICE_ERROR_NORMAL`。 如果在電腦啟動過程中，服務無法啟動，啟動程式就會記錄錯誤並顯示快顯訊息方塊，但是仍會繼續啟動作業。 這項值不能被改變。  
  
 **結束碼**  
 發生錯誤時，錯誤號碼會在這個方塊中顯示。 請使用這個號碼進行疑難排解，方法是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫中搜尋該號碼，或者將號碼提供給技術支援人員。  
  
 **Host Name**  
 顯示執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 之電腦或叢集的名稱。  
  
 **名稱**  
 表示服務的顯示名稱。  
  
 **處理序識別碼**  
 顯示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 處理序識別碼。  
  
 **SQL 服務類型**  
 顯示為呼叫處理序所提供的服務類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝數個服務。  
  
 **啟動模式**  
 將這個服務設定為下列選擇：  
  
-   手動：當電腦啟動時，這項服務不會自動啟動。 您必須使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」或其他工具來啟動服務。  
  
-   自動：當這部電腦啟動時，這項服務會嘗試啟動。  
  
-   已停用：這項服務無法啟動。  
  
 **State**  
 表示這項服務為執行中、已停止或已停用。 " **...** " 表示狀態變更已暫止。  
  
  
