---
title: 移動 Analysis Services 資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- moving databases [Anlysis Services]
- moving databases
- operations [Analysis Services - multidimensional data]
ms.assetid: fa644e5d-e276-445e-98d9-673afcfb83fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0939540af0c302832925a7a1bef6367718b8c1be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699058"
---
# <a name="move-an-analysis-services-database"></a>移動 Analysis Services 資料庫
  通常在很多情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員 (dba) 會想要將多維度或表格式模型資料庫移至不同的位置。 這些情況通常是由商務需求所驅使，例如將資料庫移至不同的磁碟以提升效能、取得讓資料庫成長的空間，或升級產品。  
  
 您可以使用許多方式來移動資料庫。 本文件將說明下列常見狀況：  
  
-   以互動方式使用 SSMS  
  
-   以程式設計方式使用 AMO  
  
-   依據指令碼使用 XMLA  
  
 所有狀況都會要求使用者存取資料庫資料夾，以及使用某種方法，將檔案移至所需的最終目的地。  
  
> [!NOTE]  
>  如果您卸離資料庫但沒有指派密碼給它，就會讓資料庫處於不安全的狀態。 我們建議您指派密碼給資料庫，以便保護機密資訊。 此外，您應該將對應的存取安全性套用至資料庫資料夾、子資料夾和檔案，防止未經授權的人員存取這些項目。  
  
## <a name="procedures"></a>程序  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>以互動方式使用 SSMS 來移動資料庫  
  
1.  在 SSMS 的左窗格或右窗格中，找出要移動的資料庫。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取**卸離...**  
  
3.  將密碼指派給要卸離的資料庫，然後按一下 [確定] 執行卸離命令。  
  
4.  您可以使用任何作業系統機制或移動檔案的標準方法，將資料庫資料夾移至新的位置。  
  
5.  在 SSMS 的左窗格或右窗格中，找出 [資料庫] 資料夾。  
  
6.  以滑鼠右鍵按一下**資料庫**資料夾，然後選取**附加...**  
  
7.  在 [資料夾] 文字方塊中，輸入資料庫資料夾的新位置。 或者，您可以使用瀏覽按鈕 (**...**) 來找出資料庫資料夾。  
  
8.  選取`ReadWrite`資料庫模式。  
  
9. 輸入在步驟 3 中使用的密碼，然後按一下 [確定] 執行附加命令。  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>以程式設計方式使用 AMO 來移動資料庫  
  
1.  在您的 C# 應用程式中，改寫下列範例程式碼並完成指定的工作。  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  在您的 C# 應用程式中，使用必要的參數來叫用 `MoveDb()` 。  
  
2.  編譯並執行程式碼，以便移動資料庫。  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>依據指令碼使用 XMLA 來移動資料庫  
  
1.  在 SSMS 中開啟新的 XMLA 索引標籤。  
  
2.  複製下列 XMLA 指令碼範本：  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  將 `%dbName%` 取代成資料庫名稱，而將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
2.  執行 XMLA 命令。  
  
3.  您可以使用任何作業系統機制或移動檔案的標準方法，將資料庫資料夾移至新的位置。  
  
4.  將下列 XMLA 指令碼範本複製到新的 XMLA 索引標籤中：  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  將 `%dbFolder%` 取代成資料庫資料夾的完整 UNC 路徑、將 `%ReadOnlyMode%` 取代成對應的 `ReadOnly` 或 `ReadWrite` 值，並將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
2.  執行 XMLA 命令。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和卸離 Analysis Services 資料庫](attach-and-detach-analysis-services-databases.md)   
 [資料庫儲存位置](database-storage-location.md)   
 [資料庫 ReadWriteMode](database-readwritemodes.md)   
 [Attach 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Detach 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
