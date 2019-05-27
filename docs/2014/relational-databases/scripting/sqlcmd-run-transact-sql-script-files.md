---
title: 使用 sqlcmd 執行 Transact-SQL 指令碼檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a55800ff1d707ce191d373a7348bf744ce5886
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063670"
---
# <a name="run-transact-sql-script-files-using-sqlcmd"></a>使用 sqlcmd 執行 Transact-SQL 指令碼檔案
  您可以使用 `sqlcmd` 來執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案是一個文字檔，可以包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、`sqlcmd` 命令和指令碼變數的組合。  
  
 若要使用「記事本」建立簡單的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案，請遵循下列步驟：  
  
1.  按一下 [開始]，依序指向 [所有程式] 和 [附屬應用程式]，然後按一下 [記事本]。  
  
2.  將下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼複製並貼到 [記事本] 中：  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  將檔案儲存成 C 磁碟機中的 **myScript.sql** 。  
  
### <a name="to-run-the-script-file"></a>執行指令碼檔案  
  
1.  開啟 [命令提示字元] 視窗。  
  
2.  在 [命令提示字元] 視窗中輸入：`sqlcmd -S myServer\instanceName -i C:\myScript.sql`  
  
3.  按 ENTER 鍵。  
  
 此時會在命令提示字元視窗中，顯示一份 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 員工姓名和地址的清單。  
  
### <a name="to-save-this-output-to-a-text-file"></a>將這份輸出儲存在文字檔中  
  
1.  開啟 [命令提示字元] 視窗。  
  
2.  在 [命令提示字元] 視窗中輸入：`sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt`  
  
3.  按 ENTER 鍵。  
  
 此時在命令提示字元視窗中不會傳回任何輸出。 而是會將輸出送往 EmpAdds.txt 檔。 您可以開啟 EmpAdds.txt 檔來確認這份輸出。  
  
## <a name="see-also"></a>另請參閱  
 [啟動 sqlcmd 公用程式](sqlcmd-start-the-utility.md)   
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)  
  
  
