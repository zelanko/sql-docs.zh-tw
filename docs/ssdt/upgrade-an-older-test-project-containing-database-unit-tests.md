---
title: 升級包含資料庫單元測試的舊版測試專案 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02978a329399612e22e952ff6c0be6201c48d32e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715062"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>升級包含資料庫單元測試的舊版測試專案
您可以升級在 Visual Studio 2010 中建立且包含資料庫單元測試的舊版測試專案，以使用新的 SQL Server Data Tools 資料庫單元測試執行階段和工具。 升級舊版專案之後，您可以將 SQL Server 單元測試加入至專案 (如需詳細資訊，請參閱[建立並定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md))。  
  
> [!TIP]  
> 如果您要使用 Visual Studio 2010，將 SQL Server 單元測試加入至測試專案之後，就不應該使用舊版資料庫單元測試範本加入單元測試。 如果這麼做，需要再次轉換專案，才能正確執行測試。  
  
如果您有 Visual Studio 2010 以前版本所建立的測試資料庫專案，可以使用 [如何：從舊版 Visual Studio 升級資料庫單元測試](http://msdn.microsoft.com/library/dd193412(VS.100).aspx)中的資訊，將資料庫專案升級至 Visual Studio 2010，然後再將專案升級至 SQL Server Data Tools。  
  
### <a name="initiating-an-upgrade"></a>起始升級  
  
-   您可以從測試專案的內容功能表啟動專案升級。  
  
    在某些情況下，SQL Server Data Tools 會顯示對話方塊，讓您起始測試專案升級。  
  
-   升級專案會移除舊版資料庫測試架構的組件參考，並加入新架構和配接器組件的參考。 app.config 檔案也會更新。  
  
    > [!NOTE]  
    > 如果您的測試專案有 DatabaseSetup 和 SQLDatabaseSetup 程式碼檔，將專案升級至 SQL Server Data Tools 時，會從組建中排除 DatabaseSetup 檔案。 如果從組建排除 DatabaseSetup 檔案，您可以將它移除。  
  
-   轉換之後，以舊版範本建立的現有資料庫單元測試會使用配接器組件中的新型別，以存取新架構。 使用配接器組件，表示升級程序不會修改測試指令碼和程式碼。 如果您將 SQL Server 單元測試加入至專案，新測試會直接參考新架構，而不會透過配接器。 您可以選擇手動更新現有的程式碼使用新架構，以便與新測試保持一致性，但這個動作並非必要。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
