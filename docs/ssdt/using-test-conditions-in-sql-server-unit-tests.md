---
title: 在 SQL Server 單元測試中使用測試條件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconditions
ms.assetid: e3d1c86c-1e58-4d2c-b625-d1b591b221aa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fa2bce398b6ac03422044c9ffad23f91ab81818c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140968"
---
# <a name="using-test-conditions-in-sql-server-unit-tests"></a>在 SQL Server 單元測試中使用測試條件
在 SQL Server 單元測試中，系統會執行一或多個 Transact\-SQL 測試指令碼。 您可以在 Transact\-SQL 指令碼內評估結果，也可以在測試中定義用來傳回錯誤及使測試失敗的 THROW 或 RAISERROR 或測試條件來評估結果。 測試會傳回 [SqlExecutionResult](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.sqlexecutionresult.aspx) 類別的執行個體。 這個類別的執行個體會包含一個或多個資料集、執行時間以及受指令碼影響的資料列。 所有這些資訊都會在執行指令碼期間收集。 可以使用測試條件來評估這些結果。 SQL Server Data Tools 會提供一組預先定義的測試條件。 您也可以建立及使用自訂條件；請參閱 [SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)。  
  
## <a name="predefined-test-conditions"></a>預先定義的測試條件  
下表列出預先定義的測試條件，您可以使用 SQL Server 單元測試設計工具中的 [測試條件] 窗格加入這些測試條件。  
  
|**測試條件**|**測試條件描述**|  
|----------------------|----------------------------------|  
|資料總和檢查碼|如果從 Transact\-SQL 指令碼所傳回結果集的總和檢查碼與預期的總和檢查碼不符，則失敗。 如需詳細資訊，請參閱 [指定資料總和檢查碼](#SpecifyDataChecksum)。<br /><br />**注意：** 如果傳回的資料會在測試回合之間變更，則不建議使用此測試條件。 例如，如果結果集包含產生的日期或時間，或包含識別資料行，則測試會因為每個回合的總和檢查碼不同而失敗。|  
|空白 ResultSet|如果從 Transact\-SQL 指令碼傳回的結果集不是空白，則失敗。|  
|執行時間|如果 Transact\-SQL 測試指令碼執行時間超出預期，則失敗。 預設執行時間是 30 秒。<br /><br />執行時間只適用於測試指令碼，不適用於測試前指令碼或測試後指令碼。|  
|預期的結構描述|如果結果集的資料行和資料型別不符合為測試條件指定的資料行和資料型別，則失敗。 您必須透過測試條件的屬性來指定結構描述。 如需詳細資訊，請參閱 [指定預期的結構描述](#SpecifyExpectedSchema)。|  
|結果不明|永遠會產生結果不明的測試。 這是加入到每一個測試中的預設條件。 包含這個測試條件的目的為要指出尚未實作測試驗證。 當您已經加入其他測試條件之後，請從測試中刪除這個測試條件。|  
|非空白 ResultSet|如果結果集是空的，則失敗。 您可以在測試指令碼中使用這個測試條件，或使用 EmptyResultSet 搭配 Transact\-SQL @@RAISERROR 函式，測試更新是否正常運作。 例如，您可以儲存更新前的值、執行更新、比較更新後的值，然後如果沒有取得預期的結果，則引發錯誤。|  
|資料列計數|如果結果集沒有包含預期的資料列數，則失敗。|  
|純量值|如果結果集中的特定值不等於指定值，則失敗。 預設 [ **需要的值** ] 為 null。|  
  
> [!NOTE]  
> [執行時間] 測試條件會指定 Transact\-SQL 測試指令碼必須執行的時間限制。 如果超過此時間限制，測試就會失敗。 測試結果也會包含 [持續期間] 統計資料，這與 [執行時間] 測試條件不同。 [持續期間] 統計資料不只包含執行時間，也包含兩次連接資料庫的時間、執行任何其他測試指令碼的時間 (例如測試前指令碼和測試後指令碼)，以及執行測試條件的時間。 因此，即使持續期間超過執行時間，測試也會成功。  
>   
> 報告的 [持續期間] 不包括產生資料和部署結構描述所用的時間，因為這些動作是在測試執行之前發生。 若要檢視測試持續期間，請在 [測試結果]  視窗中選取測試回合，按一下滑鼠右鍵，然後選擇 [檢視測試結果詳細資料]  。  
  
您可以使用 SQL Server 單元測試設計工具的 [測試條件] 窗格，將測試條件加入至 SQL Server 單元測試。 如需詳細資訊，請參閱[如何：將測試條件新增至 SQL Server 單元測試](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)。  
  
您也可以直接編輯測試方法程式碼，加入更多的功能。 如需詳細資訊，請參閱[如何：開啟要編輯的 SQL Server 單元測試](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)及[如何：撰寫在單一交易範圍內執行的 SQL Server 單元測試](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)。 例如，您可以加入 Assert 陳述式，將功能加入至測試方法。 如需詳細資訊，請參閱[在 SQL Server 單元測試中使用 Transact-SQL 判斷提示](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)。  
  
## <a name="expected-failures"></a>預期的失敗  
您可以建立 SQL Server 單元測試，測試不應成功的行為。 這些預期的失敗有時稱為負面測試。 一些例子如下：  
  
-   確認刪除客戶資料的預存程序會在指定的客戶 ID 無效時失敗。  
  
-   確認要完成訂單的預存程序會在訂單從未開出或已經完成時失敗。  
  
-   確認取消訂單的預存程序無法取消已完成的訂單或已取消的訂單。  
  
您可以為擲回預期例外狀況的預存程序，定義 SQL Server 單元測試。 您可以在單元測試方法中加入屬性，指出有哪個或哪些預期的例外狀況。 如此即可防止測試在發生例外狀況時失敗。  
  
若要標示具有預期例外狀況的 SQL Server 單元測試方法，請加入下列屬性：  
  
```  
[ExpectedSqlException(MessageNumber = nnnnn, Severity = x, MatchFirstError = false, State = y)]  
```  
  
其中：  
  
-   *nnnnn* 是預期的訊息編號，例如 14025  
  
-   *x* 是預期的例外狀況嚴重性  
  
-   *y* 是預期的例外狀況狀態  
  
任何未指定的參數都會被忽略。 可以將這些參數傳遞至資料庫程式碼中的 **THROW** 陳述式。 如果指定 MatchFirstError = false，此屬性會符合例外狀況中的任何 SqlErrors。 預設行為 (MatchFirstError = true) 是只符合第一個發生的錯誤。  
  
如需如何使用預期例外狀況以及負面 SQL Server 單元測試的範例，請參閱[逐步解說：建立及執行 SQL Server 單元測試](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)。  
  
## <a name="SpecifyDataChecksum"></a>指定資料總和檢查碼  
若要顯示 SQL Server 單元測試設計工具，請在 [方案總管]  中按兩下單元測試原始程式碼檔。  
  
在資料庫單元測試中加入 [資料總和檢查碼] 測試條件之後，必須使用下列程序來設定預期的總和檢查碼：  
  
#### <a name="to-specify-an-expected-checksum"></a>若要指定預期的總和檢查碼  
  
1.  在測試條件清單中，按一下要指定總和檢查碼的 [資料總和檢查碼] 測試條件。  
  
2.  按 F4 開啟 [ **屬性** ] 視窗。 您也可以開啟 [ **檢視** ] 功能表，然後按一下 [ **屬性** ] 視窗。  
  
3.  (選擇性) 您可以將測試條件的 [(名稱)]  屬性變更為更有描述性的文字。  
  
4.  在 [組態]  屬性中，按一下瀏覽 ([...]  ) 按鈕。  
  
    [ **TestConditionName 的組態** ] 對話方塊隨即出現。  
  
5.  指定要測試的資料庫連接。 如需詳細資訊，請參閱[如何：建立資料庫連線](https://msdn.microsoft.com/library/aa833420(VS.100).aspx)。  
  
6.  根據預設，測試的 Transact\-SQL 主體會出現在 [編輯] 窗格中。 您可以視需要修改程式碼以產生預期的結果。 例如，如果您的測試有測試前程式碼，可能必須加入該程式碼。  
  
    > [!IMPORTANT]  
    > 如果針對先前已指定總和檢查碼的總和檢查碼條件進行修改，在編輯窗格中所做的任何變更都不會儲存。 您必須重新進行變更，然後按一下 [ **擷取**]。  
  
7.  按一下 [ **擷取**]。  
  
    如此隨即針對指定的資料庫連接執行 Transact\-SQL ，而且結果會出現在對話方塊中。  
  
8.  如果結果符合預期的測試結果，請按一下 [ **確定**]。 否則請修改 Transact\-SQL 主體並重複步驟 6、7 和 8，直到結果符合預期為止。  
  
    測試條件的 [ **值** ] 資料行會顯示預期的總和檢查碼值。  
  
## <a name="SpecifyExpectedSchema"></a>指定預期的結構描述  
在您於 SQL Server 單元測試中加入 [預期的結構描述] 測試條件之後，必須使用下列程序來設定預期的結構描述：  
  
#### <a name="to-specify-an-expected-schema"></a>若要指定預期的結構描述  
  
1.  在測試條件清單中，按一下要指定結構描述的 [預期的結構描述] 測試條件。  
  
2.  按 F4 開啟 [ **屬性** ] 視窗。 您也可以開啟 [ **檢視** ] 功能表，然後按一下 [ **屬性** ] 視窗。  
  
3.  (選擇性) 您可以將測試條件的 [(名稱)]  屬性變更為更有描述性的文字。  
  
4.  在 [組態]  屬性中，按一下瀏覽 ([...]  ) 按鈕。  
  
    [ **TestConditionName 的組態** ] 對話方塊隨即出現。  
  
5.  指定要測試的資料庫連接。 如需詳細資訊，請參閱[如何：建立資料庫連線](https://msdn.microsoft.com/library/aa833420(VS.100).aspx)。  
  
6.  根據預設，測試的 Transact\-SQL 主體會出現在 [編輯] 窗格中。 您可以視需要修改程式碼以產生預期的結果。 例如，如果您的測試有測試前程式碼，可能必須加入該程式碼。  
  
    > [!IMPORTANT]  
    > 如果針對先前已指定結構描述之預期的結構描述條件進行修改，在編輯窗格中所做的任何變更都不會儲存。 您必須重新進行變更，然後按一下 [ **擷取**]。  
  
7.  按一下 [ **擷取**]。  
  
    如此隨即針對指定的資料庫連接執行 Transact\-SQL ，而且結果會出現在對話方塊中。 因為您要確認結果集的結構描述 (或型態) 而不是結果值，所以只要資料行如預期顯示，就不需檢視傳回的任何結果資料。  
  
8.  如果結果符合預期的測試結果，請按一下 [ **確定**]。 否則請修改 Transact\-SQL 主體並重複步驟 6、7 和 8，直到結果符合預期為止。  
  
    測試條件的 [ **值** ] 資料行會顯示預期的結構描述資訊。 例如，它可能會是「必須是：2 個資料表」。  
  
## <a name="extensible-test-conditions"></a>可延伸測試條件  
除了六個預先定義的測試條件，您也可以自行撰寫新的測試條件。 這些測試條件會顯示在 SQL Server 單元測試設計工具的 [測試條件] 窗格中。 如需詳細資訊，請參閱 [SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[在 SQL Server 單元測試中使用 Transact-SQL 判斷提示](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)  
[SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
