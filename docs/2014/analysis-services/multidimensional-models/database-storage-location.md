---
title: 資料庫儲存體位置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c62d463a424c1e5245a7b5f5a36e9d7a99fe7c9e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234248"
---
# <a name="database-storage-location"></a>資料庫儲存位置
  通常在很多情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員 (dba) 會想要讓特定資料庫放置於伺服器資料夾外部。 這些情況通常是由商務需求所驅使，例如改善效能或展開儲存體。 這些情況下，`DbStorageLocation`資料庫屬性可讓[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dba 在本機的磁碟或網路裝置中指定資料庫位置。  
  
## <a name="dbstoragelocation-database-property"></a>DbStorageLocation 資料庫屬性  
 `DbStorageLocation`資料庫屬性會指定其中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]建立和管理所有資料庫資料和中繼資料檔案。 所有的中繼資料檔案都會儲存在`DbStorageLocation`資料夾，但資料庫中繼資料檔案，它會儲存在伺服器資料夾除外。 設定的值時有兩個重要的考量`DbStorageLocation`資料庫屬性：  
  
-   `DbStorageLocation`資料庫屬性必須設現有的 UNC 資料夾路徑或空字串。 空字串是伺服器資料夾的預設值。 如果這個資料夾不存在，當您執行 `Create`、`Attach` 或 `Alter` 命令時，就會引發錯誤。  
  
-   `DbStorageLocation`資料庫屬性無法設定為指向伺服器資料夾或其子資料夾中的任何一個。 如果此位置指向伺服器資料夾或其中任何一個子資料夾，當您執行 `Create`、`Attach` 或 `Alter` 命令時，就會引發錯誤。  
  
> [!IMPORTANT]  
>  建議您將 UNC 路徑設定為使用存放區域網路 (SAN)、iSCSI 架構網路或附加於本機的磁碟。 任何網路共用的 UNC 路徑或任何高度延遲的遠端存放區方案，都會導致發生不支援的安裝。  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>DbStorageLocation 與 StorageLocation 的比較  
 `DbStorageLocation` 會指定所有資料庫資料和中繼資料檔案所在的資料夾，而 `StorageLocation` 則會指定一個或多個 Cube 資料分割所在的資料夾。 您可以在 `StorageLocation` 之外，獨立設定 `DbStorageLocation`。 這是根據預期結果的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 決策，而且這兩個屬性的使用方式將多次重疊。  
  
## <a name="dbstoragelocation-usage"></a>DbStorageLocation 使用方式  
 `DbStorageLocation`資料庫屬性用做為一部分`Create`資料庫中的命令`Detach` / `Attach`資料庫命令序列`Backup` / `Restore`資料庫命令序列或在`Synchronize`資料庫命令。 變更 `DbStorageLocation` 資料庫屬性會被視為資料庫物件中的結構性變更。 這表示，您必須重新建立所有中繼資料並重新處理資料。  
  
> [!IMPORTANT]  
>  您不應該使用 `Alter` 命令來變更資料庫儲存位置。 相反地，我們建議，您會使用一連串`Detach` / `Attach`資料庫命令 (請參閱[移動 Analysis Services 資料庫](move-an-analysis-services-database.md)，[附加與卸離 Analysis Services 資料庫](attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和卸離 Analysis Services 資料庫](attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](move-an-analysis-services-database.md)   
 [DbStorageLocation 元素](../xmla/xml-elements-properties/dbstoragelocation-element.md)   
 [建立項目&#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md)   
 [Attach 元素](../xmla/xml-elements-commands/attach-element.md)   
 [同步處理項目&#40;XMLA&#41;](../xmla/xml-elements-commands/synchronize-element-xmla.md)  
  
  
