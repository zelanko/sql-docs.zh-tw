---
title: 在 Analysis Services 中設定伺服器屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c05bbc1be8376144eb191ff28a9cdc6eebdd8a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068894"
---
# <a name="configure-server-properties-in-analysis-services"></a>在 Analysis Services 中設定伺服器屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員可以修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的預設伺服器組態屬性。 每一個執行個體都有自己的組態屬性，可以在同一部伺服器上與其他執行個體分開設定。  
  
 若要設定伺服器屬性，請使用 SQL Server Management Studio，或是編輯特定執行個體的 msmdsrv.ini 檔。  
  
 本主題包含下列幾節：  
  
 [設定伺服器 (執行個體) 屬性](#bkmk_config)  
  
 [伺服器屬性參考](#bkmk_ref)  
  
##  <a name="configure-server-instance-properties"></a><a name="bkmk_config"></a>設定伺服器（實例）屬性  
 SQL Server Management Studio 中的屬性頁包含可用屬性的子集，其中只會顯示較可能修改的屬性。 完整的屬性集可以在 msmdsrv.ini 檔中找到。  
  
> [!NOTE]  
>  本主題沒有在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中記載部署組態屬性。 如需部署設定的詳細資訊，請參閱[指定解決方案部署的設定](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)。  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>在 Management Studio 中檢視或設定組態屬性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
     在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後按一下 [屬性]****。 [一般] 頁面隨即顯示，其中顯示最常使用的屬性。  
  
2.  若要檢視其他屬性，請按一下頁面底部的 [顯示進階 (全部) 屬性]**** 核取方塊。  
  
     只有表格式模式和多維度模式伺服器支援修改伺服器屬性。 如果您已安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，除非 Microsoft 產品支援工程師另有指示，否則請務必使用預設值。  
  
     如需如何透過伺服器屬性處理操作或效能問題的指示，請參閱＜ [SQL Server 2008 R2 Analysis Services 作業指南](https://go.microsoft.com/fwlink/?LinkID=225539)＞。  
  
     您也可以在此 Microsoft 技術白皮書 [SQL Server 2005 Analysis Services (SSAS) 伺服器屬性](https://go.microsoft.com/fwlink/?LinkID=199102)中閱讀有關伺服器屬性 (在最後幾個版本中大部分未變更) 的資訊。  
  
    > [!NOTE]  
    >  部分屬性只能在 msmdrsrv.ini 檔中設定。 如果即使在顯示進階屬性之後仍看不到您要設定的屬性，可能需要直接編輯 msmdsrv.ini 檔。  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>在 msmdsrv.ini 檔中檢視或編輯組態屬性  
  
1.  在開始進行之前，請先檢查 Management Studio 中 [一般] 屬性頁的 **[DataDir]** 屬性，以確認 Analysis Services 程式檔的位置，包括 msmdsrv.ini 檔。 確認程式檔的位置將可確保您修改的檔案是正確的。  
  
    > [!NOTE]  
    >  在預設安裝中，檔案位於 \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config 資料夾中  
  
2.  建立檔案的備份，以免需要還原原始檔案。  
  
3.  使用文字編輯器檢視或編輯 msmdsrv.ini 檔。  
  
4.  在您儲存檔案之後，必須重新啟動服務。  
  
##  <a name="server-property-reference"></a><a name="bkmk_ref"></a> 伺服器屬性參考  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態屬性對於微調您的系統而言很重要。 例如，若要使查詢記錄行為與您的需求一致，您可以設定相關屬性。  
  
 下列主題說明各種 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態屬性：  
  
|主題|描述|  
|-----------|-----------------|  
|[一般屬性](general-properties.md)|一般屬性是基本和進階屬性，並且包含定義資料目錄、備份目錄和其他伺服器行為的屬性。|  
|[資料採礦屬性](data-mining-properties.md)|資料採礦屬性控制要啟用和停用哪些資料採礦演算法。 依預設，會啟用所有的演算法。|  
|DSO|不再支援 DSO。 DSO 屬性會遭到忽略。|  
|[功能屬性](feature-properties.md)|與產品功能有關的功能屬性，大部分是進階屬性，包含控制伺服器執行個體間之連結的屬性。|  
|[[內容] 屬性](filestore-properties.md)|檔案存放區屬性僅供進階使用。 其中包含進階記憶體管理設定。|  
|[鎖定管理員屬性](lock-manager-properties.md)|鎖定管理員屬性定義與鎖定和逾時有關的伺服器行為。 這些屬性大部分僅供進階使用。|  
|[記錄屬性](log-properties.md)|記錄屬性控制在伺服器上是否記錄事件、記錄於何處以及如何記錄。 這包含錯誤記錄、例外狀況記錄、飛行記錄器、查詢記錄和追蹤。|  
|[記憶體屬性](memory-properties.md)|記憶體屬性控制伺服器如何使用記憶體。 這些屬性主要是供進階使用。|  
|[網路屬性](network-properties.md)|網路屬性控制與網路有關的伺服器行為，包含控制壓縮和二進位 XML 的屬性。 這些屬性大部分僅供進階使用。|  
|[OLAP 屬性](olap-properties.md)|OLAP 屬性控制 Cube 和維度處理、延遲處理、資料快取，以及查詢行為。 這些包含基本和進階屬性。|  
|[安全性屬性](security-properties.md)|安全性區段包含定義存取權限的基本和進階屬性。 這包含與管理員和使用者有關的設定。|  
|[執行緒集區屬性](thread-pool-properties.md)|執行緒集區屬性控制伺服器會建立多少執行緒。 這些屬性主要是進階屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 實例管理](../instances/analysis-services-instance-management.md)   
 [指定方案部署的組態設定](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
