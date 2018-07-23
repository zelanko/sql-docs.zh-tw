---
title: 疑難排解 SQL Server 資料庫單元測試的問題 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf4c9cd1-7e73-4c3b-922a-68b9247e7b33
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0fa8e6a9e4d23c74a6908d645d422b37db1f7f36
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088450"
---
# <a name="troubleshooting-sql-server-database-unit-testing-issues"></a>疑難排解 SQL Server 資料庫單元測試的問題
搭配資料庫使用 SQL Server 單元測試時，您可能會遇到本主題所述的問題：  
  
-   [執行單元測試後，單元測試以及 App.Config 的變更遭到忽略](#UnitTestingAndAppConfigChanges)  
  
-   [執行單元測試後，資料庫部署至非預期的目標](#DatabaseDeploymentInUnitTests)  
  
-   [執行資料庫單元測試發生逾時](#TimeoutsDuringUnitTests)  
  
## <a name="UnitTestingAndAppConfigChanges"></a>執行單元測試後，單元測試以及 App.Config 的變更遭到忽略  
如果您已修改測試專案中的 App.Config 檔案，就必須重建測試專案，這些變更才會生效， 其中包括了使用 [SQL Server 測試組態] 對話方塊對 App.Config 所做的變更。 若您並未重建測試專案，執行單元測試時便不會套用任何變更。  
  
## <a name="DatabaseDeploymentInUnitTests"></a>執行單元測試後，資料庫部署至非預期的目標  
如果您是從執行單元測試的資料庫專案來部署資料庫，該資料庫將會使用單元測試組態中所指定的連接字串資訊進行部署。 這項作業並未採用資料庫專案的 [偵錯] 屬性所指定的連接資訊，以便讓您能夠對同一個資料庫的不同執行個體執行 SQL Server 單元測試。  
  
## <a name="TimeoutsDuringUnitTests"></a>執行資料庫單元測試發生逾時  
如果資料庫單元測試因為逾時而失敗，您可以藉由更新測試專案中的 app.config 檔案來延長逾時期限。 連接字串所定義的連接逾時是指定可等候多久讓單元測試連接至伺服器。 命令逾時則必須直接在 app.config 檔案中定義，其值指定了等候單元測試執行 Transact\-SQL 指令碼的時間。 如果您遇到執行單元測試時間過長的問題，請嘗試在適當的內容項目中增加命令逾時值。 例如，藉由更新 app.config 將 **PrivilegedContext** 項目的命令逾時指定為 120 秒，如下所示：  
  
```  
<SqlUnitTesting_VS2010>  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\..\..\..\Visual Studio 2010\Projects\Database10\Database10\AdventureWorks.sqlproj"  
        Configuration="Debug" />  
    <DataGeneration ClearDatabase="true" />  
    <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="30" />  
    <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="120" />  
</SqlUnitTesting_VS2010>  
```  
  
## <a name="see-also"></a>另請參閱  
[如何：建立函式、觸發程序和預存程序的 SQL Server 單元測試](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
