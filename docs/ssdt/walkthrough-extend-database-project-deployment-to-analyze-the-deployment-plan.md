---
title: 逐步解說：延伸資料庫專案部署以分析部署計畫 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ead8470-93ba-44e3-8848-b59322e37621
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 13e2b010a193e8c610c54a5b619d8a67c9b4d2d3
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097461"
---
# <a name="walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan"></a>逐步解說：擴充資料庫專案部署以分析部署計劃
您可以建立部署參與者，以便在部署 SQL 專案時執行自訂動作。 您可以建立 DeploymentPlanModifier 或 DeploymentPlanExecutor。 使用 DeploymentPlanModifier，在計畫執行前變更計畫；使用 DeploymentPlanExecutor，在計畫執行時執行作業。 在這個逐步解說中，您會建立名稱為 DeploymentUpdateReportContributor 的 DeploymentPlanExecutor，以產生有關部署資料庫專案時執行之動作的報表。 因為這個組建參與者接受參數來控制是否產生報表，您必須執行其他必要步驟。  
  
在本逐步解說中，您將會完成下列主要工作：  
  
-   [建立 DeploymentPlanExecutor 型別的部署參與者](#CreateDeploymentContributor)  
  
-   [安裝部署參與者](#InstallDeploymentContributor)  
  
-   [測試您的部署參與者](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
您需要下列元件才能完成這個逐步解說：  
  
-   您必須已安裝包含 SQL Server Data Tools (SSDT) 和支援 C# 或 VB 開發的 Visual Studio 版本。  
  
-   您必須擁有包含 SQL 物件的 SQL 專案。  
  
-   可以部署資料庫專案的 SQL Server 執行個體。  
  
> [!NOTE]  
> 這個逐步解說適用於已經熟悉 SSDT SQL 功能的使用者。 您也應該熟悉基本的 Visual Studio 概念，例如如何建立類別庫及如何使用程式碼編輯器將程式碼加入至類別。  
  
## <a name="CreateDeploymentContributor"></a>建立部署參與者  
若要建立部署參與者，您必須執行下列工作：  
  
-   建立類別庫專案並加入必要參考。  
  
-   定義繼承自 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 且名稱為 DeploymentUpdateReportContributor 的類別。  
  
-   覆寫 OnExecute 方法。  
  
-   加入私用協助程式類別。  
  
-   建置產生的組件。  
  
#### <a name="to-create-a-class-library-project"></a>若要建立類別庫專案  
  
1.  建立名稱為 MyDeploymentContributor 的 Visual Basic 或 Visual C# 類別庫專案。  
  
2.  將 "Class1.cs" 檔案重新命名為 "DeploymentUpdateReportContributor.cs"。  
  
3.  在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後按一下 [新增參考]。  
  
4.  選取 [Framework] 索引標籤上的 [System.ComponentModel.Composition]。  
  
5.  加入必要的 SQL 參考：以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]。 按一下 [瀏覽] 並巡覽至 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 資料夾。 選擇 **Microsoft.SqlServer.Dac.dll**、**Microsoft.SqlServer.Dac.Extensions.dll** 和 **Microsoft.Data.Tools.Schema.Sql.dll** 項目，按一下 [加入]，然後按一下 [確定]。  
  
    下一步，開始將程式碼加入至類別。  
  
#### <a name="to-define-the-deploymentupdatereportcontributor-class"></a>若要定義 DeploymentUpdateReportContributor 類別  
  
1.  在程式碼編輯器中，更新 DeploymentUpdateReportContributor.cs 檔案，以符合下列 **using** 陳述式：  
  
    ```csharp  
    using System;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Extensibility;  
    using Microsoft.SqlServer.Dac.Model;  
  
    ```  
  
2.  更新類別定義以符合下列範例：  
  
    ```csharp  
    /// <summary>  
        /// An executor that generates a report detailing the steps in the deployment plan. Will only run  
        /// if a "GenerateUpdateReport=true" contributor argument is set in the project file, in a targets file or  
        /// passed as an additional argument to the DacServices API. To set in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;  
        ///     </ContributorArguments>  
        /// <PropertyGroup>  
        ///   
        /// </summary>  
        [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
        public class DeploymentUpdateReportContributor : DeploymentPlanExecutor  
        {  
        }  
  
    ```  
  
    現在您已經定義繼承自 DeploymentPlanExecutor 的部署參與者。 在建置和部署程序期間，自訂參與者是從標準擴充目錄載入。 部署計畫執行參與者是由 [ExportDeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanexecutorattribute.aspx) 屬性加以識別。  
  
    參與者需要這個屬性，才能設定為可搜尋的。 看起來應類似下列範例：  
  
    ```csharp  
    [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
  
    ```  
  
    在此案例中，屬性的第一個參數應該是唯一識別碼，用來識別專案檔中的參與者。 最佳做法是將您程式庫的命名空間 (在此逐步解說中是 MyDeploymentContributor) 與類別名稱 (在此逐步解說中是 DeploymentUpdateReportContributor) 結合，來產生識別碼。  
  
3.  下一步，您將會加入下列成員，用來讓這個提供者接受命令列參數：  
  
    ```csharp  
    public const string GenerateUpdateReport = "DeploymentUpdateReportContributor.GenerateUpdateReport";  
    ```  
  
    這個成員可讓使用者使用 GenerateUpdateReport 選項，指定是否應該產生報表。  
  
    下一步，您會覆寫 OnExecute 方法，加入部署資料庫專案時要執行的程式碼。  
  
#### <a name="to-override-onexecute"></a>若要覆寫 OnExecute  
  
-   將下列方法加入至 DeploymentUpdateReportContributor 類別：  
  
    ```csharp  
    /// <summary>  
            /// Override the OnExecute method to perform actions when you execute the deployment plan for  
            /// a database project.  
            /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                ExtensibilityError reportMsg = new ExtensibilityError(msg, Severity.Message);  
                base.PublishMessage(reportMsg);  
            }  
        /// <summary>  
        /// Override the OnExecute method to perform actions when you execute the deployment plan for  
        /// a database project.  
        /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                DataSchemaError reportMsg = new DataSchemaError(msg, ErrorSeverity.Message);  
                base.PublishMessage(reportMsg);  
            }  
    ```  
  
    將 [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) 物件傳遞給 OnExecute 方法，以存取任何指定的引數、來源和目標資料庫模型、組建屬性和擴充檔。 在這個範例中，我們會取得模型，然後呼叫 Helper 函數以輸出模型資訊。 我們使用基底類別的 PublishMessage Helper 方法，回報所發生的任何錯誤。  
  
    其他相關類型和方法包括：[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)、[ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx)、[DeploymentPlanHandle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanhandle.aspx) 和 [SqlDeploymentOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqldeploymentoptions.aspx)。  
  
    下一步，您會定義挖掘部署計畫詳細資料的協助程式類別。  
  
#### <a name="to-add-the-helper-class-that-generates-the-report-body"></a>若要加入協助程式類別以產生報表主體  
  
-   加入下列程式碼，以加入協助程式類別及其方法：  
  
    ```csharp  
    /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                readonly TSqlModel _sourceModel;  
                readonly ModelComparisonResult _diff;  
                readonly DeploymentStep _planHead;  
  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
                    if (context == null)  
                    {  
                        throw new ArgumentNullException("context");  
                    }  
  
                    // save the source model, source/target differences,  
                    // and the beginning of the deployment plan.  
                    _sourceModel = context.Source;  
                    _diff = context.ComparisonResult;  
                    _planHead = context.PlanHandle.Head;  
                }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {// Assumes that we have a valid report file  
                    if (reportFile == null)  
                    {  
                        throw new ArgumentNullException("reportFile");  
                    }  
  
                    // set up the XML writer  
                    XmlWriterSettings xmlws = new XmlWriterSettings();  
                    // Indentation makes it a bit more readable  
                    xmlws.Indent = true;  
                    FileStream fs = new FileStream(reportFile.FullName, FileMode.Create, FileAccess.Write, FileShare.ReadWrite);  
                    XmlWriter xmlw = XmlWriter.Create(fs, xmlws);  
  
                    try  
                    {  
                        xmlw.WriteStartDocument(true);  
                        xmlw.WriteStartElement("DeploymentReport");  
  
                        // Summary report of the operations that  
                        // are contained in the plan.  
                        ReportPlanOperations(xmlw);  
  
                        // You could add a method call here  
                        // to produce a detailed listing of the   
                        // differences between the source and  
                        // target model.  
                        xmlw.WriteEndElement();  
                        xmlw.WriteEndDocument();  
                        xmlw.Flush();  
                        fs.Flush();  
                    }  
                    finally  
                    {  
                        xmlw.Close();  
                        fs.Dispose();  
                    }  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {// write the node to indicate the start  
                    // of the list of operations.  
                    xmlw.WriteStartElement("Operations");  
  
                    // Loop through the steps in the plan,  
                    // starting at the beginning.  
                    DeploymentStep currentStep = _planHead;  
                    while (currentStep != null)  
                    {  
                        // Report the type of step  
                        xmlw.WriteStartElement(currentStep.GetType().Name);  
  
                        // based on the type of step, report  
                        // the relevant information.  
                        // Note that this procedure only handles   
                        // a subset of all step types.  
                        if (currentStep is SqlRenameStep)  
                        {  
                            SqlRenameStep renameStep = (SqlRenameStep)currentStep;  
                            xmlw.WriteAttributeString("OriginalName", renameStep.OldName);  
                            xmlw.WriteAttributeString("NewName", renameStep.NewName);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(renameStep.RenamedElement));  
                        }  
                        else if (currentStep is SqlMoveSchemaStep)  
                        {  
                            SqlMoveSchemaStep moveStep = (SqlMoveSchemaStep)currentStep;  
                            xmlw.WriteAttributeString("OrignalName", moveStep.PreviousName);  
                            xmlw.WriteAttributeString("NewSchema", moveStep.NewSchema);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(moveStep.MovedElement));  
                        }  
                        else if (currentStep is SqlTableMigrationStep)  
                        {  
                            SqlTableMigrationStep dmStep = (SqlTableMigrationStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dmStep.SourceTable));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dmStep.SourceElement));  
                        }  
                        else if (currentStep is CreateElementStep)  
                        {  
                            CreateElementStep createStep = (CreateElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(createStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(createStep.SourceElement));  
                        }  
                        else if (currentStep is AlterElementStep)  
                        {  
                            AlterElementStep alterStep = (AlterElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(alterStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(alterStep.SourceElement));  
                        }  
                        else if (currentStep is DropElementStep)  
                        {  
                            DropElementStep dropStep = (DropElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dropStep.TargetElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dropStep.TargetElement));  
                        }  
  
                        // If the script bodies are to be included,  
                        // add them to the report.  
                        if (this.IncludeScripts)  
                        {  
                            using (StringWriter sw = new StringWriter())  
                            {  
                                currentStep.GenerateBatchScript(sw);  
                                string tsqlBody = sw.ToString();  
                                if (string.IsNullOrEmpty(tsqlBody) == false)  
                                {  
                                    xmlw.WriteCData(tsqlBody);  
                                }  
                            }  
                        }  
  
                        // close off the current step  
                        xmlw.WriteEndElement();  
                        currentStep = currentStep.Next;  
                    }  
                    xmlw.WriteEndElement();  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(TSqlObject element)  
                {  
                    return element.ObjectType.Name;  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private static string GetElementName(TSqlObject element)  
                {  
                    StringBuilder name = new StringBuilder();  
                    if (element.Name.HasExternalParts)  
                    {  
                        foreach (string part in element.Name.ExternalParts)  
                        {  
                            if (name.Length > 0)  
                            {  
                                name.Append('.');  
                            }  
                            name.AppendFormat("[{0}]", part);  
                        }  
                    }  
  
                    foreach (string part in element.Name.Parts)  
                    {  
                        if (name.Length > 0)  
                        {  
                            name.Append('.');  
                        }  
                        name.AppendFormat("[{0}]", part);  
                    }  
  
                    return name.ToString();  
                }  
            }        /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
               }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(IModelElement element)  
                {  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementName(IModelElement element)  
                {  
                }  
            }  
    ```  
  
-   將變更儲存至類別檔案。 在協助程式類別中參考一些有用的型別：  
  
    |**程式碼區域**|**有用的型別**|  
    |-----------------|--------------------|  
    |類別成員|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)、[ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx)、[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)|  
    |WriteReport 方法|XmlWriter 和 XmlWriterSettings|  
    |ReportPlanOperations 方法|相關類型包括下列項目：[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)、[SqlRenameStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlrenamestep.aspx)、[SqlMoveSchemaStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlmoveschemastep.aspx)、[SqlTableMigrationStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqltablemigrationstep.aspx)、[CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx)、[AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx)、[DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx)。<br /><br />還有一些其他步驟 (如需步驟的完整清單，請參閱 API 文件)。|  
    |GetElementCategory|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
    |GetElementName|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
  
    下一步，您會建置類別庫。  
  
#### <a name="to-sign-and-build-the-assembly"></a>若要簽署和建置組件  
  
1.  按一下 [專案] 功能表上的 [MyDeploymentContributor 屬性]。  
  
2.  按一下 [ **簽署** ] 索引標籤。  
  
3.  按一下 [ **簽署組件**]。  
  
4.  在 [選擇強式名稱金鑰檔案] 中，按一下 **<New>**。  
  
5.  在 [ **建立強式名稱金鑰** ] 對話方塊中的 [ **金鑰檔名稱**]，輸入 **MyRefKey**。  
  
6.  (選擇性) 您可以為強式名稱金鑰檔指定密碼。  
  
7.  按一下 [確定] 。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
9. 按一下 [ **建置** ] 功能表上的 [ **建置方案**]。  
  
下一步，您必須安裝組件，以便在建置及部署 SQL 專案時將其載入。  
  
## <a name="InstallDeploymentContributor"></a>安裝部署參與者  
若要安裝部署參與者，您必須將組件和關聯的 .pdb 檔案複製到 Extensions 資料夾。  
  
#### <a name="to-install-the-mydeploymentcontributor-assembly"></a>若要安裝 MyDeploymentContributor 組件  
  
-   接下來，將組件資訊複製到 Extensions 目錄。 當 Visual Studio 啟動時，它會識別 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄和子目錄中的任何擴充功能，並讓這些擴充功能可供使用：  
  
-   將 **MyDeploymentContributor.dll** 組件檔案從輸出目錄複製到 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄。 根據預設，編譯過的 .dll 檔案的路徑是 YourSolutionPath\YourProjectPath\bin\Debug 或 YourSolutionPath\YourProjectPath\bin\Release。  
  
## <a name="TestDeploymentContributor"></a>測試您的部署參與者  
若要測試部署參與者，您必須執行下列工作：  
  
-   將屬性加入至要部署的 .sqlproj 檔案。  
  
-   使用 MSBuild 並提供適當的參數，部署專案。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>將屬性加入至 SQL 專案檔 (.sqlproj)  
您一定要更新 SQL 專案檔，指定要執行之參與者的識別碼。 此外，因為這個參與者必須有 "GenerateUpdateReport" 引數，必須將它指定為參與者引數。  
  
您可以使用下列其中一種作法： 手動修改 .sqlproj 檔案，加入必要的引數。 如果您的參與者沒有組態所需的任何參與者引數，或者如果您不想要在大量專案中重複使用參與者，可以選擇這樣做。 如果您選擇這個選項，將下列陳述式加入至 .sqlproj 檔案，在檔案的第一個 Import 節點後面：  
  
```  
<PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors); MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
<ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
  </PropertyGroup>  
```  
  
第二個方法是建立包含必要參與者引數的目標檔案。 如果您針對多個專案使用同一個參與者而且有必要的參與者引數，因為其中包含預設值，這非常有用。 在此情況下，請在 MSBuild 擴充路徑建立目標檔案。  
  
1.  巡覽至 %Program Files%\MSBuild。  
  
2.  建立將儲存目標檔案的新資料夾 "MyContributors"。  
  
3.  在這個目錄中建立新檔案 "MyContributors.targets"，在檔案中新增下列文字，然後儲存檔案：  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
  
    <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors);MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
    <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments); DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
      </PropertyGroup>  
    </Project>  
    ```  
  
4.  針對要執行參與者的任何專案，在 .sqlproj 檔案內部匯入目標檔案，方法是將下列陳述式新增至 .sqlproj 檔案，在檔案的 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 節點後面：  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
    ```  
  
遵循其中一個方法之後，您可以使用 MSBuild，傳入命令列建置的參數。  
  
> [!NOTE]  
> 您一定要更新 "DeploymentContributors" 屬性指定您的參與者識別碼。 這是參與者原始程式檔中 "ExportDeploymentPlanExecutor" 屬性所用相同的識別碼。 如果沒有這個識別碼，當您建置專案時不會執行參與者。 只有在您有參與者執行所需的引數時，才需要更新 "ContributorArguments" 屬性。  
  
### <a name="deploy-the-database-project"></a>部署資料庫專案  
您的專案可以在 Visual Studio 中正常發行或部署。 只要開啟包含 SQL 專案的方案，並從專案的滑鼠右鍵操作功能表中選擇 [發行...] 選項，或使用 F5 進行 LocalDB 偵錯部署。 在這個範例中，會使用 [發行...] 對話方塊產生部署指令碼。  
  
##### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>若要部署 SQL 專案並產生部署報表  
  
1.  開啟 Visual Studio，並開啟包含 SQL 專案的方案。  
  
2.  選取專案並按 "F5" 進行偵錯部署。 注意：因為 ContributorArguments 元素設定為只在設定是 "Debug" 時才會包含在內，所以現在只產生偵錯部署的部署報表。 若要變更此情況，請將 Condition="'$(Configuration)' == 'Debug'" 陳述式從 ContributorArguments 定義移除。  
  
3.  類似下列範例的輸出應該會出現在輸出視窗中：  
  
    ```  
    ------ Deploy started: Project: Database1, Configuration: Debug Any CPU ------  
    Finished verifying cached model in 00:00:00  
    Deployment reports ->  
  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.summary.xml  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.details.xml  
  
      Deployment script generated to:  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyDatabaseProject.sql  
  
    ```  
  
4.  開啟 MyTargetDatabase.summary.xml 及檢查內容。 檔案類似顯示新資料庫部署的下列範例：  
  
    ```  
    <?xml version="1.0" encoding="utf-8" standalone="yes"?>  
    <DeploymentReport>  
      <Operations>  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <BeginPreDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPreDeploymentScriptStep />  
        <SqlBeginPreservationStep />  
        <SqlEndPreservationStep />  
        <SqlBeginDropsStep />  
        <SqlEndDropsStep />  
        <SqlBeginAltersStep />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales" Category="Schema" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Customer" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Customer_CustID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Orders" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Orders_OrderID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDOrders" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDSales" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_OrderDate" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_Status" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.FK_Orders_Customer_CustID" Category="Foreign Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_FilledDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_OrderDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspCancelOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspFillOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspNewCustomer" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspPlaceNewOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspShowOrderDetails" Category="Procedure" />  
        <SqlEndAltersStep />  
        <DeploymentScriptStep />  
        <BeginPostDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPostDeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
      </Operations>  
    </DeploymentReport>  
  
    ```  
  
    > [!NOTE]  
    > 如果部署的資料庫專案與目標資料庫相同，產生的報表不會有多大意義。 若要更有意義的結果，請將變更部署至資料庫或部署新的資料庫。  
  
5.  開啟 MyTargetDatabase.details.xml 及檢查內容。 詳細資料檔案的一小部分會顯示建立 Sales 結構描述、列印有關建立資料表的訊息，以及建立資料表的項目和指令碼：  
  
    ```  
    <CreateElementStep Name="Sales" Category="Schema"><![CDATA[CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
  
    ]]></CreateElementStep>  
        <SqlPrintStep><![CDATA[PRINT N'Creating [Sales].[Customer]...';  
  
    ]]></SqlPrintStep>  
        <CreateElementStep Name="Sales.Customer" Category="Table"><![CDATA[CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
  
    ]]></CreateElementStep>  
  
    ```  
  
    藉由在執行時分析部署計畫，可以回報在部署中包含的任何資訊，也可以根據該計畫的步驟採取其他動作。  
  
## <a name="next-steps"></a>Next Steps  
您可以建立其他工具，執行 XML 輸出檔案的處理。 這只是 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 的一個例子。 您也可以建立 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 以在計畫執行前變更部署計畫。  
  
## <a name="see-also"></a>另請參閱  
[逐步解說：延伸資料庫專案組建，以產生模型統計資料](https://msdn.microsoft.com/library/ee461508(v=vs.100).aspx)  
[逐步解說：延伸資料庫專案部署以修改部署計畫](https://msdn.microsoft.com/library/ee461507(v=vs.100).aspx)  
[使用組建和部署參與者自訂資料庫建置和部署](https://msdn.microsoft.com/library/ee461505(v=vs.100).aspx)  
  
