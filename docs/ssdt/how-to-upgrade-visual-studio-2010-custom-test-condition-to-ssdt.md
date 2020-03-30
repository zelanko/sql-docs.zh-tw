---
title: 將 Visual Studio 2010 自訂測試條件從舊版升級
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 44c895a3-dee0-4032-a60f-812f5fe3c713
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 333ef282fe4e1f9d7af53cd3569371e88018a03f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75251077"
---
# <a name="how-to-upgrade-a-visual-studio-2010-custom-test-condition-from-a-previous-release-to-sql-server-data-tools"></a>HOW TO：將 Visual Studio 2010 自訂測試條件從舊版升級至 SQL Server Data Tools

若要使用在早於 SQL Server Data Tools 的版本中建立的測試單元條件，必須將它升級：  
  
-   [更新參考](#UpdateReferences)  
  
-   [更新類別屬性和型別參考](#UpdateClassAttributesandTypeReference)  
  
-   [安裝升級的測試條件](#ApplytheNewRegistrationProcess)  
  
## <a name="update-references"></a><a name="UpdateReferences"></a>更新參考  
若要更新專案參考：  
  
1.  在 [方案總管]  中按一下 [顯示所有檔案]  (僅限 Visual Basic)。  
  
2.  展開 [方案總管]  中的 [參考]  節點。  
  
3.  以滑鼠右鍵按一下下列組件參考，然後按一下 [移除]  ：  
  
    1.  Microsoft.Data.Schema.UnitTesting  
  
    2.  Microsoft.Data.Schema  
  
4.  在 [專案]  功能表中，或在 [方案總管]  中以滑鼠右鍵按一下專案資料夾，按一下 [加入參考]  。  
  
5.  按一下 [.NET]  索引標籤。  
  
6.  在 [元件名稱]  清單中，選取 [System.ComponentModel.Composition]  ，然後按一下 [確定]  。  
  
7.  加入必要的組件參考。 以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]  。 按一下 [瀏覽]  並巡覽至 C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin 資料夾。 選擇 Microsoft.Data.Tools.Schema.Sql.dll，並按一下 [加入]，然後按一下 [確定]。  
  
8.  按一下 [專案]  功能表上的 [卸載專案]  。  
  
9. 在 [方案總管]  中，以滑鼠右鍵按一下 [專案]  ，然後選擇 [編輯 **.csproj]** `project_name`  。  
  
10. 匯入 `Microsoft.CSharp.targets` 之後，加入下列 Import 陳述式：  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
11. 儲存並關閉檔案。 在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選擇 [重新載入專案]  。  
  
12. 開啟測試條件類別，然後移除以 **Microsoft.Data.Schema** 開頭的所有 Using 陳述式。 最簡單的移除方式是以滑鼠右鍵按一下檔案，依序選擇 [組合管理 Using]  和 [移除和排序]  。 下列 Using 陳述式必須移除：  
  
    ```  
    using Microsoft.Data.Schema.UnitTesting;  
    using Microsoft.Data.Schema.UnitTesting.Conditions;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema;  
    ```  
  
13. 將下列 Using 陳述式加入至檔案 (如果沒有的話)：  
  
    ```  
    using System.ComponentModel;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
    ```  
  
您的測試條件現在就會使用 SQL Server 單元測試組件參考。  
  
## <a name="update-class-attributes-and-type-references"></a><a name="UpdateClassAttributesandTypeReference"></a>更新類別屬性和型別參考  
將較舊的單元測試類別屬性取代為新屬性。 SQL Server 單元測試擴充性現在是以 Managed Extensibility Framework (MEF) 為基礎。 您也必須更新一些型別參考。  
  
### <a name="update-class-attributes"></a>更新類別屬性  
更新程式碼，如下所示：  
  
1.  移除 `DatabaseSchemaProviderCompatibility` 屬性。 這個 (這些) 屬性是舊版的擴充性功能所需，SQL Server 單元測試並不支援。  
  
2.  移除 `DisplayName` 屬性。 顯示名稱會包含在新屬性中。  
  
3.  加入新的 `ExportTestCondition` 屬性。 必須有這個屬性，才能在 SQL Server 單元測試中發現及使用您的測試條件。 `ExportTestCondition` 並取代 `DatabaseSchemaProviderCompatibility` 屬性。 `ExportTestCondition` 接受兩個參數：  
  
    -   `DisplayName` 是第一個參數。 它取代 `DisplayName` 屬性，用來描述這個型別的所有測試條件。  
  
    -   第二個參數是用來唯一識別您的擴充功能。 您可以使用 `typeof(NewTestCondition)` 只傳入型別，因為它應該是唯一的。 不過，如果願意的話，也可以傳遞字串識別碼。  
  
4.  類別定義應該變更如下：  
  
    之前：  
  
    ```  
    [DatabaseSchemaProviderCompatibility(typeof(DatabaseSchemaProvider))]  
    [DatabaseSchemaProviderCompatibility(null)]  
    [DisplayName("NewTestCondition")]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
    之後：  
  
    ```  
    [ExportTestCondition("NewTestCondition ", typeof(NewTestCondition))]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
### <a name="update-type-references"></a>更新型別參考  
SQL Server 單元測試架構中一些型別名稱已經變更。 若要更新程式碼以使用新型別名稱，請使用 [編輯]  功能表中的 [尋找和取代]  。 現在型別名稱開頭為 **Sql**。 類別名稱應該更新如下：  
  
|舊的型別名稱|新的型別名稱|  
|-----------------|-----------------|  
|`ExecutionResult`|`SqlExecutionResult`|  
  
## <a name="install-the-upgraded-test-condition"></a><a name="ApplytheNewRegistrationProcess"></a>安裝升級的測試條件  
在舊版的資料庫單元測試中，可能需要將測試條件安裝至全域組件快取，或建立包含組件資訊的 XML 檔案。 在 SQL Server 單元測試中，不再需要這個額外程序。 (如需詳細資訊，請參閱[編譯專案及安裝測試條件](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md#xxx)。  
  
更新參考之後，驗證組件已簽署及編譯。  
  
接下來，從輸出目錄 (預設為 My Documents\Visual Studio 2010\Projects\\<yoursolutionname>\\<yourprojectname>\bin\Debug\\)，將組件檔複製到 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 目錄。 當 Visual Studio 啟動時，它會識別 TestConditions 目錄中的任何擴充功能，並提供這些擴充功能用於工作階段：  
  
## <a name="upgrade-existing-tests-that-need-to-use-the-new-test-condition"></a>將需要使用新測試條件的現有測試升級  
找出使用舊測試條件且需要使用新條件的所有測試專案。 確定這些測試專案都已升級。 如需詳細資訊，請參閱[升級包含資料庫單元測試的舊版測試專案](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)。  
  
移除舊測試條件的組件參考。  
  
將新的 SQL Server 單元測試加入至專案，在專案中建立已升級測試條件的組件參考。 也必須加入測試類別，以建立參考。 加入參考之後，可以刪除測試類別。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 單元測試的自訂測試條件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
