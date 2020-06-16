---
title: 暫存預存程序
description: 使用下列三個預存程式之一，從 Master Data Services 中的 SQL Server Management Studio 起始暫存進程。
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82b068612f0699cdba3788e4931fb6bdfe8c7e69
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796499"
---
# <a name="staging-stored-procedure-master-data-services"></a>暫存預存程序 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]起始暫存處理序時，可以使用下列三個預存程序其中之一：  
  
-   stg.< _Leaf udp_ \<name>  
  
-   stg.< _Consolidated udp_ \<name>  
  
-   stg.< _Relationship udp_ \<name>  
  
 其中 name 是建立實體時所指定之暫存資料表的名稱。  
  
## <a name="staging-process-stored-procedure-parameters"></a>暫存處理序預存程序參數  
 下表列出這些預存程序的參數。  
  
|參數|描述|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必要|版本的名稱。 是否區分大小寫取決於您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 集合設定。|  
|**LogFlag**<br /><br /> 必要|決定是否在暫存處理序期間記錄交易。 可能的值包括：<br /><br /> **0**：不記錄交易。<br /><br /> **1**：記錄交易。<br /><br /> <br /><br /> 如需交易的詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)。|  
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
      @UserName=N'domain\user'  
  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [驗證預存程式 &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [檢視暫存期間發生的錯誤 &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  
