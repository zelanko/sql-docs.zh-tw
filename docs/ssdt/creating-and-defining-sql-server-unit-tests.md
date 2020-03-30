---
title: 建立和定義 SQL Server 單元測試
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 3c082177-a2b1-4fde-8833-b49b2a351815
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 096fc7128d5c6d62dad0957445380ac8860645a6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245536"
---
# <a name="creating-and-defining-sql-server-unit-tests"></a>建立和定義 SQL Server 單元測試

您可以執行 SQL Server 單元測試，來驗證結構描述中一個或多個資料庫物件的變更是否中斷了資料庫應用程式中的現有功能。 這些測試會補充軟體開發人員所建立的單元測試。 您必須執行這兩種測試以驗證應用程式的行為。  
  
您可以加入 SQL Server 單元測試並且加入 Transact\-SQL 指令碼以測試任何物件，藉以驗證該物件在結構描述中的行為。 或者，如果您想要驗證特定函式、觸發程序或預存程序的行為，也可以自動產生 Transact\-SQL 指令碼的 Stub。 產生 Stub 之後，您必須進行自訂，才能取得有意義的結果。  
  
> [!NOTE]  
> 您可以在不開啟 SQL Server 資料庫專案的情況下，建立空白測試、加入程式碼並且執行測試。 但是，如果您沒有開啟包含想要測試之物件的專案，就無法自動產生測試函式、觸發程序或預存程序的 Transact\-SQL Stub。  
  
## <a name="common-tasks"></a>一般工作  
下表列出支援此案例之一般工作的說明，以及詳細資訊的連結，這些資訊可幫助您成功完成這些工作。  
  
|一般工作|支援內容|  
|----------------|----------------------|  
|**進行實際操作練習**：您可以依照入門逐步解說來熟悉如何建立並執行簡單的 SQL Server 單元測試。|-   [逐步解說：建立並執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**深入了解 SQL Server 單元測試**：您可以深入了解組成 SQL Server 單元測試的檔案和指令碼。 您也可以了解如何在單元測試中使用測試條件和 Transact\-SQL 判斷提示。|-   [SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)<br />-   [SQL Server 單元測試檔案](../ssdt/sql-server-unit-test-files.md)<br />-   [在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)<br />-   [在 SQL Server 單元測試中使用 Transact-SQL 判斷提示](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)|  
|**建立一個或多個測試專案**：您必須在測試專案中建立 SQL Server 單元測試。 如果您在建立測試專案之前使用 SQL Server [物件總管] 建立 SQL Server 單元測試，系統就會為您建立測試專案。 例如，如果您想要在不同的測試集中使用不同的資料產生計劃或不同的部署組態，就可以先建立多個測試專案。 建立測試專案時，您可以設定要用於該專案的測試設定 (例如連接字串)、部署設定和資料產生計劃。|-   [如何：建立 SQL Server 資料庫單元測試的測試專案](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)<br />-|  
|**設定單元測試的執行方式**：您可以針對執行測試、資料產生計劃和部署設定的目標資料庫指定連接字串。 您可以在第一次將 SQL Server 單元測試加入至專案時進行這些設定，但是之後也可以進行修改。|-   [如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)<br />-   [連接字串和權限概觀](../ssdt/overview-of-connection-strings-and-permissions.md)|  
|**建立 SQL Server 單元測試**：您可以自動建立 SQL Server 單元測試的 Transact\-SQL 程式碼 Stub，以便驗證函式、觸發程序或預存程序的行為。 您也可以建立空白的 SQL Server 單元測試，然後再加入 Transact\-SQL 程式碼以測試其他類型的資料庫物件。|-   [如何：建立函式、觸發程序和預存程序的 SQL Server 單元測試](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)<br />-   [如何：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)|  
|**撰寫 SQL Server 單元測試的程式碼**：建立單元測試之後，您必須修改或撰寫 Transact\-SQL 程式碼以測試資料庫物件。 您可以針對每個測試定義一個或多個測試條件，以便判斷測試成功或失敗。 如果是更複雜的測試，您可以修改資料庫專案中的 Visual Basic 或 Visual C\# 程式碼。 例如，您可以撰寫在單一交易範圍內執行的單元測試。|-   [如何：開啟要編輯的 SQL Server 單元測試](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)<br />-   [如何：將測試條件加入至 SQL Server 單元測試](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)<br />-   [如何：撰寫在單一交易範圍內執行的 SQL Server 單元測試](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)<br />-   [SQL Server 單元測試設計工具的鍵盤快速鍵](../ssdt/keyboard-shortcuts-for-sql-server-unit-test-designer.md)|  
|**疑難排解問題**：您可以深入了解如何疑難排解 SQL Server 的常見問題。|-   [疑難排解 SQL Server 資料庫單元測試的問題](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>相關案例  
[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)  
建立 SQL Server 單元測試之後，您可以從 [測試檢視] 視窗、SQL Server 單元測試設計工具或使用 Team Foundation Build 來執行測試。  
  
[案例：定義資料庫單元測試的自訂測試條件](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)  
您可以建立自訂測試條件來測試預設測試條件無法驗證的行為。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
