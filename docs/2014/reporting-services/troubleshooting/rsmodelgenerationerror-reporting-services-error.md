---
title: rsModelGenerationError - Reporting Services 錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 248187189db1270439e16b21139c40e9440b2ba3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63229028"
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
  
