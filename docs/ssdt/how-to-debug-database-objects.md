---
title: 如何：對資料庫物件進行偵錯 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7379c550b8bcf9ac18b1e7590bad8a10bdc83f3c
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093879"
---
# <a name="how-to-debug-database-objects"></a>HOW TO：偵錯資料庫物件
SQL Server 單元測試是由以下項目組成：  
  
-   以 Visual C\# 或 Visual Basic 撰寫的單元測試程式碼。 此程式碼是由 SQL Server 單元測試設計工具產生，負責提交構成測試本文的 Transact\-SQL 指令碼。  
  
-   以 Visual C \#或 Visual Basic 撰寫的一或多個測試條件。 若要對測試條件進行偵錯，請遵循對單元測試進行偵錯的程序來進行，如[如何：在執行測試時偵錯 (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182484(VS.100).aspx) \(機器翻譯\) 或[如何：在執行測試時偵錯 (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182484.aspx) \(機器翻譯\) 中所述。  
  
-   一個或多個 Transact\-SQL 指令碼 (這些指令碼會在您要測試之資料庫的物件上執行)。 您無法對這些 Transact\-SQL 指令碼進行偵錯。  
  
本主題的程序描述如何針對所測試的資料庫中特定的資料庫物件 (如預存程序、函式和觸發程序) 進行偵錯。 若要偵錯資料庫物件，請依照以下順序來執行這些程序：  
  
1.  在您的測試專案上啟用 SQL Server 偵錯。  
  
2.  在裝載您要測試之資料庫的 SQL Server 執行個體上啟用應用程式偵錯。  
  
3.  針對您要偵錯的資料庫物件，在其 Transact\-SQL 指令碼內設定中斷點。  
  
4.  偵錯單元測試。 在此程序中，您會在偵錯模式中執行測試。  
  
### <a name="to-enable-sql-debugging-on-your-test-project"></a>若要在測試專案上啟用 SQL 偵錯  
  
1.  開啟 [方案總管]。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下測試專案，然後按一下 [屬性]。  
  
    與測試專案同名的屬性頁面隨即開啟。  
  
3.  在屬性頁面上，按一下 [偵錯]。  
  
4.  在 [啟用偵錯工具] 下，按一下 [啟用 SQL Server 偵錯]。  
  
5.  儲存變更。  
  
### <a name="to-set-an-increased-execution-context-timeout-to-enable-debugging-for-your-test-project"></a>若要設定延長執行內容逾時來啟用測試專案的偵錯  
  
1.  在 [檔案] 功能表上，指向 [開啟]，然後按一下 [檔案]。  
  
2.  瀏覽至包含測試專案的資料夾，然後按兩下 app.config 檔案。  
  
    app.config 檔案就會在編輯器中開啟。  
  
3.  修改 ExecutionContext 節點來加入命令逾時，如下列範例所示：  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  儲存變更。  
  
5.  重建單元測試專案。  
  
> [!IMPORTANT]  
> 如果您不重建專案，則當您執行單元測試時，不會套用您對 app.config 所做的變更，而且偵錯會失敗。  
  
### <a name="to-add-breakpoints-to-your-transact-sql-script"></a>將中斷點新增至您的 Transact\-SQL 指令碼  
  
1.  在 [檢視] 功能表上，開啟 [SQL Server 物件總管]。  
  
2.  在 [資料連接] 底下，展開您要測試之資料庫的節點。  
  
3.  如果資料庫的圖示旁邊有出現一個小型的紅色 'x'，則表示該資料庫的連接已關閉。 在此情況下，請以滑鼠右鍵按一下該資料庫，然後按一下 [重新整理]。 您可能必須提供認證，才能開啟此資料庫的連接。  
  
4.  展開 [檢視表]、[預存程序] 或 [函式] 節點，以尋找您要偵錯的物件。  
  
5.  按兩下您要偵錯的物件。  
  
6.  按一下灰色提要欄位，即可設定中斷點。  
  
### <a name="to-debug-your-sql-server-unit-test"></a>對您的 SQL Server 單元測試進行偵錯  
  
1.  在 Visual Studio 2010 中，開啟 ([測試] -> [視窗]) [測試檢視] 視窗。 在 Visual Studio 2012 中，開啟 [測試總管] 視窗。  
  
2.  以滑鼠右鍵按一下測試 (其 Transact\-SQL 指令碼運用您已設定中斷點的資料庫物件)，然後選取 [偵錯選取範圍]。  
  
    這項測試會在偵錯模式中執行，直到遇到資料庫物件內的中斷點為止。  
  
3.  (選擇性) 若要開啟另一個偵錯視窗，請開啟 [偵錯] 功能表，指向 [視窗]，然後按一下 [中斷點]、[輸出] 或 [即時運算]。  
  
## <a name="see-also"></a>另請參閱  
[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)  
[偵錯 Transact-SQL (Visual Studio 2010)](http://go.microsoft.com/fwlink/?LinkId=163975)  
  
