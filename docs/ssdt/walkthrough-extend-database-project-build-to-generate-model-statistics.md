---
title: 逐步解說：擴充資料庫專案組建，以產生模型統計資料 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d44935ce-63bf-46df-976a-5a54866c8119
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9841763f003b0a177913da72cf6dd3efd0c4d3d3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523416"
---
# <a name="walkthrough-extend-database-project-build-to-generate-model-statistics"></a>逐步解說：擴充資料庫專案組建，以產生模型統計資料
您可以建立組建參與者，以便在建置資料庫時執行自訂動作。 在這個逐步解說，會建立名為 ModelStatistics 的組建參與者，以便在建置資料庫專案時從 SQL 資料庫模型輸出統計資料。 因為在建置時這個組建參與者採用參數，所以需要某些其他步驟。  
  
在本逐步解說中，您將會完成下列主要工作：  
  
-   [建立組建參與者](#CreateBuildContributor)  
  
-   [安裝組建參與者](#InstallBuildContributor)  
  
-   [測試您的組建參與者](#TestBuildContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
您需要下列元件才能完成這個逐步解說：  
  
-   您必須已安裝包含 SQL Server Data Tools (SSDT) 和支援 C# 或 VB 開發的 Visual Studio 版本。  
  
-   您必須擁有包含 SQL 物件的 SQL 專案。  
  
> [!NOTE]  
> 這個逐步解說適用於已經熟悉 SSDT SQL 功能的使用者。 您也應該熟悉基本的 Visual Studio 概念，例如如何建立類別庫及如何使用程式碼編輯器將程式碼加入至類別。  
  
## <a name="build-contributor-background"></a>組建參與者背景  
在專案建置期間，在代表專案的模型產生後但在專案儲存到磁碟之前的時間內，執行組建參與者。 它們可用於許多狀況中，例如：  
  
-   驗證模型內容以及向呼叫端回報驗證錯誤。 這可透過將錯誤加入至清單當做參數傳遞給 OnExecute 方法來完成。  
  
-   產生模型統計資料並向使用者回報。 這是這裡示範的範例。  
  
組建參與者的主要進入點是 OnExecute 方法。 繼承自 BuildContributor 的所有類別都必須實作這個方法。 BuildContributorContext 物件會傳遞給這個方法，其中包含組建的所有相關資料，例如資料庫模型、組建屬性，以及組建參與者所使用的引數/檔案。  
  
**TSqlModel 和資料庫模型 API**  
  
最有用的物件就是資料庫模型，由 TSqlModel 物件表示。 這是資料庫的邏輯表示，包括所有資料表、檢視表和其他項目，加上物件之間的關聯性。 還有強式型別的結構描述，可用於查詢特定類型的項目和周遊相關關聯性。 在逐步解說程式碼中您會看到這個用法的範例。  
  
在這個逐步解說中，範例參與者使用的某些命令如下：  
  
|**類別**|**方法/屬性**|**說明**|  
|-------------|------------------------|-------------------|  
|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)|GetObjects()|查詢模型以取得物件資訊，這是模型應用程式開發介面的主要進入點。 只可以查詢最上層型別，例如資料表或檢視表，資料行這類的型別只可以透過周遊模型找到。 如果未指定 ModelTypeClass 篩選，會傳回所有最上層型別。|  
|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|GetReferencedRelationshipInstances()|尋找與目前 TSqlObject 參考之項目的關聯性。 例如，針對資料表，這會傳回例如資料表資料行的物件。 在此情況下，ModelRelationshipClass 篩選可用來指定查詢的精確關聯性 (例如使用 "Table.Columns" 篩選確保只會傳回資料行)。<br /><br />有一些類似的方法，例如 GetReferencingRelationshipInstances、GetChildren 和 GetParent。 如需詳細資訊，請參閱應用程式開發介面文件。|  
  
**唯一識別您的參與者**  
  
在建置程序期間，自訂參與者是從標準擴充目錄載入。 組建參與者是由 [ExportBuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportbuildcontributorattribute.aspx) 屬性加以識別。 參與者需要這個屬性，才能設定為可搜尋的。 這個屬性應看起來如下：  
  
```  
[ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
  
```  
  
在此案例中，屬性的第一個參數應該是唯一識別碼，用來識別專案檔中的參與者。 最佳作法是結合程式庫的命名空間 (在這個逐步解說中為 "ExampleContributors") 與類別名稱 (在這個逐步解說中為 "ModelStatistics")，以產生識別碼。 在這個逐步解說後面，您會看到這個命名空間如何用來指定應該執行參與者。  
  
## <a name="CreateBuildContributor"></a>建立組建參與者  
若要建立組建參與者，您必須執行下列工作：  
  
-   建立類別庫專案並加入必要參考。  
  
-   定義繼承自 [BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)名稱為 ModelStatistics 的類別。  
  
-   覆寫 OnExecute 方法。  
  
-   加入一些私用 Helper 方法。  
  
-   建置產生的組件。  
  
#### <a name="to-create-a-class-library-project"></a>若要建立類別庫專案  
  
1.  建立名稱為 MyBuildContributor 的 Visual Basic 或 Visual C# 類別庫專案。  
  
2.  將 "Class1.cs" 檔案重新命名為 "ModelStatistics.cs"。  
  
3.  在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後按一下 [新增參考]。  
  
4.  選取 **System.ComponentModel.Composition** 項目，然後按一下 [ **確定**]。  
  
5.  加入必要的 SQL 參考：以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]。 按一下 [ **瀏覽** ] 按鈕。 巡覽至 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 資料夾。 選擇 **Microsoft.SqlServer.Dac.dll**、 **Microsoft.SqlServer.Dac.Extensions.dll**和 **Microsoft.Data.Tools.Schema.Sql.dll** 項目，然後按一下 [ **確定**]。  
  
    下一步，開始將程式碼加入至類別。  
  
#### <a name="to-define-the-modelstatistics-class"></a>若要定義 ModelStatistics 類別  
  
1.  ModelStatistics 類別會傳遞給 OnExecute 方法的處理資料庫模型，並產生詳述模型內容的 XML 報表。  
  
    在程式碼編輯器中，更新 ModelStatistics.cs 檔案以符合下列程式碼：  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Linq;  
    using System.Xml.Linq;  
    using Microsoft.Data.Schema;  
    using Microsoft.Data.Schema.Build;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema.SchemaModel;  
    using Microsoft.Data.Schema.Sql;  
  
    namespace ExampleContributors  
    {  
    /// <summary>  
        /// A BuildContributor that generates statistics about a model and saves this to the output directory.  
        /// Will only run if a "GenerateModelStatistics=true" contributor argument is set in the project file, or a targets file.   
        /// Statistics can be sorted by "none, "name" or "value", with "none" being the default sort behavior.  
        ///   
        /// To set contributor arguments in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
        ///     </ContributorArguments>  
        /// <PropertyGroup>      
        ///   
        /// This will generate model statistics when building in Debug mode only - remove the condition to generate in all build modes.  
        /// </summary>  
        [ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
        public class ModelStatistics : BuildContributor  
        {  
            public const string GenerateModelStatistics = "ModelStatistics.GenerateModelStatistics";  
            public const string SortModelStatisticsBy = "ModelStatistics.SortModelStatisticsBy";  
            public const string OutDir = "ModelStatistics.OutDir";  
            public const string ModelStatisticsFilename = "ModelStatistics.xml";  
            private enum SortBy { None, Name, Value };  
            private static Dictionary<string, SortBy> SortByMap = new Dictionary<string, SortBy>(StringComparer.OrdinalIgnoreCase)  
            {  
                { "none", SortBy.None },  
                { "name", SortBy.Name },  
                { "value", SortBy.Value },  
            };  
  
            private SortBy _sortBy = SortBy.None;  
  
            /// <summary>  
            /// Override the OnExecute method to perform actions when you build a database project.  
            /// </summary>  
            protected override void OnExecute(BuildContributorContext context, IList<ExtensibilityError> errors)  
            {  
                // handle related arguments, passed in as part of  
                // the context information.  
                bool generateModelStatistics;  
                ParseArguments(context.Arguments, errors, out generateModelStatistics);  
  
                // Only generate statistics if requested to do so  
                if (generateModelStatistics)  
                {  
                    // First, output model-wide information, such  
                    // as the type of database schema provider (DSP)  
                    // and the collation.  
                    StringBuilder statisticsMsg = new StringBuilder();  
                    statisticsMsg.AppendLine(" ")  
                                 .AppendLine("Model Statistics:")  
                                 .AppendLine("===")  
                                 .AppendLine(" ");  
                    errors.Add(new ExtensibilityError(statisticsMsg.ToString(), Severity.Message));  
  
                    var model = context.Model;  
  
                    // Start building up the XML that will later  
                    // be serialized.  
                    var xRoot = new XElement("ModelStatistics");  
  
                    SummarizeModelInfo(model, xRoot, errors);  
  
                    // First, count the elements that are contained   
                    // in this model.  
                    IList<TSqlObject> elements = model.GetObjects(DacQueryScopes.UserDefined).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "UserDefinedElements", xRoot, errors);  
  
                    // Now, count the elements that are defined in  
                    // another model. Examples include built-in types,  
                    // roles, filegroups, assemblies, and any   
                    // referenced objects from another database.  
                    elements = model.GetObjects(DacQueryScopes.BuiltIn | DacQueryScopes.SameDatabase | DacQueryScopes.System).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "OtherElements", xRoot, errors);  
  
                    // Now, count the number of each type  
                    // of relationship in the model.  
                    SurveyRelationships(model, xRoot, errors);  
  
                    // Determine where the user wants to save  
                    // the serialized XML file.  
                    string outDir;  
                    if (context.Arguments.TryGetValue(OutDir, out outDir) == false)  
                    {  
                        outDir = ".";  
                    }  
                    string filePath = Path.Combine(outDir, ModelStatisticsFilename);  
                    // Save the XML file and tell the user  
                    // where it was saved.  
                    xRoot.Save(filePath);  
                    ExtensibilityError resultArg = new ExtensibilityError("Result was saved to " + filePath, Severity.Message);  
                    errors.Add(resultArg);  
                }  
            }  
  
            /// <summary>  
            /// Examine the arguments provided by the user  
            /// to determine if model statistics should be generated  
            /// and, if so, how the results should be sorted.  
            /// </summary>  
            private void ParseArguments(IDictionary<string, string> arguments, IList<ExtensibilityError> errors, out bool generateModelStatistics)  
            {  
                // By default, we don't generate model statistics  
                generateModelStatistics = false;  
  
                // see if the user provided the GenerateModelStatistics   
                // option and if so, what value was it given.  
                string valueString;  
                arguments.TryGetValue(GenerateModelStatistics, out valueString);  
                if (string.IsNullOrWhiteSpace(valueString) == false)  
                {  
                    if (bool.TryParse(valueString, out generateModelStatistics) == false)  
                    {  
                        generateModelStatistics = false;  
  
                        // The value was not valid from the end user  
                        ExtensibilityError invalidArg = new ExtensibilityError(  
                            GenerateModelStatistics + "=" + valueString + " was not valid.  It can be true or false", Severity.Error);  
                        errors.Add(invalidArg);  
                        return;  
                    }  
                }  
  
                // Only worry about sort order if the user requested  
                // that we generate model statistics.  
                if (generateModelStatistics)  
                {  
                    // see if the user provided the sort option and  
                    // if so, what value was provided.  
                    arguments.TryGetValue(SortModelStatisticsBy, out valueString);  
                    if (string.IsNullOrWhiteSpace(valueString) == false)  
                    {  
                        SortBy sortBy;  
                        if (SortByMap.TryGetValue(valueString, out sortBy))  
                        {  
                            _sortBy = sortBy;  
                        }  
                        else  
                        {  
                            // The value was not valid from the end user  
                            ExtensibilityError invalidArg = new ExtensibilityError(  
                                SortModelStatisticsBy + "=" + valueString + " was not valid.  It can be none, name, or value", Severity.Error);  
                            errors.Add(invalidArg);  
                        }  
                    }  
                }  
            }  
  
            /// <summary>  
            /// Retrieve the database schema provider for the  
            /// model and the collation of that model.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SummarizeModelInfo(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // use a Dictionary to accumulate the information  
                // that will later be output.  
                var info = new Dictionary<string, string>();  
  
                // Two things of interest: the database schema  
                // provider for the model, and the language id and  
                // case sensitivity of the collation of that  
                // model  
                info.Add("Version", model.Version.ToString());  
  
                TSqlObject options = model.GetObjects(DacQueryScopes.UserDefined, DatabaseOptions.TypeClass).FirstOrDefault();  
                if (options != null)  
                {  
                    info.Add("Collation", options.GetProperty<string>(DatabaseOptions.Collation));  
                }  
  
                // Output the accumulated information and add it to   
                // the XML.  
                OutputResult("Basic model info", info, xContainer, errors);  
            }  
  
            /// <summary>  
            /// For a provided list of model elements, count the number  
            /// of elements for each class name, sorted as specified  
            /// by the user.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private void Summarize<T>(IList<T> set, Func<T, string> groupValue, string category, XElement xContainer, IList<ExtensibilityError> errors)  
            { // Use a Dictionary to keep all summarized information  
                var statistics = new Dictionary<string, int>();  
  
                // For each element in the provided list,  
                // count items based on the specified grouping  
                var groups =  
                    from item in set  
                    group item by groupValue(item) into g  
                    select new { g.Key, Count = g.Count() };  
  
                // order the groups as requested by the user  
                if (this._sortBy == SortBy.Name)  
                {  
                    groups = groups.OrderBy(group => group.Key);  
                }  
                else if (this._sortBy == SortBy.Value)  
                {  
                    groups = groups.OrderBy(group => group.Count);  
                }  
  
                // build the Dictionary of accumulated statistics  
                // that will be passed along to the OutputResult method.  
                foreach (var item in groups)  
                {  
                    statistics.Add(item.Key, item.Count);  
                }  
  
                statistics.Add("subtotal", set.Count);  
                statistics.Add("total items", groups.Count());  
  
                // output the results, and build up the XML  
                OutputResult(category, statistics, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Iterate over all model elements, counting the  
            /// styles and types for relationships that reference each   
            /// element  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SurveyRelationships(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // get a list that contains all elements in the model  
                var elements = model.GetObjects(DacQueryScopes.All);  
                // We are interested in all relationships that  
                // reference each element.  
                var entries =  
                    from element in elements  
                    from entry in element.GetReferencedRelationshipInstances(DacExternalQueryScopes.All)  
                    select entry;  
  
                // initialize our counting buckets  
                var composing = 0;  
                var hierachical = 0;  
                var peer = 0;  
  
                // process each relationship, adding to the   
                // appropriate bucket for style and type.  
                foreach (var entry in entries)  
                {  
                    switch (entry.Relationship.Type)  
                    {  
                        case RelationshipType.Composing:  
                            ++composing;  
                            break;  
                        case RelationshipType.Hierarchical:  
                            ++hierachical;  
                            break;  
                        case RelationshipType.Peer:  
                            ++peer;  
                            break;  
                        default:  
                            break;  
                    }  
                }  
  
                // build a dictionary of data to pass along  
                // to the OutputResult method.  
                var stat = new Dictionary<string, int>  
                {  
                    {"Composing", composing},  
                    {"Hierarchical", hierachical},  
                    {"Peer", peer},  
                    {"subtotal", entries.Count()}  
                };  
  
                OutputResult("Relationships", stat, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Performs the actual output for this contributor,  
            /// writing the specified set of statistics, and adding any   
            /// output information to the XML being constructed.  
            /// </summary>  
            private static void OutputResult<T>(string category, Dictionary<string, T> statistics, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                var maxLen = statistics.Max(stat => stat.Key.Length) + 2;  
                var format = string.Format("{{0, {0}}}: {{1}}", maxLen);  
  
                StringBuilder resultMessage = new StringBuilder();  
                //List<ExtensibilityError> args = new List<ExtensibilityError>();  
                resultMessage.AppendLine(category);  
                resultMessage.AppendLine("-----------------");  
  
                // Remove any blank spaces from the category name  
                var xCategory = new XElement(category.Replace(" ", ""));  
                xContainer.Add(xCategory);  
  
                foreach (var item in statistics)  
                {  
                    //Console.WriteLine(format, item.Key, item.Value);  
                    var entry = string.Format(format, item.Key, item.Value);  
                    resultMessage.AppendLine(entry);  
                    // Replace any blank spaces in the element key with  
                    // underscores.  
                    xCategory.Add(new XElement(item.Key.Replace(' ', '_'), item.Value));  
                }  
                resultMessage.AppendLine(" ");  
                errors.Add(new ExtensibilityError(resultMessage.ToString(), Severity.Message));  
            }  
        }  
    }  
  
    ```  
  
    下一步，您會建置類別庫。  
  
### <a name="to-sign-and-build-the-assembly"></a>若要簽署和建置組件  
  
1.  按一下 [ **專案** ] 功能表上的 [ **MyBuildContributor 屬性**]。  
  
2.  按一下 [ **簽署** ] 索引標籤。  
  
3.  按一下 [ **簽署組件**]。  
  
4.  在 [選擇強式名稱金鑰檔案] 中，按一下 **<New>**。  
  
5.  在 [ **建立強式名稱金鑰** ] 對話方塊中的 [ **金鑰檔名稱**]，輸入 **MyRefKey**。  
  
6.  (選擇性) 您可以為強式名稱金鑰檔指定密碼。  
  
7.  按一下 [確定] 。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
9. 按一下 [ **建置** ] 功能表上的 [ **建置方案**]。  
  
    下一步，您必須安裝組件，以便在建置 SQL 專案時將其載入。  
  
## <a name="InstallBuildContributor"></a>安裝組建參與者  
若要安裝組建參與者，您必須將組件和關聯的 .pdb 檔案複製到 Extensions 資料夾。  
  
#### <a name="to-install-the-mybuildcontributor-assembly"></a>若要安裝 MyBuildContributor 組件  
  
1.  接下來，將組件資訊複製到 Extensions 目錄。 當 Visual Studio 啟動時，它會識別 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄和子目錄中的任何擴充功能，並讓這些擴充功能可供使用。  
  
2.  將 **MyBuildContributor.dll** 組件檔案從輸出目錄複製到 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄。  
  
    > [!NOTE]  
    > 根據預設，編譯過的 .dll 檔案的路徑是 YourSolutionPath\YourProjectPath\bin\Debug 或 YourSolutionPath\YourProjectPath\bin\Release。  
  
## <a name="TestBuildContributor"></a>執行或測試您的組建參與者  
若要執行或測試組建參與者，您必須執行下列工作：  
  
-   將屬性加入至要建置的 .sqlproj 檔案。  
  
-   使用 MSBuild 並提供適當的參數，建置資料庫專案。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>將屬性加入至 SQL 專案檔 (.sqlproj)  
您一定要更新 SQL 專案檔，指定要執行之參與者的識別碼。 此外，因為這個建立參與者會從 MSBuild 接收命令列參數，您必須修改 SQL 專案，讓使用者可透過 MSBuild 傳遞這些參數。  
  
您可以使用下列其中一種作法：  
  
-   手動修改 .sqlproj 檔案，加入必要的引數。 如果您不想要在大量專案中重複使用組建參與者，可以選擇這樣做。 如果您選擇這個選項，將下列陳述式加入至 .sqlproj 檔案，在檔案的第一個 Import 節點後面：  
  
    ```  
    /// <PropertyGroup>  
    ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
    ///         $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
    ///     </ContributorArguments>  
    /// <PropertyGroup>  
  
    ```  
  
-   第二個方法是建立包含必要參與者引數的目標檔案。 如果您針對多個專案使用同一個參與者，因為其中包含預設值，這非常有用。  
  
    在此情況下，請在 MSBuild 擴充路徑建立目標檔案：  
  
    1.  巡覽至 %Program Files%\MSBuild\\。  
  
    2.  建立將儲存目標檔案的新資料夾 "MyContributors"。  
  
    3.  在這個目錄中建立新檔案 "MyContributors.targets"，在檔案中加入下列文字，然後儲存檔案：  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <BuildContributors>$(BuildContributors);ExampleContributors.ModelStatistics</BuildContributors>  
            <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy=name;</ContributorArguments>  
          </PropertyGroup>  
        </Project>  
        ```  
  
    4.  針對要執行參與者的任何專案，在 .sqlproj 檔案內部匯入目標檔案，方法是將下列陳述式加入至 .sqlproj 檔案，在檔案的 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 節點後面：  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
        ```  
  
遵循其中一個方法之後，您可以使用 MSBuild，傳入命令列建置的參數。  
  
> [!NOTE]  
> 您一定要更新 "BuildContributors" 屬性指定您的參與者識別碼。 這是參與者原始程式檔中 "ExportBuildContributor" 屬性所用相同的識別碼。 如果沒有這個識別碼，當您建置專案時不會執行參與者。 只有在您有參與者執行所需的引數時，才必須更新 "ContributorArguments" 屬性。  
  
### <a name="build-the-sql-project"></a>建置 SQL 專案  
  
##### <a name="to-rebuild-your-database-project-by-using-msbuild-and-generate-statistics"></a>若要使用 MSBuild 重建您的資料庫專案和產生統計資料  
  
1.  在 Visual Studio 中，以滑鼠右鍵按一下專案並選取 [重建]。 這會重建專案，而且您應該會看見產生的模型統計資料，其輸出包含在建置輸出中並儲存至 ModelStatistics.xml。 請注意，您可能需要在方案總管中選取 [顯示所有檔案] 才能看得到 xml 檔案。  
  
2.  開啟 Visual Studio 命令提示字元：在 [開始] 功能表上，依序按一下 [所有程式]、[Microsoft Visual Studio <Visual Studio Version>]、[Visual Studio Tools]，然後按一下 [Visual Studio 命令提示字元 (<Visual Studio Version>)]。  
  
3.  在命令提示字元中，巡覽至包含 SQL 專案的資料夾。  
  
4.  在命令提示字元中，輸入下列命令：  
  
    ```  
    MSBuild /t:Rebuild MyDatabaseProject.sqlproj /p:BuildContributors=$(BuildContributors);ExampleContributors.ModelStatistics /p:ContributorArguments=$(ContributorArguments);GenerateModelStatistics=true;SortModelStatisticsBy=name;OutDir=.\;  
    ```  
  
    將 *MyDatabaseProject* 取代為您要建置之資料庫專案的名稱。 如果您在上次建置後變更了專案，可以使用 /t:Build 而不是 /t:Rebuild。  
  
    在輸出中您應該會看到類似下列的組建資訊：  
  
```  
Model Statistics:  
===  
  
Basic model info  
-----------------  
    Version: Sql110  
  Collation: SQL_Latin1_General_CP1_CI_AS  
  
UserDefinedElements  
-----------------  
  DatabaseOptions: 1  
         subtotal: 1  
      total items: 1  
  
OtherElements  
-----------------  
                Assembly: 1  
       BuiltInServerRole: 9  
           ClrTypeMethod: 218  
  ClrTypeMethodParameter: 197  
         ClrTypeProperty: 20  
                Contract: 6  
                DataType: 34  
                Endpoint: 5  
               Filegroup: 1  
             MessageType: 14  
                   Queue: 3  
                    Role: 10  
                  Schema: 13  
                 Service: 3  
                    User: 4  
         UserDefinedType: 3  
                subtotal: 541  
             total items: 16  
  
Relationships  
-----------------  
     Composing: 477  
  Hierarchical: 6  
          Peer: 19  
      subtotal: 502  
  
```  
  
1.  開啟 ModelStatistics.xml 及檢查內容。  
  
    報告的結果也會保存到 XML 檔案。  
  
## <a name="next-steps"></a>Next Steps  
您可以建立其他工具，執行 XML 輸出檔案的處理。 這只是組建參與者的一個例子。 例如，您可以建立組建參與者，以便輸出資料字典檔案做為建置流程的一部分。  
  
## <a name="see-also"></a>另請參閱  
[使用組建和部署參與者自訂資料庫建置和部署](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[逐步解說：擴充資料庫專案部署以分析部署計畫](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
