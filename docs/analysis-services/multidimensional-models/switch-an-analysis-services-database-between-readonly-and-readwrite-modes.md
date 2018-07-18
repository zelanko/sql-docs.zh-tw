---
title: 切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0df164b267043e4784260b30b039ecb58c2c4cc7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026725"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>在 ReadOnly 和 ReadWrite 模式之間切換 Analysis Services 資料庫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員可以變更表格式或多維度資料庫的讀寫模式，以便將查詢工作負載分散於多部僅供查詢的伺服器。  
  
 您可以使用多種方式來切換資料庫模式。 本文件將說明下列常見狀況：  
  
-   以互動方式使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   以程式設計方式使用 AMO  
  
-   使用 XMLA 或 TMSL 的指令碼  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>以互動方式使用 Management Studio 來切換資料庫的讀取/寫入模式  
  
1.  在物件總管中，以滑鼠右鍵按一下資料庫，然後選取 [屬性]。  
  
     記下位置。 空白的資料庫儲存位置是表示該資料庫資料夾位於伺服器資料中。  
  
2.  以滑鼠右鍵按一下該資料庫，然後選取 [卸離…]  
  
3.  將密碼指派給要卸離的資料庫，然後按一下 [確定] 執行卸離命令。  
  
4.  在物件總管中，以滑鼠右鍵按一下 [資料庫] 資料夾，然後選取 [附加…]  
  
5.  在 [資料夾] 文字方塊中，輸入資料庫資料夾的原始位置。 或者，您也可以使用瀏覽按鈕 (**…**) 來找出資料庫資料夾。  
  
6.  選取資料庫的讀取/寫入模式。  
  
7.  輸入密碼，然後按一下 [確定] 執行附加命令。  
  
## <a name="switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>以程式設計方式使用 AMO 來切換資料庫的讀取/寫入模式  
 在您的 C# 應用程式中，使用必要的參數來叫用 `SwitchReadWrite()` 。 編譯並執行程式碼，以便移動資料庫。  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## <a name="switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>使用 XMLA 有指令碼切換資料庫的讀取/寫入模式  
 下列指示適用於相容性模式 1050、1100 或 1103 的多維度資料庫和表格式資料庫。  
  
1.  在物件總管中，以滑鼠右鍵按一下資料庫，然後選取 [屬性]。  
  
     記下位置。 空白的資料庫儲存位置是表示該資料庫資料夾位於伺服器資料中。  
  
2.  以滑鼠右鍵按一下該資料庫，然後選取 [卸離…]  
  
3.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中開啟新的 XMLA 索引標籤。  
  
4.  複製下列 XMLA 指令碼範本：  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  將 `%dbName%` 取代成資料庫名稱，而將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
6.  執行 XMLA 命令。  
  
7.  將下列 XMLA 指令碼範本複製到新的 XMLA 索引標籤中：  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  將 `%dbFolder%` 取代成資料庫資料夾的完整 UNC 路徑、將 `%ReadOnlyMode%` 取代成對應的 **ReadOnly** 或 **ReadWrite**值，並將 `%password%` 取代成密碼。 % 字元屬於範本的一部分，而且您必須移除這些字元。  
  
9. 執行 XMLA 命令。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 的高可用性與延展性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [附加和卸離 Analysis Services 資料庫](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [資料庫儲存位置](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [資料庫 Readwritemode](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Attach 元素](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Detach 元素](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode 元素](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation 元素](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  
