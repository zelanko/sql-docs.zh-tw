---
title: SQL Server 單元測試檔案 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e23304a429b77bcb4a5fc6a4c1001f2f28cf7885
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093888"
---
# <a name="sql-server-unit-test-files"></a>SQL Server 單元測試檔案
如同受控碼的單元測試一樣，SQL Server 單元測試也位於測試專案中。 您可以在 [方案總管] 的測試專案階層架構中，看到組成 SQL Server 單元測試的項目。  
  
SQL Server 單元測試由多個項目組成，而這些項目又包含在數個檔案中。 下表描述這些彼此互動以形成 SQL Server 單元測試的檔案。  
  
|**檔案**|**說明**|  
|------------|-------------------|  
|.cs 或 .vb|這個原始程式碼檔案包含由 [TestClass] 屬性裝飾的類別。 這個類別則針對每個包含的 SQL Server 單元測試，包含單一測試方法。 這些方法使用 [TestMethod] 屬性裝飾。<br /><br />每個測試方法都包含適當的程式碼，以執行 Transact\-SQL 測試指令碼。 此指令碼會在測試方法建立時產生，而且可供修改。<br /><br />**注意**：如果在 [方案總管] 中按兩下這個檔案，測試類別會在 SQL Serve 單元測試設計工具中開啟。 若要開啟 .cs 或 .vb 檔案來檢視原始程式碼，請以滑鼠右鍵按一下 [方案總管] 中的檔案，然後按一下 [檢視程式碼]。|  
|.resx|這個資源檔包含為相關 .cs 或 .vb 檔案中的所有測試定義的 Transact\-SQL 指令碼。 這組指令碼包含測試前指令碼、測試指令碼和測試後指令碼。 資源檔包含可供編輯的 XML。 資源檔會編譯至測試組件內。<br /><br />您必須使用 [SQL Server 單元測試設計工具] 來編寫 Transact\-SQL 指令碼。 如需有關 SQL Server 單元測試中使用之指令碼的詳細資訊，請參閱 [SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)。|  
|app.config|這個檔案會儲存測試專案的資料庫連接字串，以及其他 SQL Server 單元測試組態設定，例如命令逾時。如需詳細資訊，請參閱 [SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)。|  
|SQLDatabaseSetup.cs 或 SQLDatabaseSetup.vb|這個檔案包含針對測試專案中所有 SQL Server 單元測試準備測試環境的類別。 根據 app.config 檔案中的組態設定，它可以將 SQL Server 資料庫專案部署至測試資料庫。|  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
