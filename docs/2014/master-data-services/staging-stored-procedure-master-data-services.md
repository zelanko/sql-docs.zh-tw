---
title: 暫存預存程序 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9259352350a099db5d9b18411ad4da06dfb19819
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971068"
---
# <a name="staging-stored-procedure-master-data-services"></a>暫存預存程序 (Master Data Services)
  從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]起始暫存處理序時，可以使用下列三個預存程序其中之一：  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 其中 name 是建立實體時所指定之暫存資料表的名稱。  
  
## <a name="staging-process-stored-procedure-parameters"></a>暫存處理序預存程序參數  
 下表列出這些預存程序的參數。  
  
|參數|描述|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必要|版本的名稱。 是否區分大小寫取決於您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 集合設定。|  
|**LogFlag**<br /><br /> 必要|決定是否在暫存處理序期間記錄交易。 可能的值包括：<br /><br /> **0**：不記錄交易。<br />**1**：記錄交易。<br /><br /> <br /><br /> 如需交易的詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](transactions-master-data-services.md)。|  
|**BatchTag**<br /><br /> 必要項，只有 Web 服務不需要|**BatchTag** 值，依暫存資料表中所指定。|  
|**Batch_ID**<br /><br /> 只有 Web 服務需要|**Batch_ID** 值，依暫存資料表中所指定。|  
  
### <a name="staging-process-stored-procedure-example"></a>暫存處理序預存程序範例  
 下列範例顯示如何使用暫存預存程序啟動暫存處理序。  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [驗證預存程式 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [使用暫存進程在 Master Data Services 中載入或更新成員](add-update-and-delete-data-master-data-services.md)   
 [查看暫存進程期間發生的錯誤 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
