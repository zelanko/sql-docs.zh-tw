---
title: MSSQLSERVER_33081 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5c47dd2a9d349da10e876f8da486790355be125
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|33081|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_DLL_TRUST_VERIFICATION_FAILED|  
|訊息文字|無法載入密碼編譯提供者 '%.*ls'，因為 Authenticode 簽章或檔案路徑無效。  請檢查先前其他失敗的訊息。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法載入錯誤訊息中所列的密碼編譯提供者。 有幾項 Win API 失敗可能導致此錯誤。 信號緩衝區中包含 API 所傳回已失敗的 API 名稱及 Windows 錯誤碼。 如需詳細資訊，請使用下列查詢針對 sys.dm_os_ring_buffers 檢視進行查詢。  
  
```  
SELECT * FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
```  
  
## <a name="user-action"></a>使用者動作  
若要調查問題，請搜尋 MSDN (http://msdn.microsoft.com/) 中的 Windows 錯誤碼。 解決此錯誤或連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS 以了解詳細資訊。 如果您需要連絡 CSS，請收集下列資訊以供支援人員參考。  
  
-   顯示無法載入密碼編譯提供者錯誤的錯誤記錄檔。  
  
-   下列陳述式的輸出：  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
> 請立即收集信號緩衝區資訊，以免於重新開啟時失去這些資訊。  
  

