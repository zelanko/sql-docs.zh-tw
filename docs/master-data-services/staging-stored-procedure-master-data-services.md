---
title: "暫存預存程序 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: 15
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 19ce25e1182e362761b1919f36d72623dd7289e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="staging-stored-procedure-master-data-services"></a>暫存預存程序 (Master Data Services)
  從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]起始暫存處理序時，可以使用下列三個預存程序其中之一：  
  
-   stg.udp_\<名稱>_Leaf  
  
-   stg.udp_\<名稱>_Consolidated  
  
-   stg.udp_\<名稱>_Relationship  
  
 其中 name 是建立實體時所指定之暫存資料表的名稱。  
  
## <a name="staging-process-stored-procedure-parameters"></a>暫存處理序預存程序參數  
 下表列出這些預存程序的參數。  
  
|參數|說明|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必要項|版本的名稱。 是否區分大小寫取決於您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 集合設定。|  
|**LogFlag**<br /><br /> 必要項|決定是否在暫存處理序期間記錄交易。 可能的值為：<br /><br /> **0**：不記錄交易。<br /><br /> **1**：記錄交易。<br /><br /> <br /><br /> 如需交易的詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)。|  
|**BatchTag**<br /><br /> 必要項，只有 Web 服務不需要|**BatchTag** 值，依暫存資料表中所指定。|  
|**Batch_ID**<br /><br /> 只有 Web 服務需要|**Batch_ID** 值，依暫存資料表中所指定。|  
|**使用者名稱**|選擇性參數|  
|**使用者識別碼**|選擇性參數|  
  
### <a name="staging-process-stored-procedure-example"></a>暫存處理序預存程序範例  
 下列範例顯示如何使用暫存預存程序啟動暫存處理序。  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N’domain\user’  
  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [驗證預存程序 &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [檢視暫存期間發生的錯誤 &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  

