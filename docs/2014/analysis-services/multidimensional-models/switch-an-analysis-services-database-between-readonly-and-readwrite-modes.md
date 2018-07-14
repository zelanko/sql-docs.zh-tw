---
title: 切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫 |Microsoft Docs
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
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb0d9ae239d33cd55d50e0e876df1584ff2fe965
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286104"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>在 ReadOnly 和 ReadWrite 模式之間切換 Analysis Services 資料庫
  通常很多情況下當[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫管理員 (dba) 想要變更表格式或多維度資料庫的讀取/寫入模式。 這些情況通常是由商務需求所驅使，例如在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器集區之間共用資料庫，以便改善使用者經驗。  
  
 您可以使用許多方式來切換資料庫模式。 本文件將說明下列常見狀況：  
  
-   以互動方式使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   以程式設計方式使用 AMO  
  
-   依據指令碼使用 XMLA  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>以互動方式使用 Management Studio 來切換資料庫的讀取/寫入模式  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的左窗格或右窗格中，找出要切換的資料庫。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取**屬性**。 尋找資料庫資料夾並記下位置。 空白的資料庫儲存位置是表示該資料庫資料夾位於伺服器資料中。  
  
    > [!IMPORTANT]  
    >  一旦資料庫卸離之後，[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 便無法再協助您取得資料庫位置。  
  
3.  以滑鼠右鍵按一下該資料庫，然後選取 [卸離…]  
  
4.  將密碼指派給要卸離的資料庫，然後按一下 [確定] 執行卸離命令。  
  
5.  找出**資料庫**的左或右窗格中的資料夾[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
6.  以滑鼠右鍵按一下**資料庫**資料夾，然後選取**附加...**  
  
7.  在 [資料夾] 文字方塊中，輸入資料庫資料夾的原始位置。 或者，您也可以使用瀏覽按鈕 (**…**) 來找出資料庫資料夾。  
  
8.  選取資料庫的讀取/寫入模式。  
  
9. 步驟 3 中輸入所用的密碼，然後按一下**確定**執行 attach 命令。  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>以程式設計方式使用 AMO 來切換資料庫的讀取/寫入模式  
  
1.  在您的 C# 應用程式中，改寫下列範例程式碼並完成指定的工作。  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  在您的 C# 應用程式中，使用必要的參數來叫用 `SwitchReadWrite()` 。  
  
2.  編譯並執行程式碼，以便移動資料庫。  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>依據指令碼使用 XMLA 來切換資料庫的讀取/寫入模式  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的左窗格或右窗格中，找出要切換的資料庫。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取**屬性**。 尋找資料庫資料夾並記下位置。 空白的資料庫儲存位置是表示該資料庫資料夾位於伺服器資料中。  
  
    > [!IMPORTANT]  
    >  一旦資料庫卸離之後，[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 便無法再協助您取得資料庫位置。  
  
3.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中開啟新的 XMLA 索引標籤。  
  
4.  複製下列 XMLA 指令碼範本：  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  將 `%dbName%` 取代成資料庫名稱，而將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
2.  執行 XMLA 命令。  
  
3.  將下列 XMLA 指令碼範本複製到新的 XMLA 索引標籤中：  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  將 `%dbFolder%` 取代成資料庫資料夾的完整 UNC 路徑、將 `%ReadOnlyMode%` 取代成對應的 `ReadOnly` 或 `ReadWrite` 值，並將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
2.  執行 XMLA 命令。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和卸離 Analysis Services 資料庫](attach-and-detach-analysis-services-databases.md)   
 [資料庫儲存位置](database-storage-location.md)   
 [資料庫 Readwritemode](database-readwritemodes.md)   
 [Attach 元素](../xmla/xml-elements-commands/attach-element.md)   
 [Detach 元素](../xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode 元素](../xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation 元素](../xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  
