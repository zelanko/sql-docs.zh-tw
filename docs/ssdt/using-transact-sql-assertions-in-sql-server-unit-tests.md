---
title: 在 SQL Server 單元測試中使用 Transact-SQL 判斷提示
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 55d8be9c-9282-47d3-be7f-e2c26f00c95e
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: b8feb69dc25d55b279d65904126afd2733160d6f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243504"
---
# <a name="using-transact-sql-assertions-in-sql-server-unit-tests"></a>在 SQL Server 單元測試中使用 Transact-SQL 判斷提示

在 SQL Server 單元測試中，Transact\-SQL 測試指令碼會執行並傳回結果。 有時候，結果會當做結果集傳回來。 您可以使用測試條件來驗證結果。 例如，您可以使用測試條件來檢查特定結果集傳回的資料列數目或驗證執行特定測試所花費的時間長度。 如需有關測試條件的詳細資訊，請參閱[在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)。  
  
如果不使用測試條件，您也可以使用 Transact\-SQL 判斷提示，亦即 Transact\-SQL 指令碼中的 THROW 或 RAISERROR 陳述式。 在某些情況下，您可能會想要使用 Transact\-SQL 判斷提示而非測試條件。  
  
## <a name="using-transact-sql-assertions"></a>使用 Transact-SQL 判斷提示  
在您決定要使用 Transact\-SQL 判斷提示或測試條件驗證資料之前，應該先考慮下列各點。  
  
-   **效能**： 在伺服器上執行 Transact\-SQL 判斷提示的速度會比先將資料移至用戶端電腦，然後在本機上操作資料要快。  
  
-   **對語言的熟悉程度**： 您可能會根據目前的專業知識而偏好特定語言，因此選擇 Transact\-SQL 判斷提示或 Visual C\# 或 Visual Basic 測試條件。  
  
-   **複雜的驗證**： 在某些情況下，您可以在 Visual C\# 或 Visual Basic 中建置更複雜的測試，並且在用戶端上驗證測試。  
  
-   **簡單**： 使用預先定義的測試條件比在 Transact\-SQL 中撰寫對等的指令碼通常更簡單。  
  
-   **舊版驗證程式庫**： 如果您已經擁有執行驗證的程式碼，就可以將它用於 SQL Server 單元測試，而非使用測試條件。  
  
## <a name="mark-unit-test-methods-with-the-expected-exception"></a>使用預期的例外狀況來標示單元測試方法  
若要標示具有預期例外狀況的 SQL Server 單元測試方法，請加入下列屬性：  
  
```vb  
<ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)> _  
```  
  
```csharp  
[ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)]  
```  
  
其中：  
  
-   *nnnnn* 是預期的訊息編號，例如 14025  
  
-   *x* 是預期的例外狀況嚴重性  
  
-   *y* 是預期的例外狀況狀態  
  
任何未指定的參數都會被忽略。 您可以將這些參數傳遞至資料庫程式碼中的 RAISERROR 陳述式。 如果指定 MatchFirstError = true，此屬性會符合例外狀況中的任何 SqlErrors。 預設行為 (MatchFirstError = true) 是只符合第一個發生的錯誤。  
  
如需如何使用預期的例外狀況和負面的 SQL Server 單元測試的範例，請參閱[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)。  
  
## <a name="the-raiserror-statement"></a>RAISERROR 陳述式  
  
> [!NOTE]  
> 使用 THROW，而不是 RAISERROR。 RAISERROR 現在已被取代。  
  
您可以在 Transact\-SQL 指令碼中使用 RAISERROR 陳述式，藉以直接在伺服器上使用 Transact\-SQL 判斷提示。 其語法如下：  
  
**RAISERROR (@ErrorMessage、@ErrorSeverity、@ErrorState)**  
  
其中：  
  
@ErrorMessage 是任何使用者定義的錯誤訊息。 您可以格式化此訊息字串 (與 printf_s 函式很相似)。  
  
@ErrorSeverity 是使用者定義的嚴重性層級 (範圍從 0 - 18)。  
  
> [!NOTE]  
> 嚴重性層級的 '0' 和 '10' 值不會導致 SQL Server 單元測試失敗。 您可以使用範圍 0 - 18 中的任何其他值來導致測試失敗。  
  
@ErrorState 是 1 - 127 之間的任意整數。 您可以使用此整數來區別在程式碼中不同位置引發之單一錯誤的出現項目。  
  
如需詳細資訊，請參閱 [RAISERROR (Transact-SQL)](https://msdn.microsoft.com/library/ms178592.aspx)。 [如何：撰寫在單一交易範圍內執行的 SQL Server 單元測試](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)主題會提供在 SQL Server 單元測試中使用 RAISERROR 的範例。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[在 SQL Server 單元測試中使用測試條件](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[如何：開啟要編輯的 SQL Server 單元測試](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)  
  
