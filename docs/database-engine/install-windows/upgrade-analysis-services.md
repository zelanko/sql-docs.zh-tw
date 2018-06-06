---
title: 升級 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 235ed4172275df440f86df47d72f9eed0a1f0a5d
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34772584"
---
# <a name="upgrade-analysis-services"></a>升級 Analysis Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Analysis Services 執行個體可以升級至相同伺服器模式的 SQL Server 版本，以利用目前版本中所採用的功能，如 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)中所述。  
  
 您可以就地升級每個執行個體，相同硬體上執行的執行個體皆與其他執行個體無關。 但大部分的系統管理員會為應用程式測試選擇安裝新版本的新執行個體，然後再對新的伺服器傳輸實際執行的工作負載。 但是對於開發或測試伺服器而言，就地升級就可能會比較方便。  
  
## <a name="server-upgrade"></a>伺服器升級  
 升級伺服器與資料庫有兩種基本方法︰  
  
> [!NOTE]
> 除非手動變更連結至指定伺服器的資料庫之相容性層級，否則這些層級會維持不變。
   
  
### <a name="in-place-upgrade"></a>就地升級  
 升級程序會自動將現有的資料庫從舊的執行個體移轉至新的執行個體。 由於這兩個版本之間的中繼資料和二進位資料是相容的，所以在您升級之後將會保留資料，而且不必手動移轉資料。  
  
 若要升級現有的執行個體，請執行安裝程式，並指定現有執行個體的名稱做為新執行個體的名稱。  
  
### <a name="side-by-side-upgrade"></a>並存升級  
  
-   備份所有資料庫，並確認每個資料庫皆可還原。 若要深入了解，請參閱[備份與還原 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
-   找出報表、試算表或儀表板快照集的子集，以供日後用作為確認升級後伺服器作業的基礎。 請在可能的情況下收集效能測量，如此即可在升級的伺服器上針對相同的工作負載進行比較。  
  
-   安裝 Analysis Services 的新執行個體，選擇和您要取代的伺服器相同之伺服器模式 (表格式或多維度)。 
  
     請遵循安裝後續工作，設定連接埠及新增伺服器管理員。 若要深入了解，請參閱[後續安裝組態 &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)。  
  
-   附加或還原每個資料庫。  
  
-   執行 DBCC 以檢查資料庫完整性。 表格式模型會進行更徹底地檢查，會測試整個模型階層中是否有孤立的物件。 若是多維度模型，就只會檢查分割區索引。 若要深入了解，請參閱[適用於 Analysis Services 表格式和多維度資料庫資料庫的一致性檢查程式 &#40;DBCC&#41;](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)。  
  
-   確認行為或計算是否有任何不良變更的測試報表、試算表與儀表板 您應會發現多維度與表格式工作負載的效能更佳。  
  
-   測試處理作業、更正任何登入或權限問題。 如果使用預設服務帳戶進行連線，新的服務會以不同的帳戶執行。 若要深入了解，請參閱[設定服務帳戶 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。  
  
-   在升級的伺服器上測試備份與還原作業，調整指令碼以使用新的伺服器名稱。  
  
## <a name="database-upgrade"></a>資料庫升級  
 在舊版中建立的資料庫會在使用原相容性層級設定的升級伺服器上執行。 一般而言，您可以升級資料庫或模型到更高的相容性層級以存取新功能，但請注意，如此做會將您繫結至特定的伺服器版本。  
  
 若要升級資料庫，通常會升級 SQL Server Data Tools (SSDT) 中的模型，然後再將解決方案部署到已升級的伺服器執行個體。
  
 表格式與多維度資料庫走不同的版本路徑。 但多維度與表格式模型都有相同編號的相容性層級。  如果功能變更只影響其中一個模式，則模式會上升至不同的費率。  
  
 由於背景的不同，下表摘要說明相容性層級；請檢閱詳細文章以了解每個層級所提供的功能。  
  
||||  
|-|-|-|  
|表格式|1400|SQL Server 2017|
|表格式|1200|SQL Server 2016|  
|表格式|1103|SQL Server 2014|  
|表格式|1100|SQL Server 2012|  
|多維度|1100|SQL Server 2012 及更新版本|  
|多維度|1050|SQL Server 2005、2008、2008 R2|  
  
 若要深入了解，請參閱[多維度資料庫的相容性層級 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) 和 [Analysis Services 表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升級 Power Pivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
  
