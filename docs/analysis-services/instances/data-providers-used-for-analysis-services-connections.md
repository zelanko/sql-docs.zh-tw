---
title: 用於 Analysis Services 連接的資料提供者 |Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057846"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>使用 Analysis services 連接的用戶端程式庫 （資料提供者）
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 會提供三個用戶端程式庫，也稱為**資料提供者**、 伺服器和資料存取工具和用戶端應用程式。 SSMS 和 SSDT 中，例如 Power BI Desktop 和 Excel 連接到 Analysis Services 使用這些程式庫的應用程式之類的工具。 兩個用戶端程式庫，ADOMD.NET 和 Analysis Services 管理物件 (AMO)，是受管理的用戶端程式庫。 Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。 用戶端程式庫也適用於 SQL Server Analysis Services 和 Azure Analysis Services。
  
##  <a name="bkmk_downloadsite"></a> 何處可取得較新版本  
 用戶端電腦上安裝的版本應該符合提供之資料的伺服器主要版本。 如果伺服器安裝比網路中工作站上安裝的資料提供者還要新，您可能需要安裝較新版的程式庫。  

包含在舊版的 SQL Server Feature Pack 的用戶端程式庫對應至該 SQL 版本;不過，它們可能無法最新版本。 連線到 Azure Analysis Services，可能需要更新的版本。 所有版本都都具有回溯相容性。

若要取得最新版本，請參閱[連接到 Azure Analysis Services 的用戶端程式庫](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
