---
title: 用於 Analysis Services 連接的資料提供者 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ba97f90b877896d68cd62598f11d0845fb698e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016075"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>使用 Analysis services 連接的用戶端程式庫 （資料提供者）
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 提供三個用戶端程式庫，也稱為**資料提供者**、 伺服器和資料存取工具和用戶端應用程式。 工具，例如 SSMS 和 SSDT 中，以及應用程式像是 Power BI Desktop 和 Excel 連接到 Analysis Services 使用這些程式庫。 ADOMD.NET 和 Analysis Services 管理物件 (AMO)，用戶端程式庫是受管理的用戶端程式庫。 Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。 用戶端程式庫是適用於 SQL Server Analysis Services 和 Azure Analysis Services。
  
##  <a name="bkmk_downloadsite"></a> 何處可取得較新版本  
 用戶端電腦上安裝的版本應與提供資料的伺服器主要版本相符。 如果伺服器安裝比網路中工作站上安裝的資料提供者還要新，您可能需要安裝較新版的程式庫。  

包含在舊版的 SQL Server Feature Pack 的用戶端程式庫對應至該 SQL 版本。不過，它們可能不是最新。 連接到 Azure Analysis Services 可能需要更新的版本。 所有版本都都具有回溯相容性。

若要取得最新，請參閱[用戶端程式庫連接到 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
