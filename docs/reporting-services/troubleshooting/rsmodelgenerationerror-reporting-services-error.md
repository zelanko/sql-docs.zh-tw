---
title: "rsModelGenerationError-Reporting Services 錯誤 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 658d9bdaffa05e3bf287b38953bc2e318da7d319
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services 錯誤
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|rsRenderingError|  
|事件來源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|產生模型時發生錯誤。 (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>說明  
 無法產生報表模型。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 及更舊版本中，當 System.Data.DataSet 物件無法處理資料庫結構描述中的資料表或關聯性時 (例如在資料表內的同一個資料行中定義兩個外部索引鍵)，很可能就會出現這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 若要判斷導致這個訊息出現的明確原因，請檢閱位於 \Microsoft SQL Server\\<SQL Server 執行個體\>\Reporting Services\LogFiles 的報表伺服器記錄檔。  
  
## <a name="internal-only"></a>僅供內部使用  
  

