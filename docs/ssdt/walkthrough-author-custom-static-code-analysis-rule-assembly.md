---
title: 針對 SQL Server 撰寫自訂靜態程式碼分析規則組件
description: 了解如何建立 SQL Server 程式碼分析規則。 設定規則以避免在預存程序、觸發程序與函式中，使用 WAITFOR DELAY 陳述式。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: f7b6ed8c-a4e0-4e33-9858-a8aa40aef309
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 31d183a212ea18f681724d06834041b0a50f752c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896244"
---
# <a name="walkthrough-authoring-a-custom-static-code-analysis-rule-assembly-for-sql-server"></a>為 SQL Server 編寫自訂靜態程式碼分析規則組件的逐步解說

此逐步解說示範用來建立 SQL Server 程式碼分析規則的步驟。 在此逐步解說中建立的規則是用來避開預存程序、觸發程序和函數中的 WAITFOR DELAY 陳述式。  
  
在此逐步解說中，您將使用下列程序，建立自訂規則進行 Transact\-SQL 靜態程式碼分析：  
  
1. 建立類別庫、啟用該專案的簽署，以及新增必要參考。  
  
2. 建立 Visual C\# 自訂規則類別。  
  
3. 建立兩個協助程式 Visual C\# 類別。  
  
4. 將您建立的結果 DLL 複製至 Extensions 目錄，以便安裝它。  
  
5. 驗證新的程式碼分析規則是否就定位。  
  
**先決條件**
  
您需要下列元件才能完成這個逐步解說：  
  
- 您必須已安裝包含 SQL Server Data Tools 和支援 Visual C\# 或 Visual Basic 開發的 Visual Studio 版本。  
  
- 您必須擁有包含 SQL Server 物件的 SQL Server 專案。  
  
- 可以部署資料庫專案的 SQL Server 執行個體。  
  
> [!NOTE]  
> 這個逐步解說適用於已經熟悉 SQL Server Data Tools SQL Server 功能的使用者。 您也應該熟悉 Visual Studio 概念，例如如何建立類別庫及如何使用程式碼編輯器將程式碼加入至類別。  
  
## <a name="creating-a-custom-code-analysis-rule-for-sql-server"></a>建立 SQL Server 的自訂程式碼分析規則  

首先建立類別庫。 若要建立類別庫專案：  
  
1. 建立名稱為 SampleRules 的 Visual C\# 或 Visual Basic 類別庫專案。  
  
2. 將檔案 Class1.cs 重新命名為 AvoidWaitForDelayRule.cs。  
  
3. 在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後按一下 [新增參考]。  
  
4. 選取 [Framework] 索引標籤上的 [System.ComponentModel.Composition]。  
  
5. 按一下 [瀏覽] 並巡覽至 C:\Program Files (x86)\\Microsoft SQL Server\120\SDK\Assemblies 目錄，選取 Microsoft.SqlServer.TransactSql.ScriptDom.dll，然後按一下 [確定]。  
  
6. 接下來，安裝必要的 DACFx 參考。 按一下 [瀏覽] 並巡覽至 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120 目錄。 選擇 Microsoft.SqlServer.Dac.dll、Microsoft.SqlServer.Dac.Extensions.dll 和 Microsoft.Data.Tools.Schema.Sql.dll 項目，按一下 [加入]，然後按一下 [確定]。  
  
    DACFx 二進位檔現在會安裝在 Visual Studio 安裝目錄內。 針對 Visual Studio 2012，<Visual Studio Install Dir> 通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0。 針對 Visual Studio 2013，這通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0。  
  
接下來，您會新增規則將使用的支援類別。  
  
## <a name="creating-the-custom-code-analysis-rule-supporting-classes"></a>建立自訂程式碼分析規則支援類別

在建立規則本身的類別之前，您將新增訪客類別和屬性類別至專案。 這些類別可能有助於建立額外的自訂規則。  
  
您必須定義的第一個類別為 WaitForDelayVisitor 類別，衍生自 [TSqlConcreteFragmentVisitor](https://docs.microsoft.com/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.tsqlconcretefragmentvisitor)。 此類別提供模型中 WAITFOR DELAY 陳述式的存取權。 訪客類別會使用 SQL Server 所提供的 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API。 在此 API 中，Transact\-SQL 程式碼以抽象語法樹 (AST) 表示，而當您想要尋找特定語法物件 (例如 WAITFORDELAY 陳述式) 時，訪客類別可能很有用。 這些物件因為未與特定物件屬性或關係建立關聯，所以可能難以使用物件模型找到，但是使用訪客模式和 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API，就能輕易找到這些物件。  
  
### <a name="defining-the-waitfordelayvisitor-class"></a>定義 WaitForDelayVisitor 類別  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 在 [專案] 功能表上，選取 [新增類別]。 [加入新項目]  對話方塊隨即出現。  
  
3. 在 [名稱] 文字方塊中鍵入 WaitForDelayVisitor.cs，然後按一下 [新增] 按鈕。 WaitForDelayVisitor.cs 檔案隨即新增到 [方案總管] 中的專案。  
  
4. 開啟 WaitForDelayVisitor.cs 檔案並更新內容，以符合下列程式碼：  
  
    ```  
    using System.Collections.Generic;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    namespace SampleRules {  
        class WaitForDelayVistor {}  
    }  
    ```  
  
5. 在類別宣告中，將存取修飾詞變更為 internal，然後從 TSqlConcreteFragmentVisitor 衍生類別：  
  
    ```  
    internal class WaitForDelayVisitor : TSqlConcreteFragmentVisitor {}  
    ```  
  
6. 新增下列程式碼以定義 List 成員變數：  
  
    ```  
    public IList<WaitForStatement> WaitForDelayStatements { get; private set; }  
    ```  
  
7. 加入下列程式碼來定義類別建構函式：  
  
    ```  
    public WaitForDelayVisitor() {  
       WaitForDelayStatments = new List<WaitForStatement>();  
    }  
    ```  
  
8. 加入下列程式碼來覆寫 ExplicitVisit 方法：  
  
    ```  
    public override void ExplicitVisit(WaitForStatement node) {  
       // We are only interested in WAITFOR DELAY occurrences  
       if (node.WaitForOption == WaitForOption.Delay)  
          WaitForDelayStatments.Add(node);  
    }  
    ```  
  
    此方法會造訪模型中的 WAITFOR 陳述式，並將那些已指定 DELAY 選項的陳述式加入至 WAITFOR DELAY 陳述式的清單。 這裡參考的索引鍵類別為 [WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx)。  
  
9. 在 [檔案] 功能表上，按一下 [儲存]。  
  
第二個類別為 LocalizedExportCodeAnalysisRuleAttribute.cs。 這是架構所提供之內建 Microsoft.SqlServer.Dac.CodeAnalysis.ExportCodeAnalysisRuleAttribute 的延伸模組，並支援從資源檔讀取您的規則所使用的 DisplayName 和 Description。 如果您曾經想要以多種語言使用規則，則這是有用的類別。  
  
### <a name="defining-the-localizedexportcodeanalysisruleattribute-class"></a>定義 Localizedexportcodeanalysisruleattribute.cs 類別  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 在 [專案] 功能表上，選取 [新增類別]。 [加入新項目]  對話方塊隨即出現。  
  
3. 在 [名稱] 文字方塊中鍵入 LocalizedExportCodeAnalysisRuleAttribute.cs，然後按一下 [新增] 按鈕。 檔案隨即新增到 [方案總管] 中的專案。  
  
4. 開啟檔案並更新內容，以符合下列程式碼：  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using System;  
    using System.Globalization;  
    using System.Reflection;  
    using System.Resources;  
  
    namespace SampleRules  
    {  
  
        internal class LocalizedExportCodeAnalysisRuleAttribute : ExportCodeAnalysisRuleAttribute  
        {  
            private readonly string _resourceBaseName;  
            private readonly string _displayNameResourceId;  
            private readonly string _descriptionResourceId;  
  
            private ResourceManager _resourceManager;  
            private string _displayName;  
            private string _descriptionValue;  
  
            /// <summary>  
            /// Creates the attribute, with the specified rule ID, the fully qualified  
            /// name of the resource file that will be used for looking up display name  
            /// and description, and the Ids of those resources inside the resource file.  
            /// </summary>  
            public LocalizedExportCodeAnalysisRuleAttribute(  
                string id,  
                string resourceBaseName,  
                string displayNameResourceId,  
                string descriptionResourceId)  
                : base(id, null)  
            {  
                _resourceBaseName = resourceBaseName;  
                _displayNameResourceId = displayNameResourceId;  
                _descriptionResourceId = descriptionResourceId;  
            }  
  
            /// <summary>  
            /// Rules in a different assembly would need to overwrite this  
            /// </summary>  
            /// <returns></returns>  
            protected virtual Assembly GetAssembly()  
            {  
                return GetType().Assembly;  
            }  
  
            private void EnsureResourceManagerInitialized()  
            {  
                var resourceAssembly = GetAssembly();  
  
                try  
                {  
                    _resourceManager = new ResourceManager(_resourceBaseName, resourceAssembly);  
                }  
                catch (Exception ex)  
                {  
                    var msg = String.Format(CultureInfo.CurrentCulture, RuleResources.CannotCreateResourceManager, _resourceBaseName, resourceAssembly);  
                    throw new RuleException(msg, ex);  
                }  
            }  
  
            private string GetResourceString(string resourceId)  
            {  
                EnsureResourceManagerInitialized();  
                return _resourceManager.GetString(resourceId, CultureInfo.CurrentUICulture);  
            }  
  
            /// <summary>  
            /// Overrides the standard DisplayName and looks up its value inside a resources file  
            /// </summary>  
            public override string DisplayName  
            {  
                get  
                {  
                    if (_displayName == null)  
                    {  
                        _displayName = GetResourceString(_displayNameResourceId);  
                    }  
                    return _displayName;  
                }  
            }  
  
            /// <summary>  
            /// Overrides the standard Description and looks up its value inside a resources file  
            /// </summary>  
            public override string Description  
            {  
                get  
                {  
                    if (_descriptionValue == null)  
                    {   
                        _descriptionValue = GetResourceString(_descriptionResourceId);  
                    }  
                    return _descriptionValue;  
                }  
            }  
        }  
    }  
    ```  
  
接下來，加入資源檔，其會定義規則名稱、規則說明，以及規則將出現在規則組態介面的哪個類別中。  
  
### <a name="to-add-a-resource-file-and-three-resource-strings"></a>若要加入一個資源檔和三個資源字串  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 在 [專案] 功能表上，選取 [新增項目]。 [加入新項目]  對話方塊隨即出現。  
  
3. 在 [已安裝的範本] 清單中，按一下 [一般]。  
  
4. 在詳細資料窗格中，按一下 [資源檔]。  
  
5. 在 [名稱] 中，鍵入 RuleResources.resx。 資源編輯器隨即出現，沒有已定義的資源。  
  
6. 定義四個資源字串，如下所示：  
  
    |名稱|值|  
    |--------|---------|  
    |AvoidWaitForDelay_ProblemDescription|已在 {0} 找到 WAITFOR DELAY 陳述式。|  
    |AvoidWaitForDelay_RuleName|避免在預存程序、函數和觸發程序中使用 WaitFor Delay 陳述式。|  
    |CategorySamples|SamplesCategory|  
    |CannotCreateResourceManager|無法從 {1} 建立 {0} 的 ResourceManager。|  
  
7. 按一下 [檔案] 功能表上的 [儲存 RuleResources.resx]。  
  
接下來，定義一個參考資源檔中資源的類別，Visual Studio 使用這些資源在使用者介面顯示規則的相關資訊。  
  
### <a name="defining-the-sampleconstants-class"></a>定義 SampleConstants 類別  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 在 [專案] 功能表上，選取 [新增類別]。 [加入新項目]  對話方塊隨即出現。  
  
3. 在 [名稱] 文字方塊中鍵入 SampleRuleConstants.cs，然後按一下 [新增] 按鈕。 SampleRuleConstants.cs 檔案隨即新增到 [方案總管] 中的專案。  
  
4. 開啟 SampleRuleConstants.cs 檔案，然後將下列 Using 陳述式新增到檔案：  
  
    ```  
    namespace SampleRules  
    {   
        internal static class RuleConstants  
        {  
            /// <summary>  
            /// The name of the resources file to use when looking up rule resources  
            /// </summary>  
            public const string ResourceBaseName = "Public.Dac.Samples.Rules.RuleResources";  
  
            /// <summary>  
            /// Lookup name inside the resources file for the select asterisk rule name  
            /// </summary>  
            public const string AvoidWaitForDelay_RuleName = "AvoidWaitForDelay_RuleName";  
            /// <summary>  
            /// Lookup ID inside the resources file for the select asterisk description  
            /// </summary>  
            public const string AvoidWaitForDelay_ProblemDescription = "AvoidWaitForDelay_ProblemDescription";  
  
            /// <summary>  
            /// The design category (should not be localized)  
            /// </summary>  
            public const string CategoryDesign = "Design";  
  
            /// <summary>  
            /// The performance category (should not be localized)  
            /// </summary>  
            public const string CategoryPerformance = "Design";  
        }  
    }  
    ```  
  
5. 按一下 [檔案] > [儲存]。  
  
## <a name="creating-the-custom-code-analysis-rule-class"></a>建立自訂程式碼分析規則類別

既然已加入自訂程式碼分析規則將使用的 Helper 類別，那麼您將建立自訂規則類別，並將它命名為 AvoidWaitForDelayRule。 AvoidWaitForDelayRule 自訂規則將用來協助資料庫開發人員避免在預存程序、觸發程序和函數中使用 WAITFOR DELAY 陳述式。  
  
### <a name="creating-the-avoidwaitfordelayrule-class"></a>建立 AvoidWaitForDelayRule 類別  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 在 [專案] 功能表上，選取 [新增類別]。 [加入新項目]  對話方塊隨即出現。  
  
3. 在 [名稱] 文字方塊中鍵入 AvoidWaitForDelayRule.cs，然後按一下 [新增]。 AvoidWaitForDelayRule.cs 檔案隨即新增到 [方案總管] 中的專案。  
  
4. 開啟 AvoidWaitForDelayRule.cs 檔案，然後將下列 Using 陳述式新增到檔案：  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;   
    namespace SampleRules {  
        class AvoidWaitForDelayRule {}  
    }  
    ```  
  
5. 在 AvoidWaitForDelayRule 類別宣告中，將存取修飾詞變更為 public：  
  
    ```  
    /// <summary>  
    /// This is a rule that returns a warning message   
    /// whenever there is a WAITFOR DELAY statement appears inside a subroutine body.  
    /// This rule only applies to stored procedures, functions and triggers.  
    /// </summary>  
    public sealed class AvoidWaitForDelayRule  
    ```  
  
6. 從 Microsoft.SqlServer.Dac.CodeAnalysis.SqlCodeAnalysisRule 基底類別衍生 AvoidWaitForDelayRule 類別︰  
  
    ```  
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    ```  
  
7. 將 Localizedexportcodeanalysisruleattribute.cs 新增到您的類別。  
  
    LocalizedExportCodeAnalysisRuleAttribute 允許程式碼分析服務探索自訂程式碼分析規則。 只有以 ExportCodeAnalysisRuleAttribute (或衍生自此項的屬性) 標示的類別才能在程式碼分析中使用。  
  
    LocalizedExportCodeAnalysisRuleAttribute 提供服務所使用的一些必要中繼資料。 這包括此規則的唯一識別碼、將顯示在 Visual Studio 使用者介面的顯示名稱，以及您的規則在識別問題時可以使用的說明。  
  
    ```  
    [LocalizedExportCodeAnalysisRule(AvoidWaitForDelayRule.RuleId,  
        RuleConstants.ResourceBaseName,  
        RuleConstants.AvoidWaitForDelay_RuleName,   
        RuleConstants.AvoidWaitForDelay_ProblemDescription  
        Category = RuleConstants.CategoryPerformance,   
        RuleScope = SqlRuleScope.Element)]   
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    {  
       /// <summary>  
       /// The Rule ID should resemble a fully-qualified class name. In the Visual Studio UI  
       /// rules are grouped by "Namespace + Category", and each rule is shown using "Short ID: DisplayName".  
       /// For this rule, that means the grouping will be "Public.Dac.Samples.Performance", with the rule  
       /// shown as "SR1004: Avoid using WaitFor Delay statements in stored procedures, functions and triggers."  
       /// </summary>  
       public const string RuleId = "RuleSamples.SR1004";  
    }  
    ```  
  
    因為此規則會分析特定元素，所以 RuleScope 屬性應為 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Element。 對於模型中的每一個相符元素，將呼叫一次規則。 如果您想分析整個模型，就可以改用 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Model。  
  
8. 新增會設定 Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.SupportedElementTypes 的建構函式。 這是元素範圍規則的必要項。 它會定義將套用此規則的元素類型。 在此情況下，規則將套用至預存程序，觸發程序和函數。 請注意，Microsoft.SqlServer.Dac.Model.ModelSchema 類別會列出所有可供分析的元素類型。  
  
    ```  
    public AvoidWaitForDelayRule()  
    {  
       // This rule supports Procedures, Functions and Triggers. Only those objects will be passed to the Analyze method  
       SupportedElementTypes = new[]  
       {  
          // Note: can use the ModelSchema definitions, or access the TypeClass for any of these types  
          ModelSchema.ExtendedProcedure,  
          ModelSchema.Procedure,  
          ModelSchema.TableValuedFunction,  
          ModelSchema.ScalarFunction,  
  
          ModelSchema.DatabaseDdlTrigger,  
          ModelSchema.DmlTrigger,  
          ModelSchema.ServerDdlTrigger  
       };  
    }  
    ```  
  
9. 為 Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.Analyze(Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext) 方法新增覆寫，其使用 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext 作為輸入參數。 此方法會傳回潛在問題的清單。  
  
    方法會從內容參數獲得 Microsoft.SqlServer.Dac.Model.TSqlModel、Microsoft.SqlServer.Dac.Model.TSqlObject 和 [TSqlFragment](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlfragment.aspx)。 然後，使用 WaitForDelayVisitor 類別，取得模型中所有 WAITFOR DELAY 陳述式的清單。  
  
    對於該清單中的每個 [WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx) 建立 Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleProblem。  
  
    ```  
    /// <summary>  
    /// For element-scoped rules the Analyze method is executed once for every matching   
    /// object in the model.   
    /// </summary>  
    /// <param name="ruleExecutionContext">The context object contains the TSqlObject being   
    /// analyzed, a TSqlFragment  
    /// that's the AST representation of the object, the current rule's descriptor, and a   
    /// reference to the model being  
    /// analyzed.  
    /// </param>  
    /// <returns>A list of problems should be returned. These will be displayed in the Visual   
    /// Studio error list</returns>  
    public override IList<SqlRuleProblem> Analyze(  
        SqlRuleExecutionContext ruleExecutionContext)  
    {  
         IList<SqlRuleProblem> problems = new List<SqlRuleProblem>();  
  
         TSqlObject modelElement = ruleExecutionContext.ModelElement;  
  
         // this rule does not apply to inline table-valued function  
         // we simply do not return any problem in that case.  
         if (IsInlineTableValuedFunction(modelElement))  
         {  
             return problems;  
         }  
  
         string elementName = GetElementName(ruleExecutionContext, modelElement);  
  
         // The rule execution context has all the objects we'll need, including the   
         // fragment representing the object,  
         // and a descriptor that lets us access rule metadata  
         TSqlFragment fragment = ruleExecutionContext.ScriptFragment;  
         RuleDescriptor ruleDescriptor = ruleExecutionContext.RuleDescriptor;  
  
         // To process the fragment and identify WAITFOR DELAY statements we will use a   
         // visitor   
         WaitForDelayVisitor visitor = new WaitForDelayVisitor();  
         fragment.Accept(visitor);  
         IList<WaitForStatement> waitforDelayStatements = visitor.WaitForDelayStatements;  
  
         // Create problems for each WAITFOR DELAY statement found   
         // When creating a rule problem, always include the TSqlObject being analyzed. This   
         // is used to determine  
         // the name of the source this problem was found in and a best guess as to the   
         // line/column the problem was found at.  
         //  
         // In addition if you have a specific TSqlFragment that is related to the problem   
         //also include this  
         // since the most accurate source position information (start line and column) will   
         // be read from the fragment  
         foreach (WaitForStatement waitForStatement in waitforDelayStatements)  
         {  
            SqlRuleProblem problem = new SqlRuleProblem(  
                String.Format(CultureInfo.CurrentCulture,   
                    ruleDescriptor.DisplayDescription, elementName),  
                modelElement,  
                waitForStatement);  
            problems.Add(problem);  
        }  
        return problems;  
    }  
  
    private static string GetElementName(  
        SqlRuleExecutionContext ruleExecutionContext,   
        TSqlObject modelElement)  
    {  
        // Get the element name using the built in DisplayServices. This provides a number of   
        // useful formatting options to  
        // make a name user-readable  
        var displayServices = ruleExecutionContext.SchemaModel.DisplayServices;  
        string elementName = displayServices.GetElementName(  
            modelElement, ElementNameStyle.EscapedFullyQualifiedName);  
        return elementName;  
    }  
  
    private static bool IsInlineTableValuedFunction(TSqlObject modelElement)  
    {  
        return TableValuedFunction.TypeClass.Equals(modelElement.ObjectType)  
                       && FunctionType.InlineTableValuedFunction ==   
            modelElement.GetMetadata<FunctionType>(TableValuedFunction.FunctionType);  
    }  
    ```  
  
10. 按一下 [檔案] > [儲存]。  
  
### <a name="building-the-class-library"></a>建置類別庫  
  
1. 在 [專案] 功能表上，按一下 [SampleRules 屬性]。  
  
2. 按一下 [ **簽署** ] 索引標籤。  
  
3. 按一下 [ **簽署組件**]。  
  
4. 在 [選擇強式名稱金鑰檔案] 中，按一下 **<New>** 。  
  
5. 在 [建立強式名稱金鑰] 對話方塊中的 [金鑰檔案名稱]，鍵入 MyRefKey。  
  
6. (選擇性) 您可以為強式名稱金鑰檔指定密碼。  
  
7. 按一下 [確定]。  
  
8. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
9. 在 [建置] 功能表上，按一下 [建置方案]。  
  
下一步，您必須安裝組件，以便在建置及部署 SQL Server 專案時將其載入。  
  
## <a name="install-a-static-code-analysis-rule"></a>安裝靜態程式碼分析規則

若要安裝規則，您必須將組件和已建立關聯的 .pdb 檔案複製到 Extensions 資料夾。  
  
### <a name="to-install-the-samplerules-assembly"></a>若要安裝 SampleRules 組件

接下來，將組件資訊複製到 Extensions 目錄。 當 Visual Studio 啟動時，它會識別 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions 目錄和子目錄中的任何延伸模組，並讓這些延伸模組可供使用。  
  
針對 Visual Studio 2012，<Visual Studio Install Dir> 通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0。 針對 Visual Studio 2013，這通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0。  
  
將 SampleRules.dll 組件檔從輸出目錄複製到 <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions 目錄。 根據預設，編譯過的 .dll 檔案的路徑是 YourSolutionPath\YourProjectPath\bin\Debug 或 YourSolutionPath\YourProjectPath\bin\Release。  
  
您的規則現在應該已完成安裝，一旦重新啟動 Visual Studio，即會出現。 接下來，啟動新的 Visual Studio 工作階段並建立資料庫專案。  
  
### <a name="starting-a-new-visual-studio-session-and-creating-a-database-project"></a>啟動新的 Visual Studio 工作階段並建立資料庫專案  
  
1. 啟動第二個 Visual Studio 工作階段。  
  
2. 按一下 [檔案] > [新增] > [專案]。  
  
3. 在 [新增專案]**** 對話方塊的 [已安裝的範本]**** 清單中，展開 **SQL Server** 節點，然後按一下 [SQL Server 資料庫專案]****。  
  
4. 在 [名稱] 文字方塊中鍵入 SampleRulesDB，然後按一下 [確定]。  
  
最後，您會看到新的規則顯示在 SQL Server 專案中。 若要檢視新的 AvoidWaitForRule 程式碼分析規則：  
  
1. 在 [方案總管] 中，選取 SampleRules 專案。  
  
2. 按一下 [專案] 功能表上的 [屬性]。 隨即顯示 SampleRulesDB 屬性頁面。  
  
3. 按一下 [程式碼分析]。 您應該看到名稱為 RuleSamples.CategorySamples 的新分類。  
  
4. 展開 RuleSamples.CategorySamples。 您應該會看到 SR1004：避免在預存程序、觸發程序和函式中使用 WAITFOR DELAY 陳述式。  
  
## <a name="see-also"></a>另請參閱

[資料庫程式碼分析規則的擴充性概觀](../ssdt/overview-of-extensibility-for-database-code-analysis-rules.md)