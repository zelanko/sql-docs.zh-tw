---
title: 撰寫在單一交易範圍內執行的 SQL Server 單元測試
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: cb241e94-d81c-40e9-a7ae-127762a6b855
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 36bc1ac2a4a20dd0d05d90b8d12ff63b0a7a6b3e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246492"
---
# <a name="how-to-write-a-sql-server-unit-test-that-runs-within-the-scope-of-a-single-transaction"></a>HOW TO：撰寫在單一交易範圍內執行的 SQL Server 單元測試

您可以修改單元測試，使其在單一交易範圍中執行。 如果採用這種方法，在測試結束之後，可以復原此測試所進行的任何變更。 下列程序說明其做法：  
  
-   在 Transact\-SQL 測試指令碼中，建立使用 **BEGIN TRANSACTION** 和 **ROLLBACK TRANSACTION** 的交易。  
  
-   在測試類別中建立單一測試方法的交易。  
  
-   在指定的測試類別中建立所有測試方法的交易。  
  
**必要條件**  
  
對於本主題中的部分程序而言，必須在執行單元測試的電腦上執行分散式交易協調器服務。 如需詳細資訊，請參閱本主題結尾的程序。  
  
## <a name="to-create-a-transaction-using-transact-sql"></a>若要使用 Transact\-SQL 建立交易  
  
#### <a name="to-create-a-transaction-using-transact-sql"></a>若要使用 Transact\-SQL 建立交易  
  
1.  在 SQL Server 單元測試設計工具中，開啟單元測試。 (按兩下單元測試的原始程式碼檔，即可顯示設計工具)。  
  
2.  指定您要建立交易的指令碼類型。 例如，您可以指定測試前、測試或測試後。  
  
3.  在 Transact\-SQL 編輯器中輸入測試指令碼。  
  
4.  插入 `BEGIN TRANSACTION` 和 `ROLLBACK TRANSACTION` 陳述式，如以下的簡單範例所示。 這個範例使用名稱為 OrderDetails 的資料庫資料表，其中包含 50 個資料列：  
  
    ```  
    BEGIN TRANSACTION TestTransaction  
    UPDATE "OrderDetails" set Quantity = Quantity + 10  
    IF @@ROWCOUNT!=50  
    RAISERROR('Row count does not equal 50',16,1)  
    ROLLBACK TRANSACTION TestTransaction  
    ```  
  
    > [!NOTE]  
    > 在執行 COMMIT TRANSACTION 陳述式之後，無法復原交易。  
  
    如需如何搭配預存程序和觸發程序使用 ROLLBACK TRANSACTION 的詳細資訊，請參閱 Microsoft 網站上的這個網頁：[ROLLBACK TRANSACTION (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkID=115927)。  
  
## <a name="to-create-a-transaction-for-a-single-test-method"></a>若要建立單一測試方法的交易  
在此範例中，您是在使用 [System.Transactions.TransactionScope](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope) 類型時使用環境交易。 根據預設，執行連接和授權連接不會使用環境交易，因為這些連接是在執行方法前即已建立。 SqlConnection 擁有的 [System.Data.SqlClient.SqlConnection.EnlistTransaction](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlconnection.enlisttransaction) 方法會將作用中的連接與交易產生關聯。 建立環境交易時，會將自己註冊為目前的交易，而您可以透過 [System.Transactions.Transaction.Current](https://docs.microsoft.com/dotnet/api/system.transactions.transaction.current) 屬性存取此交易。 在此範例中，在處置環境交易時就會復原交易。 如果想要認可在執行單元測試時進行的任何變更，您必須呼叫 [System.Transactions.TransactionScope.Complete](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope.complete) 方法。  
  
#### <a name="to-create-a-transaction-for-a-single-test-method"></a>若要建立單一測試方法的交易  
  
1.  在 [方案總管]  中，以滑鼠右鍵按一下測試專案中的 [參考]  節點，然後按一下 [加入參考]  。  
  
    [新增參考]  對話方塊隨即出現。  
  
2.  按一下 [.NET]  索引標籤。  
  
3.  在組件清單中，按一下 **System.Transactions**，然後按一下 [確定]  。  
  
4.  開啟單元測試的 Visual Basic 或 C# 檔案。  
  
5.  包裝測試前、測試和測試後動作，如下列 Visual Basic 程式碼範例所示：  
  
    ```  
    <TestMethod()> _  
    Public Sub dbo_InsertTable1Test()  
  
        Using ts as New System.Transactions.TransactionScope( System.Transactions.TransactionScopeOption.Required)  
            ExecutionContext.Connection.EnlistTransaction(Transaction.Current)  
            PrivilegedContext.Connection.EnlistTransaction(Transaction.Current)  
  
            Dim testActions As DatabaseTestActions = Me.dbo_InsertTable1TestData  
            'Execute the pre-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PretestAction) Is Nothing), "Executing pre-test script...")  
            Dim pretestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PretestAction)  
            'Execute the test script  
  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.TestAction) Is Nothing), "Executing test script...")  
            Dim testResults() As ExecutionResult = TestService.Execute(ExecutionContext, Me.PrivilegedContext, testActions.TestAction)  
  
            'Execute the post-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PosttestAction) Is Nothing), "Executing post-test script...")  
            Dim posttestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PosttestAction)  
  
            'Because the transaction is not explicitly committed, it  
            'is rolled back when the ambient transaction is   
            'disposed.  
            'To commit the transaction, remove the comment delimiter  
            'from the following statement:  
            'ts.Complete()  
  
    End Sub  
    Private dbo_InsertTable1TestData As DatabaseTestActions  
    ```  
  
    > [!NOTE]  
    > 如果您是使用 Visual Basic，則必須新增 `Imports System.Transactions` (除了 `Imports Microsoft.VisualStudio.TestTools.UnitTesting`、`Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTesting` 和 `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTest.Conditions` 之外)。如果您是使用 Visual C#，則必須新增 `using System.Transactions` (除了 Microsoft.VisualStudio.TestTools、Microsoft.VisualStudio.TeamSystem.Data.UnitTesting 和 Microsoft.VisualStudio.TeamSystem.Data.UnitTesting.Conditions 的 `using` 陳述式之外)。 您也必須將專案的參考加入到這些組件。  
  
## <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>若要在測試類別中建立所有測試方法的交易  
  
#### <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>若要在測試類別中建立所有測試方法的交易  
  
1.  開啟單元測試的 Visual Basic 或 C# 檔案。  
  
2.  在 TestInitialize 中建立交易，並在 TestCleanup 中加以處置，如下列 Visual C# 程式碼範例所示：  
  
    ```  
    TransactionScope _trans;  
  
            [TestInitialize()]  
            public void Init()  
            {  
                _trans = new TransactionScope();  
                base.InitializeTest();  
            }  
  
            [TestCleanup()]  
            public void Cleanup()  
            {  
                base.CleanupTest();  
                _trans.Dispose();  
            }  
  
            [TestMethod()]  
            public void TransactedTest()  
            {  
                DatabaseTestActions testActions = this.DatabaseTestMethod1Data;  
                // Execute the pre-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PretestAction != null), "Executing pre-test script...");  
                ExecutionResult[] pretestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PretestAction);  
                // Execute the test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.TestAction != null), "Executing test script...");  
                ExecutionResult[] testResults = TestService.Execute(this.ExecutionContext, this.PrivilegedContext, testActions.TestAction);  
                // Execute the post-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PosttestAction != null), "Executing post-test script...");  
                ExecutionResult[] posttestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PosttestAction);  
  
            }  
    ```  
  
## <a name="to-start-the-distributed-transaction-coordinator-service"></a>若要啟動分散式交易協調器服務  
本主題中的部分程序使用 System.Transactions 組件中的型別。 在進行這些程序之前，您必須確定在執行單元測試的電腦上有執行分散式交易協調器服務。 否則測試就會失敗，並出現下列錯誤訊息：「測試方法 *ProjectName*.*TestName*.*MethodName* 擲回例外狀況: System.Data.SqlClient.SqlException: 伺服器 '*ComputerName*' 上的 MSDTC 無法使用」。  
  
#### <a name="to-start-the-distributed-transaction-coordinator-service"></a>若要啟動分散式交易協調器服務  
  
1.  開啟 [ **控制台**]。  
  
2.  在 [控制台]  中，開啟 [系統管理工具]  。  
  
3.  在 [系統管理工具]  中，開啟 [服務]  。  
  
4.  在 [服務]  窗格中，以滑鼠右鍵按一下 [分散式交易控制器]  服務，然後按一下 [啟動]  。  
  
    服務的狀態應該會更新為 [已啟動]  。 現在應該就能夠執行使用 System.Transactions 的單元測試。  
  
> [!IMPORTANT]  
> 即使您已啟動分散式交易控制器服務，仍有可能發生下列錯誤：`System.Transactions.TransactionManagerCommunicationException: Network access for Distributed Transaction Manager (MSDTC) has been disabled. Please enable DTC for network access in the security configuration for MSDTC using the Component Services Administrative tool. ---> System.Runtime.InteropServices.COMException: The transaction manager has disabled its support for remote/network transactions. (Exception from HRESULT: 0x8004D024)`。 如果發生這個錯誤，您必須針對網路存取設定分散式交易控制器。 如需詳細資訊，請參閱[啟用網路 DTC 存取](https://go.microsoft.com/fwlink/?LinkId=193916)。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
