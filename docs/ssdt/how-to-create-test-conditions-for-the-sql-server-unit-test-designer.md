---
title: 建立 SQL Server 單元測試設計工具的測試條件
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 48076062-1ef5-419a-8a55-3c7b4234cc35
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 75d65bb7b30a8a48a35ada0c929ddf4698ad8408
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241484"
---
# <a name="how-to-create-test-conditions-for-the-sql-server-unit-test-designer"></a>HOW TO：建立 SQL Server 單元測試設計工具的測試條件

您可以使用可延伸的 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 類別，建立新的測試條件。 例如，您可以建立新的測試條件，驗證結果集中的資料行數目或值。  
  
## <a name="to-create-a-test-condition"></a>若要建立測試條件  
這個程序說明如何建立測試條件，讓它出現在 SQL Server 單元測試設計工具中。  
  
1.  在 Visual Studio 中，建立類別庫專案。  
  
2.  在 [專案]  功能表上，按一下 [加入參考]  。  
  
3.  按一下 [.NET]  索引標籤。  
  
4.  在 [元件名稱]  清單中，選取 [System.ComponentModel.Composition]  ，然後按一下 [確定]  。  
  
5.  加入必要的組件參考。 以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]  。 按一下 [瀏覽]  並巡覽至 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 資料夾。 選擇 Microsoft.Data.Tools.Schema.Sql.dll，並按一下 [加入]，然後按一下 [確定]。  
  
6.  按一下 [專案]  功能表上的 [卸載專案]  。  
  
7.  在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [編輯 <project name>.csproj]。  
  
8.  匯入 Microsoft.CSharp.targets 之後，加入下列 Import 陳述式：  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. 儲存並關閉檔案。 在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選擇 [重新載入專案]  。  
  
10. 從 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 類別衍生您的類別。  
  
11. 使用強式名稱簽署組件。 如需詳細資訊，請參閱[如何：使用強式名稱簽章組件](https://msdn.microsoft.com/library/xc31ft41.aspx)。  
  
12. 建置類別庫。  
  
13. 使用新的測試條件之前，必須先將已簽署的組件複製到 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 資料夾。 如果這個資料夾不存在，則予以建立。 您需要電腦的系統管理權限，才能複製到這個目錄。  
  
14. 安裝測試條件。 如需詳細資訊，請參閱 [SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)。  
  
15. 將新的 SQL Server 單元測試加入至專案，建立測試條件的參考，以加入至專案。 您可以在專案中手動加入測試條件組件的參考。 在此步驟後重新載入設計工具。  
  
    > [!NOTE]  
    > 也必須加入測試類別，以建立參考。 加入參考之後，可以刪除測試類別。  
  
在下列範例中，您建立簡單的測試條件來驗證結果集中傳回的資料行數目。 您可以使用這個簡單測試條件，確定預存程序的合約是否正確。  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace Ssdt.Samples.SqlUnitTesting  
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
  
        // method you need to override  
        // to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            // call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            // verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            // verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            // actual condition verification  
            // verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        // this method is called to provide the string shown in the  
        // test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        // below are the test condition properties  
        // that are exposed to the user in the property browser  
        #region Properties  
  
        // property specifying the resultset for which  
        // you want to check the column count  
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
  
        // property specifying  
        // expected column count  
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
  
自訂測試條件的類別繼承自基底 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 類別。 由於自訂測試條件的額外屬性，在安裝條件之後，使用者可在 [屬性] 視窗中設定條件。  
  
[ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx) 必須加入至擴充 [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 的類別。 此屬性可讓 SQL Server Data Tools 發現類別，並在單元測試設計和執行期間使用。 這個屬性接受兩個參數：  
  
|屬性參數|位置|描述|  
|-----------------------|------------|---------------|  
|DisplayName|1|識別 [測試條件] 下拉式方塊中的字串。 這個名稱必須是唯一的。 如果兩個條件有相同的顯示名稱，第一個找到的條件會向使用者顯示，並在 Visual Studio 錯誤管理員中顯示警告。|  
|ImplementingType|2|這個參數是用來唯一識別擴充功能。 您必須變更它，以符合屬性放置所在的型別。 此範例會使用 **ResultSetColumnCountCondition** 類型，因此請使用 **typeof(ResultSetColumnCountCondition)** 。 如果您的類型是 **NewTestCondition**，則使用 **typeof(NewTestCondition)** 。|  
  
在這個範例中，您加入兩個屬性。 自訂測試條件的使用者可以使用 ResultSet 屬性，指定要驗證哪個結果集的資料行計數。 然後，使用者可以使用 Count 屬性來指定預期的資料行計數。  
  
針對每個屬性 (Property)，加入三個屬性 (Attribute)：  
  
-   類別目錄名稱，有助於組織屬性。  
  
-   屬性的顯示名稱。  
  
-   屬性的描述。  
  
在屬性上執行驗證，以驗證 ResultSet 屬性的值不小於一，而且 Count 屬性大於零。  
  
Assert 方法執行測試條件的主要工作。 您覆寫 Assert 方法，以驗證預期條件相符。 這個方法提供兩個參數：  
  
-   第一個參數是用來驗證測試條件的資料庫連接。  
  
-   第二個 (更重要的) 參數是結果陣列，針對執行的每個批次，會傳回單一陣列元素。  
  
對於每個測試指令碼都只支援單一批次。 因此，測試條件永遠檢查第一個陣列元素。 陣列元素包含資料集，其中包含針對測試指令碼所傳回的結果集。 在這個範例中，程式碼會驗證資料集的資料表包含正確的資料行數目。 如需詳細資訊，請參閱＜DataSet＞。  
  
您必須設定類別庫，使其包含要簽署的測試條件，可在 [簽署] 索引標籤上的專案屬性中執行這項作業。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
