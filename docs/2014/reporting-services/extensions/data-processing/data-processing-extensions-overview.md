---
title: 資料處理延伸模組概觀 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 14ec583360509be356aa12751c0a090b2a7dc676
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191688"
---
# <a name="data-processing-extensions-overview"></a>資料處理延伸模組概觀
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的資料處理延伸模組，可讓您連接到資料來源並擷取資料。 它們也可當做資料來源與資料集之間的橋樑。 因為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組是依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者介面子集建立的。  
  
 下表列出 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 隨附的資料處理延伸模組。  
  
|資料處理延伸模組|描述|  
|-------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的資料處理延伸模組|使用 .NET Framework Data Provider for SQL Server 來連線和擷取 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 的資料。|  
|OLE DB 的資料處理延伸模組|使用 .NET Framework Data Provider for OLE DB。 透過這個延伸模組，報表伺服器可以查詢具有 OLE DB 提供者的資料來源。|  
|Oracle 的資料處理延伸模組|使用 .NET Framework Data Provider for Oracle。 透過這個延伸模組，報表伺服器可以藉由 Oracle 用戶端連接軟體存取 Oracle 資料來源。|  
|ODBC 的資料處理延伸模組|使用 .NET Framework Data Provider for ODBC。 透過這個延伸模組，報表伺服器可以存取具有 ODBC 驅動程式之資料庫中的資料。|  
  
 您可以使用 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 資料處理 API 將自訂資料處理加入報表伺服器。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 為 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中的資料提供者提供了內建支援。 如果您已實作完整的資料提供者，就不需要實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組。 不過，您應該考慮擴充資料提供者，使其得以涵蓋 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005 的特定功能，例如安全的連接認證與伺服器端的彙總。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 隨附的每個資料處理延伸模組會使用一組共用的介面。 這可確保每個延伸模組都會實作可比較的功能。  
  
 您可以為自己的資料來源開發資料處理延伸模組，或使用介面來將其他資料處理層加入共同的資料庫基礎結構。 您可以部署自訂資料處理延伸模組，以將資料緊密整合到組織中的現有報表伺服器。 這些自訂資料處理延伸模組也可以做為提供給客戶之自訂報表套件的一部分。  
  
 ![資料處理延伸模組架構](../../media/bk-dataprocess-extensions.gif "資料處理延伸模組架構")  
Reporting Services 資料處理延伸模組架構  
  
 實作自訂 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組有下列幾項優點：  
  
-   簡化資料存取架構，通常可提供較佳的可維護性與更高的效能。  
  
-   直接向取用者公開延伸模組特定功能。  
  
-   提供取用者特定介面，供其存取 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的資料來源。  
  
## <a name="data-extension-process-flow"></a>資料延伸模組處理流量  
 開發自訂資料延伸模組之前，應該先了解報表伺服器如何使用資料延伸模組處理資料， 並熟悉報表伺服器呼叫的建構函式與方法。  
  
 ![資料處理延伸模組的處理流程](../../media/bk-ext-01.gif "資料處理延伸模組的處理流程")  
報表伺服器呼叫的資料延伸模組之逐步處理流程  
  
 圖例中顯示了下列事件的順序：  
  
1.  報表伺服器會建立連接物件，並傳遞與報表關聯的連接字串與認證。  
  
2.  報表的命令文字會用以建立命令物件。 在程序中，資料處理延伸模組可能包含剖析命令文字以及為命令建立任何參數的程式碼。  
  
3.  處理命令物件與任何參數之後，就會產生資料讀取器，以傳回結果集並允許報表伺服器將報表資料與報表配置相關聯。  
  
## <a name="developer-requirements"></a>開發人員需求  
 若要開發 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組，您需要：  
  
-   已安裝報表設計師或報表伺服器的部署電腦。  
  
-   安裝 [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] 或以上版本，或是 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 軟體開發套件 (SDK) 的開發電腦。  
  
-   對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的特性與功能有深入的了解。  
  
-   對 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 架構、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者、ADO.NET DataSet 物件以及常用的 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 介面有深入的了解。  
  
-   [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 語言的開發體驗，例如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 或是 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
