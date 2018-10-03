---
title: 如何：開啟要編輯的 SQL Server 單元測試 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c6af1b12-54cd-42f9-b2ef-7164f8078323
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 480f5c487c5fb8f9db9f1db61dd7b4126b6c8bb4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787426"
---
# <a name="how-to-open-a-sql-server-unit-test-to-edit"></a>HOW TO：開啟要編輯的 SQL Server 單元測試
在建立 SQL Server 單元測試之後，您可以使用 [SQL Server 單元測試設計工具] 加入 Transact\-SQL 陳述式和測試條件。 使用設計工具所建立的測試會產生 Visual C# 或 Visual Basic 程式碼。 此程式碼是測試執行時所執行的程式碼。  
  
如果您對測試感到滿意，可以直接執行測試。 如果要在此單元測試中加入更多功能，可以編輯其程式碼。 此程式碼位於測試專案中的 .cs 或 .vb 檔案。 如需詳細資訊，請參閱 [SQL Server 單元測試檔案](../ssdt/sql-server-unit-test-files.md)。 您也可以建立新的測試條件來自訂測試。 如需詳細資訊，請參閱[如何：建立資料庫單元測試設計工具的測試條件 (Visual Studio 2010)](http://msdn.microsoft.com/library/aa833409(VS.100).aspx)。  
  
> [!NOTE]  
> 如果以編輯 .cs 或 .vb 檔案的方式刪除測試方法，該測試方法仍會出現在 [SQL Server 單元測試設計工具] 中。 這是因為測試類別的 InitializeComponent 方法仍會包含該測試的成員變數。 雖然測試會出現在設計工具中，但您無法執行測試，因為其程式碼已不存在。 若要重新產生這個測試的測試方法，請在編輯器中編輯 Transact\-SQL，然後儲存 .cs 或 .vb 測試檔案，或重建測試專案。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-solution-explorer"></a>若要從 [方案總管] 開啟 SQL Server 單元測試的原始程式碼檔  
  
-   在 [方案總管] 中，以滑鼠右鍵按一下包含 SQL Server 單元測試的原始程式碼檔，然後按一下 [檢視程式碼]。  
  
    在檔案開啟時，單元測試的測試方法會出現在 Visual Studio 的主要編輯視窗中。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2010"></a>若要從 [測試檢視] 視窗開啟 SQL Server 單元測試的原始程式碼檔 (Visual Studio 2010)  
  
1.  執行單元測試。 如需詳細資訊，請參閱[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)中的＜執行 SQL Server 單元測試＞一節。  
  
2.  在 [測試檢視] 視窗中，以滑鼠右鍵按一下測試，然後按一下 [開啟測試]。  
  
    在檔案開啟時，單元測試的測試方法會出現在 Visual Studio 的主要編輯視窗中。  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2012"></a>若要從 [測試檢視] 視窗開啟 SQL Server 單元測試的原始程式碼檔 (Visual Studio 2012)  
  
1.  執行單元測試。 如需詳細資訊，請參閱[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)中的＜執行 SQL Server 單元測試＞一節。  
  
2.  在 [測試總管] 視窗中，按一下單元測試原始程式碼檔的名稱。  
  
    在檔案開啟時，單元測試的測試方法會出現在 Visual Studio 的主要編輯視窗中。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
