---
title: "安裝 Analysis Services 資料提供者 (AMO、 ADOMD.NET、 MSOLAP) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd6aa812228cce132b4180a8537ba853f3ea92a2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>安裝 Analysis Services 資料提供者 (AMO、ADOMD.NET、MSOLAP)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 是 Analysis Services 資料提供者 (包含 ADOMD.Net、AMO 和 MSOLAP) 的版本更新。  
  
 在大部分查詢資料存取案例中，您可以使用用戶端系統上已安裝的現有舊版資料提供者來存取 SQL Server 2016 Analysis Services 執行個體上的表格式和多維度模型 (包括使用 SQL Server 2016 專屬功能的表格式模型)。 存取 Analysis Services 模型時，可產生查詢的用戶端應用程式 (例如 Excel、Reporting Services 或 Tableau) 一般應該不需要最新的資料提供者。  
  
 至少根據資料提供者的版本需求，模型和系統管理工具是此規則的例外情況。 這些工具必須有特別針對目標伺服器所建置的資料提供者，才能操作該伺服器上的物件。 幸運的是， [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 所隨附的工具會自動包含符合目前伺服器版本的資料提供者。  SQL Server Data Tools for Visual Studio 2015 安裝程式會安裝 SQL Server 2016 Analysis Services 的資料提供者。 同樣地，SQL Server 2016 Management Studio (同時使用 AMO 和 ADOMD.Net) 會安裝目標設為 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的這兩個資料提供者。  
  
 呼叫資料提供者手動安裝的其中一個案例是使用 Analysis Services 管理物件 (AMO) 的自訂應用程式或指令碼。 此版本引進重構命名空間，以將主要物件 (例如 Server 和 Database) 移至為 Microsoft.AnalysisServices.dll 組件一部分的新命名空間 (Microsoft.AnalysisServices.Core)。 如果您有使用 AMO 的自訂程式碼或指令碼，則需要重新編譯程式碼，以及手動更新每個伺服器和用戶端工作站上的 AMO，來透過 AMO 直接連接至 SQL Server 2016 Analysis Services 執行個體。  
  
## <a name="provider-list"></a>提供者清單  
 下表描述每一個提供者。  
  
||||  
|-|-|-|  
|提供者|檔名|版本|  
|Analysis Services 管理物件 (AMO)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services 核心|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services (ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|OLE DB Provider for Analysis Services (MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>下載並安裝資料提供者  
  
1.  移至 [SQL Server 2016 的功能套件下載頁面](http://go.microsoft.com/fwlink/?LinkID=398150)。  
  
2.  按一下 [下載]  啟用個別元件的安裝。  
  
3.  針對 64 位元電腦，選取下列所有或部分項目 (否則，選擇 x86 對等項目)：  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  按一下 [下一步]  下載檔案。  
  
5.  執行每個程式來安裝提供者。 ADO.MD 和 AMO 組件安裝在 C:\Windows\assembly\GAC_MSIL。 Analysis Services OLE DB 提供者安裝在 C:\Program Files\Microsoft Analysis Services\AS OLEDB\130。  
  
## <a name="verify-installation"></a>確認安裝  
  
1.  在檔案總管中，移至 C:\Windows\Assembly。  
  
2.  以滑鼠右鍵按一下 Microsoft.AnalysisServices，然後選取 [屬性]。  
  
3.  按一下 [版本]  確認您有最新的組建。  
  
  
