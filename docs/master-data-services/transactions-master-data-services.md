---
description: 交易 (Master Data Services)
title: 交易
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9f98afd4445d135ba7437f42c7f71355e265217c
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480337"
---
# <a name="transactions-master-data-services"></a>交易 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]



--------------------------------------------------
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，每次對成員採取動作時，就會記錄交易。 交易可由所有使用者檢視，並由系統管理員反轉。 交易會顯示日期、時間、採取動作的使用者以及其他詳細資料。 使用者可以在交易中加入註解，指出交易發生的原因。  
  
## <a name="when-transaction-are-recorded"></a>記錄交易時  
 當成員發生下列情況時，則記錄交易：  
  
-   建立、刪除或重新啟用。  
  
-   屬性值變更。  
  
-   在階層中移動。  
  
 當商務規則變更屬性值時，不會記錄交易。  
  
## <a name="view-and-manage-transactions"></a>檢視及管理交易  
 在 [總管]**** 功能區域中，您可以檢視和註解自己進行的交易。 
  
 在 [版本管理]**** 功能區域中，系統管理員可以檢視其可存取模型當中所有使用者的全數交易，並反轉任何交易。
 
> [!NOTE]  
>  只要系統管理員的 [版本管理]**** 功能區域未套用唯讀權限層級，即可檢視所有使用者的全數交易。 例如，如果系統管理員設定了唯讀權限和更新權限等級，系統管理員就無法查看其他使用者的交易，因為唯讀權限的優先順序高於更新權限。
  
 若要設定交易記錄資料保留的時間長度，您可以設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫系統設定中的 **Log retention in Days** 屬性，或是在建立或編輯模型時設定 [記錄保留天數]****。 如需詳細資訊，請參閱[系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) 和[建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)。  
  
 SQL Server Agent 工作 MDS_MDM_Sample_Log_Maintenace，會觸發清除交易記錄的程序，並於每晚執行。 您可以使用 SQL Server Agent 來修改此工作的排程。  
  
 也可以呼叫下列預存程序來清除交易記錄檔。  
  
|預存程序|描述|  
|----------------------|-----------------|  
|mdm.udpTransactionsCleanup|會清除交易記錄|  
|mdm.udpValidationsCleanup|會清除驗證記錄|  
|mdm.udpEntityStagingBatchTableCleanup|會清除暫存資料表|  
  
 **範例**  
  
```  
DECLARE @CleanupOlderThanDate date = '2014-11-11',  
@ModelID INT = 7  
--Clean up Transaction Logs  
EXEC mdm.udpTransactionsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up Validation History  
EXEC mdm.udpValidationsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up EBS tables  
EXEC mdm.udpEntityStagingBatchTableCleanup @ModelID, @CleanupOlderThanDate;  
  
```  
  
## <a name="system-settings"></a>系統設定  
 當記錄暫存時， [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有一項設定會影響是否記錄交易。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 [系統設定] 資料表中調整這項設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
 在此版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中匯入資料時，可以指定是否要在起始預存程序時記錄交易。 如需詳細資訊，請參閱[暫存預存程序 &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md)。  
  
## <a name="concurrency"></a>並行  
 如果在多個「檔案總管」工作階段中同時顯示一個特定的實體值，就可以對相同的值進行同時編輯。 MDS 將不會自動偵測到同時編輯。 當多個使用者從多個工作階段 (例如從多部電腦、多個瀏覽器索引標籤或視窗，或多個使用者帳戶) 的網頁瀏覽器中使用 MDS Explorer 時，可能會發生這個情況。  
  
 即使允許異動，多個使用者還是可以更新相同的實體值而不發生任何錯誤。 通常在時間順序上，對值進行的最後一個編輯，其優先順序最高。 重複編輯衝突可以在異動記錄中手動觀察到，並透過管理員手動保留。 交易記錄將會針對 [先前的值]**** 顯示個別的交易，並針對每個工作階段的相關屬性顯示 [新值]****，但若有多個含相同舊值的 [新值]**** 存在時，不會自動解決衝突。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|藉由反轉交易來復原一個動作 (僅限系統管理員)。|[反轉交易 &#40;Master Data Services&#41;](../master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="external-resources"></a>外部資源  
 msdn.com 上的部落格文章 [Transactions, Validation Issue and Staging table cleanup](https://techcommunity.microsoft.com/t5/sql-server-integration-services/transactions-validation-issue-and-staging-table-cleanup/ba-p/388209)(交易、驗證問題與暫存資料表清除)。  
  
## <a name="related-content"></a>相關內容  
  
-   [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   [註解 &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)  
  
  
