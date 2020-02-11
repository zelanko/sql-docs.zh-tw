---
title: 定義連結維度 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: d5ad5eae-5dde-46a6-91c3-c8766d016dec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca4b3c0b2f2a6c63e62a44499d6e33e651ca9bae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075580"
---
# <a name="define-linked-dimensions"></a>定義連結維度
  連結維度是根據在相同版本與相容性層級的另一個 Analysis Services 資料庫中所建立和儲存的維度。 藉由使用連結維度，您可以在一個資料庫上建立、儲存和維護維度，同時將該維度提供給多個資料庫的使用者使用。 對於使用者來說，連結維度和其他任何維度看起來都一樣。  
  
 連結維度是唯讀的。 若您想修改維度或建立新的關聯性，則必須變更來源維度，然後刪除並重新建立連結維度和其關聯性。 您無法重新整理連結維度來收集來源物件中的變更。  
  
 所有相關的量值群組與維度，必須來自相同的來源資料庫。 您無法建立本機量值群組和您加入 Cube 的連結維度之間的新關聯性。 將連結維度與量值群組加入目前的 Cube 之後，必須在它們的來源資料庫中維護兩者間的關聯性。  
  
> [!NOTE]  
>  因為無法使用重新整理，所以大多數的 Analysis Services 開發人員都會複製維度而不是連結維度。 您可以在相同方案內複製不同專案中的維度。 如需詳細資訊，請參閱 [Refresh of a linked dimension in SSAS](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx)(在 SSAS 中重新整理連結維度)。  
  
## <a name="prerequisites"></a>Prerequisites  
 提供維度的來源資料庫和使用該維度的目前資料庫都必須具有相同的版本和相容性層級。 如需詳細資訊，請參閱[將多維度資料庫的相容性層級設定 &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
 來源資料庫必須已部署並處於線上。 您必須將發行或取用連結物件的伺服器設定為允許該作業 (如下所示)。  
  
 您所要使用的維度本身不能是連結維度。  
  
## <a name="configure-server-to-allow-linked-objects"></a>將伺服器設定為允許連結物件  
  
1.  在 SQL Server Management Studio 中，連接到 Analysis Services 伺服器。 在 [物件總管] 中，以滑鼠右鍵按一下伺服器名稱，然後選取 [Facet]****。  
  
2.  將 **LinkedObjectsLinksFromOtherInstancesEnabled** 設定為 **True** ，允許伺服器發出在其他執行個體上執行之資料庫的連結物件要求。  
  
3.  將 **LinkedObjectsLinksToOtherInstances** 設定為 **True** ，允許伺服器要求資料連結於在其他執行個體上執行的資料庫。  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中建立連結維度  
  
1.  啟動精靈。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，以滑鼠右鍵按一下 ** 資料庫或專案中的 [維度]**[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料夾，然後按一下 [新增連結維度]****。  
  
2.  連接至提供維度的 Analysis Services 資料庫。 在連結物件精靈會的 [選取資料來源]**** 頁面上，選擇 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源或建立新的資料來源。  
  
3.  在精靈的 [選取物件]**** 頁面上，選擇您要在遠端資料庫中連結的維度。  
  
4.  在 [正在完成精靈]**** 頁面上，您可以預覽連結物件。 如果您連結的維度與已存在的維度具有相同名稱，則會在名稱後附加序號 (第一個重複的名稱會從 '1' 開始)。 當您完成精靈時，維度會加入至 [維度]**** 資料夾。  
  
##  <a name="bkmk_CreateNew"></a>建立與 Analysis Services 資料庫的新資料來源連接  
 使用 [建立新的資料來源] 精靈，以將提供維度之 Analysis Services 資料庫相關資訊加入您的專案連接。 您可以在 [連結物件精靈] 中的 [選取資料來源] 頁面上，按一下 [新增資料來源]**** 以啟動精靈。  
  
1.  在 [資料來源精靈] 中的 [選取如何定義連接] 頁面上，按一下 [新增]****。  
  
2.  在 [連線管理員] 中，確認提供者是否設定為 **Native OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0**。  
  
3.  輸入伺服器的名稱（使用指定實例的*servername*\\*instancename* ）<sup>1</sup> ，或鍵入**localhost**來連接到在同一部電腦上執行的 Analysis Services 伺服器。  
  
4.  使用連接的 Windows 驗證。  
  
5.  在 [初始目錄]**** 中，按一下向下鍵選取此伺服器上的資料庫。  
  
6.  在 [資料來源精靈] 中，按一下 [下一步]**** 繼續。  
  
7.  在 [模擬資訊] 頁面上，按一下 [使用服務帳戶]****。 按一下 [下一步]**** 以完成精靈。 [連結物件精靈] 即會選取您所定義的連接。  
  
## <a name="next-steps"></a>後續步驟  
 您不能變更連結維度的結構，所以無法使用維度設計師的 [維度結構]**** 索引標籤來檢視它。 處理連結維度之後，您可以使用 [**瀏覽器**] 索引標籤來查看它。您也可以變更其名稱，並建立名稱的翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [將多維度資料庫的相容性層級設定 &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [連結量值群組](linked-measure-groups.md)   
 [維度關聯性](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
