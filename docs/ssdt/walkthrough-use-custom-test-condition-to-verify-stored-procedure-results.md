---
title: 可驗證預存程序結果的自訂測試條件
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 4c33b494-a85e-4dd2-97b6-c88ee858a99c
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 60160fe3f36d61364b8bf4385fa53b744f9a3475
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286592"
---
# <a name="walkthrough-using-a-custom-test-condition-to-verify-the-results-of-a-stored-procedure"></a>逐步解說：使用自訂測試條件來驗證預存程序的結果

在這個延伸模組功能逐步解說中，您將建立測試條件，並透過建立 SQL Server 單元測試來驗證其功能。 此程序包含建立測試條件的類別庫專案，以及簽署及安裝專案。 如果您已經擁有想要更新的測試條件，請參閱[如何：將 Visual Studio 2010 自訂測試條件從舊版升級至 SQL Server Data Tools](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)。  
  
本逐步解說將說明下列工作：  
  
-   如何建立測試條件。  
  
-   如何使用強式名稱簽署組件。  
  
-   如何將必要參考加入至專案。  
  
-   如何建立測試條件。  
  
-   如何安裝新的測試條件。  
  
-   如何測試新的測試條件。  
  
您必須擁有含最新版 SQL Server Data Tools 的 Visual Studio 2010 或 Visual Studio 2012 才能完成此逐步解說。 如需詳細資訊，請參閱[安裝 SQL Server Data Tools](../ssdt/install-sql-server-data-tools.md)。  
  
## <a name="creating-a-custom-test-condition"></a>建立自訂測試條件  
首先，您將建立類別庫。  
  
1.  在 [檔案]  功能表上，按一下 [新增]  ，然後按一下 [專案]  。  
  
2.  在 [新增專案]  對話方塊中，按一下 [專案類型]  底下的 [Visual C\#]。  
  
3.  在 [範本]  底下，選取 [類別庫]  。  
  
4.  在 [名稱]  文字方塊中，輸入 **ColumnCountCondition** 然後按一下 [確定]  。  
  
接下來，簽署專案。  
  
1.  按一下 [專案]  功能表上的 [ColumnCountCondition 屬性]  。  
  
2.  在 [簽署]  索引標籤上，選取 [簽署組件]  核取方塊。  
  
3.  在 [選擇強式名稱金鑰檔] 方塊中，按一下 [\<新增...>]。  
  
    [建立強式名稱金鑰]  對話方塊隨即出現。  
  
4.  在 [金鑰檔名稱]  方塊中，輸入 **SampleKey**。  
  
5.  輸入並確認密碼，然後按一下 [確定]  。 當您建置方案時，金鑰檔是用來簽署組件。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
7.  在 [建置]  功能表上，按一下 [建置方案]  。  
  
接下來，將必要參考加入至專案。  
  
1.  在 [方案總管]  中，選取 [ColumnCountCondition]  專案。  
  
2.  在 [專案]  功能表上，按一下 [加入參考]  顯示 [加入參考]  對話方塊。  
  
3.  選取 [.NET]  索引標籤。  
  
4.  在 [元件名稱]  欄中，找出並選取 [System.ComponentModel.Composition]  元件。 選取元件之後，按一下 [確定]  。  
  
5.  加入必要的組件參考。 以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]  。 按一下 [瀏覽]  並巡覽至 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 資料夾。 選擇 Microsoft.Data.Tools.Schema.Sql.dll，並按一下 [加入]，然後按一下 [確定]。  
  
6.  按一下 [專案]  功能表上的 [卸載專案]  。  
  
7.  在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [編輯 <project name>.csproj]。  
  
8.  匯入 **Microsoft.CSharp.targets** 之後，新增下列 Import 陳述式：  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. 儲存並關閉檔案。 在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選擇 [重新載入專案]  。  
  
    在 [方案總管] 中專案的 [參考] 節點底下，會顯示必要的參考。  
  
## <a name="creating-the-resultsetcolumncountcondition-class"></a>建立 ResultSetColumnCountCondition 類別  
現在，將 **Class1** 命名為 **ResultSetColumnCountCondition**，並從 [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 來加以衍生。 **ResultSetColumnCountCondition** 類別是簡單的測試條件，可驗證 ResultSet 中所傳回資料行的數目。 您可以使用這個條件，確定預存程序的合約是否正確。  
  
1.  在 [方案總管]  中，以滑鼠右鍵按一下 [Class1.cs]，按一下 [重新命名]  ，然後輸入 **ResultSetColumnCountCondition.cs**。  
  
2.  按一下 [是]  ，確認 Class1 的所有參考都要重新命名。  
  
3.  開啟 [ResultSetColumnCountCondition.cs]  檔案，並將下列 using 陳述式新增至該檔案：  
  
    ```  
    using System;  
    using System.ComponentModel;  
    using System.Data;  
    using System.Data.Common;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
    namespace ColumnCountCondition {  
        public class ResultSetColumnCountCondition  
    ```  
  
4.  從 [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 衍生該類別：  
  
    ```  
    public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
5.  新增 [ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx)。 如需 UnitTesting.Conditions.ExportTestConditionAttribute 的詳細資訊，請參閱[如何：建立 SQL Server 單元測試設計工具的測試條件](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)。  
  
    ```  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
        public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
6.  建立成員變數和建構函式：  
  
    ```  
            private int _resultSet;  
            private int _count;  
            private int _batch;  
  
            public ResultSetColumnCountCondition() {  
                _resultSet = 1;  
                _count = 0;  
                _batch = 1;  
            }  
    ```  
  
7.  覆寫 **Assert** 方法。 該方法包含 **IDbConnection** 的引數 (代表資料庫的連線)，以及 **SqlExecutionResult**。 該方法將 **DataSchemaException** 用於錯誤處理：  
  
    ```  
           //method you need to override  
            //to perform the condition verification  
            public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
            {  
                //call base for parameter validation  
                base.Assert(validationConnection, results);  
  
                //verify batch exists  
                if (results.Length < _batch)  
                    throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
                SqlExecutionResult result = results[_batch - 1];  
  
                //verify resultset exists  
                if (result.DataSet.Tables.Count < ResultSet)  
                    throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
                DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
                //actual condition verification  
                //verify resultset column count matches expected  
                if (table.Columns.Count != Count)  
                    throw new DataException(String.Format(  
                        "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                        ResultSet, table.Columns.Count, Count));  
            }  
  
    Add the following method, which overrides the ToString method:  
    C#  
            //this method is called to provide the string shown in the  
            //test conditions panel grid describing what the condition tests  
            public override string ToString()  
            {  
                return String.Format(  
                    "Condition fails if ResultSet {0} does not contain {1} columns",  
                    ResultSet, Count);  
            }  
    ```  
  
8.  使用 **CategoryAttribute**、**DisplayNameAttribute**和 **DescriptionAttribute** 屬性來新增以下測試條件屬性：  
  
    ```  
            //below are the test condition properties  
            //that are exposed to the user in the property browser  
            #region Properties  
  
            //property specifying the resultset for which  
            //you want to check the column count  
            [Category("Test Condition")]  
            [DisplayName("ResultSet")]  
            [Description("ResultSet Number")]  
            public int ResultSet  
            {  
                get { return _resultSet; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 1)  
                        throw new ArgumentException("ResultSet cannot be less than 1");  
  
                    _resultSet = value;  
                }  
            }  
  
            //property specifying  
            //expected column count  
            [Category("Test Condition")]  
            [DisplayName("Count")]  
            [Description("Column Count")]  
            public int Count  
            {  
                get { return _count; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 0)  
                        throw new ArgumentException("Count cannot be less than 0");  
  
                    _count = value;  
                }  
            }  
             #endregion  
    ```  
  
最後的程式碼如下所列：  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace ColumnCountCondition  
{  
  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
    public class ResultSetColumnCountCondition : TestCondition  
    {  
        private int _resultSet;  
        private int _count;  
        private int _batch;  
  
        public ResultSetColumnCountCondition()  
        {  
            _resultSet = 1;  
            _count = 0;  
            _batch = 1;  
        }  
  
        //method you need to override  
        //to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            //call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            //verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            //verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            //actual condition verification  
            //verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        //this method is called to provide the string shown in the  
        //test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        //below are the test condition properties  
        //that are exposed to the user in the property browser  
        #region Properties  
  
        //property specifying the resultset for which  
        //you want to check the column count  
        [Category("Test Condition")]  
        [DisplayName("ResultSet")]  
        [Description("ResultSet Number")]  
        public int ResultSet  
        {  
            get { return _resultSet; }  
  
            set  
            {  
                //basic validation  
                if (value < 1)  
                    throw new ArgumentException("ResultSet cannot be less than 1");  
  
                _resultSet = value;  
            }  
        }  
  
        //property specifying  
        //expected column count  
        [Category("Test Condition")]  
        [DisplayName("Count")]  
        [Description("Column Count")]  
        public int Count  
        {  
            get { return _count; }  
  
            set  
            {  
                //basic validation  
                if (value < 0)  
                    throw new ArgumentException("Count cannot be less than 0");  
  
                _count = value;  
            }  
        }  
  
        #endregion  
    }  
}  
  
```  
  
接下來，建置專案。  
  
## <a name="compiling-the-project-and-installing-your-test-condition"></a><a name="xxx"></a>編譯專案及安裝測試條件  
在 [建置]  功能表上，按一下 [建置方案]  。  
  
接下來，將組件資訊複製到 Extensions 目錄。 當 Visual Studio 啟動時，會識別 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 目錄和子目錄中的任何延伸模組，並讓這些延伸模組可供使用：  
  
從輸出目錄中，將 **ColumnCountCondition.dll** 組件檔複製到 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 目錄。  
  
根據預設，編譯過的 .dll 檔案的路徑是 *YourSolutionPath*\\*YourProjectPath*\bin\Debug 或 *YourSolutionPath*\\*YourProjectPath*\bin\Release。  
  
接下來，啟動新的 Visual Studio 工作階段並建立資料庫專案。 開始新的 Visual Studio 工作階段並建立資料庫專案：  
  
1.  啟動第二個 Visual Studio 工作階段。  
  
2.  在 [檔案]  功能表上，按一下 [新增]  ，然後按一下 [專案]  。  
  
3.  在 [新增專案]  對話方塊中，於已安裝的範本清單中選取 [SQL Server]  節點。  
  
4.  在 [詳細資料] 窗格中，按一下 [SQL Server 資料庫專案]  。  
  
5.  在 [名稱]  文字方塊中，輸入 **SampleConditionDB**，然後按一下 [確定]  。  
  
接下來必須建立單元測試。 在新的測試類別內建立 SQL Server 單元測試：  
  
1.  在 [測試]  功能表上，按一下 [新增測試]  以顯示 [加入新測試]  對話方塊。  
  
    您也可以開啟 [方案總管]  ，以滑鼠右鍵按一下測試專案，指向 [加入]  ，然後按一下 [新增測試]  。  
  
2.  在範本清單中，按一下 [SQL Server 單元測試]  。  
  
3.  在 [測試名稱]  中，輸入 **SampleUnitTest**。  
  
4.  在 [加入至測試專案]，按一下 [建立新的 Visual C\# 測試專案]。 然後按一下 [確定]  以顯示 [新增測試專案]  對話方塊。  
  
5.  輸入 **SampleUnitTest** 作為專案名稱。  
  
6.  按一下 [取消]  即可建立單元測試，而不設定測試專案使用資料庫連線。 您的空白測試會出現在「SQL Server 單元測試設計工具」中。 Visual C\# 原始程式碼檔會加入至測試專案。  
  
    如需建立和設定資料庫單元測試與資料庫連線的詳細資訊，請參閱[如何：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)。  
  
7.  按一下 [按一下此處以建立]  以完成建立單元測試。 您會看到新的測試條件顯示在 SQL Server 專案中。  
  
> [!NOTE]  
> 若要將自訂測試條件用於現有的單元測試專案，必須建立至少一個新的 SQL Server 單元測試類別。 建立測試類別期間，測試條件組件的必要參考就會加入至測試專案。  
  
若要檢視新的測試條件：  
  
1.  在 [SQL Server 單元測試設計工具]  的 [測試條件]  底下，按一下 [名稱]  欄底下的 [inconclusiveCondition1] 測試。  
  
2.  按一下 [刪除測試條件]  工具列按鈕，以移除 inconclusiveCondition1 測試。  
  
3.  按一下 [測試條件]  下拉式清單，並選取 [ResultSet 資料行計數]  。  
  
4.  按一下 [加入測試條件]  工具列按鈕，以加入自訂測試條件。  
  
5.  在 [屬性]  視窗中，設定 Count、Enabled 和 ResultSet 屬性。  
  
    如需詳細資訊，請參閱[如何：將測試條件加入至 SQL Server 單元測試](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
