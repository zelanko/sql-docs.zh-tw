---
title: 逐步解說：延伸資料庫專案部署以修改部署計畫 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 22b077b1-fa25-49ff-94f6-6d0d196d870a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fbd30a8b0e112d74bf9bd0d009592d753688fadd
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099547"
---
# <a name="walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan"></a>逐步解說：擴充資料庫專案部署以修改部署計劃
您可以建立部署參與者，以便在部署 SQL 專案時執行自訂動作。 您可以建立 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 或 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx)。 使用 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)，在計畫執行前變更計畫；使用 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx)，在計畫執行時執行作業。 在這個逐步解說中，您將建立 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx)，名稱為 SqlRestartableScriptContributor，這個部署參與者會將 IF 陳述式加入至部署指令碼中的批次，以在執行期間發生錯誤時，讓指令碼重新執行直到完成為止。  
  
在本逐步解說中，您將會完成下列主要工作：  
  
-   [建立 DeploymentPlanModifier 型別的部署參與者](#CreateDeploymentContributor)  
  
-   [安裝部署參與者](#InstallDeploymentContributor)  
  
-   [執行或測試您的部署參與者](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
您需要下列元件才能完成這個逐步解說：  
  
-   您必須已安裝包含 SQL Server Data Tools 和支援 C# 或 VB 開發的 Visual Studio 版本。  
  
-   您必須擁有包含 SQL 物件的 SQL 專案。  
  
-   可以部署資料庫專案的 SQL Server 執行個體。  
  
> [!NOTE]  
> 這個逐步解說適用於已經熟悉 SQL Server Data Tools SQL 功能的使用者。 您也應該熟悉基本的 Visual Studio 概念，例如如何建立類別庫及如何使用程式碼編輯器將程式碼加入至類別。  
  
## <a name="CreateDeploymentContributor"></a>建立部署參與者  
若要建立部署參與者，您必須執行下列工作：  
  
-   建立類別庫專案並加入必要參考。  
  
-   定義繼承自 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 且名稱為 SqlRestartableScriptContributor 的類別。  
  
-   覆寫 [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) 方法。  
  
-   加入私用 Helper 方法。  
  
-   建置產生的組件。  
  
#### <a name="to-create-a-class-library-project"></a>若要建立類別庫專案  
  
1.  建立名稱為 MyOtherDeploymentContributor 的 Visual C# 或 Visual Basic 類別庫專案。  
  
2.  將 "Class1.cs" 檔案重新命名為 "SqlRestartableScriptContributor.cs"。  
  
3.  在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後按一下 [新增參考]。  
  
4.  選取 [Framework] 索引標籤上的 [System.ComponentModel.Composition]。  
  
5.  按一下 [瀏覽] 並巡覽至 **C:\Program Files (x86)\Microsoft SQL Server\110\SDK\Assemblies** 目錄，選取 [Microsoft.SqlServer.TransactSql.ScriptDom.dll]，然後按一下 [確定]。  
  
6.  加入必要的 SQL 參考：以滑鼠右鍵按一下專案節點，然後按一下 [加入參考]。 按一下 [瀏覽] 並巡覽至 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** 資料夾。 選擇 **Microsoft.SqlServer.Dac.dll**、**Microsoft.SqlServer.Dac.Extensions.dll** 和 **Microsoft.Data.Tools.Schema.Sql.dll** 項目，按一下 [加入]，然後按一下 [確定]。  
  
下一步，開始將程式碼加入至類別。  
  
#### <a name="to-define-the-sqlrestartablescriptcontributor-class"></a>若要定義 SqlRestartableScriptContributor 類別  
  
1.  在程式碼編輯器中，更新 class1.cs 檔案，以符合下列 **using**陳述式：  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.Text;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    ```  
  
2.  更新類別定義以符合下列範例：  
  
    ```csharp  
        /// <summary>  
    /// This deployment contributor modifies a deployment plan by adding if statements  
    /// to the existing batches in order to make a deployment script able to be rerun to completion  
    /// if an error is encountered during execution  
    /// </summary>  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
    public class SqlRestartableScriptContributor : DeploymentPlanModifier  
    {  
    }  
  
    ```  
  
    現在您已經定義繼承自 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 的部署參與者。 在建置和部署程序期間，自訂參與者是從標準擴充目錄載入。 部署計畫修改參與者是由 [ExportDeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanmodifierattribute.aspx) 屬性加以識別。 參與者需要這個屬性，才能設定為可搜尋的。 這個屬性應看起來如下：  
  
    ```csharp  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
  
    ```  
  
3.  加入下列成員宣告：  
  
    ```vb  
         private const string BatchIdColumnName = "BatchId";  
            private const string DescriptionColumnName = "Description";  
  
            private const string CompletedBatchesVariableName = "CompletedBatches";  
            private const string CompletedBatchesVariable = "$(CompletedBatches)";  
            private const string CompletedBatchesSqlCmd = @":setvar " + CompletedBatchesVariableName + " __completedBatches_{0}_{1}";  
            private const string TotalBatchCountSqlCmd = @":setvar TotalBatchCount {0}";  
            private const string CreateCompletedBatchesTable = @"  
    if OBJECT_ID(N'tempdb.dbo." + CompletedBatchesVariable + @"', N'U') is null  
    begin  
    use tempdb  
    create table [dbo].[$(CompletedBatches)]  
    (  
    BatchId int primary key,  
    Description nvarchar(300)  
    )  
    use [$(DatabaseName)]  
    end  
    ";  
  
    ```  
  
    下一步，您會覆寫 OnExecute 方法，加入部署資料庫專案時要執行的程式碼。  
  
#### <a name="to-override-onexecute"></a>若要覆寫 OnExecute  
  
1.  將下列方法加入至 SqlRestartableScriptContributor 類別：  
  
    ```csharp  
    /// <summary>  
    /// You override the OnExecute method to do the real work of the contributor.  
    /// </summary>  
    /// <param name="context"></param>  
    protected override void OnExecute(DeploymentPlanContributorContext context)  
    {  
         // Replace this with the method body  
    }  
  
    ```  
  
    覆寫 [DeploymentPlanContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.aspx) 基底類別的 [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) 方法，這是 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) 和 [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 的基底類別。 將 [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) 物件傳遞給 OnExecute 方法，以存取任何指定的引數、來源和目標資料庫模型、部署計畫和部署選項。 在這個範例中，我們會取得部署計畫和目標資料庫名稱。  
  
2.  現在將主體開頭加入至 OnExecute 方法：  
  
    ```vb  
    // Obtain the first step in the Plan from the provided context  
    DeploymentStep nextStep = context.PlanHandle.Head;  
    int batchId = 0;  
    BeginPreDeploymentScriptStep beforePreDeploy = null;  
  
    // Loop through all steps in the deployment plan  
    while (nextStep != null)  
    {  
        // Increment the step pointer, saving both the current and next steps  
        DeploymentStep currentStep = nextStep;  
        nextStep = currentStep.Next;  
  
        // Add additional step processing here  
    }  
  
    // if we found steps that required processing, set up a temporary table to track the work that you are doing  
    if (beforePreDeploy != null)  
    {  
        // Add additional post-processing here  
    }  
  
    // Cleanup and drop the table   
    DeploymentScriptStep dropStep = new DeploymentScriptStep(DropCompletedBatchesTable);  
    base.AddAfter(context.PlanHandle, context.PlanHandle.Tail, dropStep);  
  
    ```  
  
    在這個程式碼，我們定義一些區域變數，而且設定會處理部署計畫中所有步驟的迴圈。 在迴圈完成後，我們必須進行一些後置處理，然後卸除部署期間建立用來追蹤計畫執行進度的暫存資料表。 此處的重要類型為：[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx) 和 [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx)。 重要的方法是 AddAfter。  
  
3.  現在加入額外的步驟處理，以取代註解 "Add additional step processing here"：  
  
    ```csharp  
    // Look for steps that mark the pre/post deployment scripts  
    // These steps will always be in the deployment plan even if the  
    // user's project does not have a pre/post deployment script  
    if (currentStep is BeginPreDeploymentScriptStep)  
    {  
        // This step marks the beginning of the predeployment script.  
        // Save the step and move on.  
        beforePreDeploy = (BeginPreDeploymentScriptStep)currentStep;  
        continue;  
    }  
    if (currentStep is BeginPostDeploymentScriptStep)  
    {  
        // This is the step that marks the beginning of the post deployment script.    
        // We do not continue processing after this point.  
        break;  
    }  
    if (currentStep is SqlPrintStep)  
    {  
        // We do not need to put if statements around these  
        continue;  
    }  
  
    // if we have not yet found the beginning of the pre-deployment script steps,   
    // skip to the next step.  
    if (beforePreDeploy == null)  
    {  
        // We only surround the "main" statement block with conditional  
        // statements  
        continue;  
    }  
  
    // Determine if this is a step that we need to surround with a conditional statement  
    DeploymentScriptDomStep domStep = currentStep as DeploymentScriptDomStep;  
    if (domStep == null)  
    {  
        // This step is not a step that we know how to modify,  
        // so skip to the next step.  
        continue;  
    }  
  
    TSqlScript script = domStep.Script as TSqlScript;  
    if (script == null)  
    {  
        // The script dom step does not have a script with batches - skip  
        continue;  
    }  
  
        // Loop through all the batches in the script for this step.  All the statements  
        // in the batch will be enclosed in an if statement that will check the  
        // table to ensure that the batch has not already been executed  
        TSqlObject sqlObject;  
        string stepDescription;  
        GetStepInfo(domStep, out stepDescription, out sqlObject);  
        int batchCount = script.Batches.Count;  
  
    for (int batchIndex = 0; batchIndex < batchCount; batchIndex++)  
    {  
        // Add batch processing here  
    }  
  
    ```  
  
    程式碼註解說明處理程序。 在高層次上，此程式碼尋找您重視的步驟，略過其他步驟，並在到達部署後步驟開頭時停止。 如果步驟包含我們必須以條件式圍繞的陳述式，我們會執行額外的處理。 重要類型、方法和屬性包含下列項目：[BeginPreDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpredeploymentscriptstep.aspx)、[BeginPostDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpostdeploymentscriptstep.aspx)、[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)、[TSqlScript](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlscript.aspx)、Script、[DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx) 和 [SqlPrintStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlprintstep.aspx)。  
  
4.  現在，取代註解 "Add batch processing here"，加入批次處理程式碼：  
  
    ```csharp  
        // Create the if statement that will contain the batch's contents  
        IfStatement ifBatchNotExecutedStatement = CreateIfNotExecutedStatement(batchId);  
        BeginEndBlockStatement statementBlock = new BeginEndBlockStatement();  
        ifBatchNotExecutedStatement.ThenStatement = statementBlock;  
        statementBlock.StatementList = new StatementList();  
  
        TSqlBatch batch = script.Batches[batchIndex];  
        int statementCount = batch.Statements.Count;  
  
        // Loop through all statements in the batch, embedding those in an sp_execsql  
        // statement that must be handled this way (schemas, stored procedures,   
        // views, functions, and triggers).  
        for (int statementIndex = 0; statementIndex < statementCount; statementIndex++)  
        {  
            // Add additional statement processing here  
        }  
  
        // Add an insert statement to track that all the statements in this  
        // batch were executed.  Turn on nocount to improve performance by  
        // avoiding row inserted messages from the server  
        string batchDescription = string.Format(CultureInfo.InvariantCulture,  
            "{0} batch {1}", stepDescription, batchIndex);  
  
        PredicateSetStatement noCountOff = new PredicateSetStatement();  
        noCountOff.IsOn = false;  
        noCountOff.Options = SetOptions.NoCount;  
  
        PredicateSetStatement noCountOn = new PredicateSetStatement();  
        noCountOn.IsOn = true;  
        noCountOn.Options = SetOptions.NoCount;   
        InsertStatement batchCompleteInsert = CreateBatchCompleteInsert(batchId, batchDescription);  
        statementBlock.StatementList.Statements.Add(noCountOn);  
    statementBlock.StatementList.Statements.Add(batchCompleteInsert);  
        statementBlock.StatementList.Statements.Add(noCountOff);  
  
        // Remove all the statements from the batch (they are now in the if block) and add the if statement  
        // as the sole statement in the batch  
        batch.Statements.Clear();  
        batch.Statements.Add(ifBatchNotExecutedStatement);  
  
        // Next batch  
        batchId++;  
  
    ```  
  
    這個程式碼會建立 IF 陳述式和 BEGIN/END 區塊。 然後我們對批次中的陳述式執行額外處理。 完成後，我們加入 INSERT 陳述式，將資訊加入至追蹤指令碼執行進度的暫存資料表。 最後，更新批次，將舊有陳述式取代為包含這些陳述式的新 IF 陳述式。金鑰類型、方法和屬性包括：[IfStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.ifstatement.aspx)、[BeginEndBlockStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.beginendblockstatement.aspx)、[StatementList](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.statementlist.aspx)、[TSqlBatch](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlbatch.aspx)、[PredicateSetStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.predicatesetstatement.aspx)、[SetOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.setoptions.aspx)，以及 [InsertStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.insertstatement.aspx)。  
  
5.  現在，加入陳述式處理迴圈的主體。 取代註解 "Add additional statement processing here"：  
  
    ```csharp  
    TSqlStatement smnt = batch.Statements[statementIndex];  
  
    if (IsStatementEscaped(sqlObject))  
    {  
        // "escape" this statement by embedding it in a sp_executesql statement  
        string statementScript;  
        domStep.ScriptGenerator.GenerateScript(smnt, out statementScript);  
        ExecuteStatement spExecuteSql = CreateExecuteSql(statementScript);  
        smnt = spExecuteSql;  
    }  
  
    statementBlock.StatementList.Statements.Add(smnt);  
  
    ```  
  
    對於批次內的每個陳述式，如果陳述式是必須以 sp_executesql 陳述式包裝的類型，請據此修改陳述式。 然後程式碼會將陳述式加入至您建立之 BEGIN/END 區塊的陳述式清單。 重要型別、方法和屬性包含 [TSqlStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlstatement.aspx) 和 [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx)。  
  
6.  最後，加入後置處理區段，以取代註解 "Add additional post-processing here"：  
  
    ```csharp  
    // Declare a SqlCmd variables.  
    //  
    // CompletedBatches variable - defines the name of the table in tempdb that will track  
    // all the completed batches.  The temporary table's name has the target database name and  
    // a guid embedded in it so that:  
    // * Multiple deployment scripts targeting different DBs on the same server  
    // * Failed deployments with old tables do not conflict with more recent deployments  
    //  
    // TotalBatchCount variable - the total number of batches surrounded by if statements.  Using this  
    // variable pre/post deployment scripts can also use the CompletedBatches table to make their  
    // script rerunnable if there is an error during execution  
    StringBuilder sqlcmdVars = new StringBuilder();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, CompletedBatchesSqlCmd,  
        context.Options.TargetDatabaseName, Guid.NewGuid().ToString("D"));  
    sqlcmdVars.AppendLine();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, TotalBatchCountSqlCmd, batchId);  
  
    DeploymentScriptStep completedBatchesSetVarStep = new DeploymentScriptStep(sqlcmdVars.ToString());  
    base.AddBefore(context.PlanHandle, beforePreDeploy, completedBatchesSetVarStep);  
  
    // Create the temporary table we will use to track the work that we are doing  
    DeploymentScriptStep createStatusTableStep = new DeploymentScriptStep(CreateCompletedBatchesTable);  
    base.AddBefore(context.PlanHandle, beforePreDeploy, createStatusTableStep);  
  
    ```  
  
    如果處理程序找到以條件陳述式圍繞的一個或多個步驟，我們必須將陳述式加入至部署指令碼以定義 SQLCMD 變數。 第一個變數 CompletedBatches 包含暫存資料表的唯一名稱，部署指令碼使用這個暫存資料表追蹤指令碼執行時哪些批次已順利完成。 第二個變數 TotalBatchCount 包含部署指令碼中的批次總數。  
  
    其他相關型別、屬性和方法包含：  
  
    StringBuilder、[DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx) 和 AddBefore。  
  
    下一步，您會定義這個方法呼叫的 Helper 方法。  
  
#### <a name="to-add-the-helper-methods"></a>若要加入 Helper 方法  
  
-   必須定義一些 Helper 方法。 重要方法包含：  
  
    |**方法**|**說明**|  
    |--------------|-------------------|  
    |CreateExecuteSQL|定義 CreateExecuteSQL 方法，以便用 EXEC sp_executesql 陳述式圍繞提供的陳述式。 金鑰類型、方法和屬性包含下列項目：[ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx)、[ExecutableProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executableprocedurereference.aspx)、[SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx)、[ProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.procedurereference.aspx) 和 [ExecuteParameter](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executeparameter.aspx)。|  
    |CreateCompletedBatchesName|定義 CreateCompletedBatchesName 方法。 此方法會建立插入批次暫存資料表的名稱。金鑰類型、方法和屬性包括下列項目：[SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx)。|  
    |IsStatementEscaped|定義 IsStatementEscaped 方法。 這個方法會判斷模型項目型別是否要求陳述式先包裝在 EXEC sp_executesql 陳述式中，然後才可以使用 IF 陳述式括住。 金鑰類型、方法和屬性包含下列項目：下列模型類型的 TSqlObject.ObjectType、ModelTypeClass 和 TypeClass 屬性：Schema、Procedure、View、TableValuedFunction、ScalarFunction、DatabaseDdlTrigger、DmlTrigger、ServerDdlTrigger。|  
    |CreateBatchCompleteInsert|定義 CreateBatchCompleteInsert 方法。 這個方法會建立將加入至部署指令碼以追蹤指令碼執行進度的 INSERT 陳述式。 金鑰類型、方法和屬性包含下列項目：InsertStatement、NamedTableReference、ColumnReferenceExpression、ValuesInsertSource 和 RowValue。|  
    |CreateIfNotExecutedStatement|定義 CreateIfNotExecutedStatement 方法。 這個方法會產生 IF 陳述式，檢查暫存批次執行資料表是否指出此批次已經執行。 金鑰類型、方法和屬性包含下列項目：IfStatement、ExistsPredicate、ScalarSubquery、NamedTableReference、WhereClause、ColumnReferenceExpression、IntegerLiteral、BooleanComparisonExpression 和 BooleanNotExpression。|  
    |GetStepInfo|定義 GetStepInfo 方法。 除了步驟名稱之外，這個方法還會擷取用來建立步驟指令碼的模型項目資訊。 其他相關類型和方法包括：[DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx)、[DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx)、[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)、[CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx)、[AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx) 和 [DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx)。|  
    |GetElementName|建立 TSqlObject 的格式化名稱。|  
  
1.  加入下列程式碼以定義 Helper 方法：  
  
    ```csharp  
  
    /// <summary>  
    /// The CreateExecuteSql method "wraps" the provided statement script in an "sp_executesql" statement  
    /// Examples of statements that must be so wrapped include: stored procedures, views, and functions  
    /// </summary>  
    private static ExecuteStatement CreateExecuteSql(string statementScript)  
    {  
        // define a new Exec statement  
        ExecuteStatement executeSp = new ExecuteStatement();  
        ExecutableProcedureReference spExecute = new ExecutableProcedureReference();  
        executeSp.ExecuteSpecification = new ExecuteSpecification { ExecutableEntity = spExecute };  
  
        // define the name of the procedure that you want to execute, in this case sp_executesql  
        SchemaObjectName procName = new SchemaObjectName();  
        procName.Identifiers.Add(CreateIdentifier("sp_executesql", QuoteType.NotQuoted));  
        ProcedureReference procRef = new ProcedureReference { Name = procName };  
  
        spExecute.ProcedureReference = new ProcedureReferenceName { ProcedureReference = procRef };  
  
        // add the script parameter, constructed from the provided statement script  
        ExecuteParameter scriptParam = new ExecuteParameter();  
        spExecute.Parameters.Add(scriptParam);  
        scriptParam.ParameterValue = new StringLiteral { Value = statementScript };  
        scriptParam.Variable = new VariableReference { Name = "@stmt" };  
        return executeSp;  
    }  
  
    /// <summary>  
    /// The CreateIdentifier method returns a Identifier with the specified value and quoting type  
    /// </summary>  
    private static Identifier CreateIdentifier(string value, QuoteType quoteType)  
    {  
        return new Identifier { Value = value, QuoteType = quoteType };  
    }  
  
    /// <summary>  
    /// The CreateCompletedBatchesName method creates the name that will be inserted  
    /// into the temporary table for a batch.  
    /// </summary>  
    private static SchemaObjectName CreateCompletedBatchesName()  
    {  
        SchemaObjectName name = new SchemaObjectName();  
        name.Identifiers.Add(CreateIdentifier("tempdb", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier("dbo", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier(CompletedBatchesVariable, QuoteType.SquareBracket));  
        return name;  
    }  
  
    /// <summary>  
    /// Helper method that determins whether the specified statement needs to  
    /// be escaped  
    /// </summary>  
    /// <param name="sqlObject"></param>  
    /// <returns></returns>  
    private static bool IsStatementEscaped(TSqlObject sqlObject)  
    {  
        HashSet<ModelTypeClass> escapedTypes = new HashSet<ModelTypeClass>  
        {  
            Schema.TypeClass,  
            Procedure.TypeClass,  
            View.TypeClass,  
            TableValuedFunction.TypeClass,  
            ScalarFunction.TypeClass,  
            DatabaseDdlTrigger.TypeClass,  
            DmlTrigger.TypeClass,  
            ServerDdlTrigger.TypeClass  
        };  
        return escapedTypes.Contains(sqlObject.ObjectType);  
    }  
  
    /// <summary>  
    /// Helper method that creates an INSERT statement to track a batch being completed  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <param name="batchDescription"></param>  
    /// <returns></returns>  
    private static InsertStatement CreateBatchCompleteInsert(int batchId, string batchDescription)  
    {  
        InsertStatement insert = new InsertStatement();  
        NamedTableReference batchesCompleted = new NamedTableReference();  
        insert.InsertSpecification = new InsertSpecification();  
        insert.InsertSpecification.Target = batchesCompleted;  
        batchesCompleted.SchemaObject = CreateCompletedBatchesName();  
  
        // Build the columns inserted into  
        ColumnReferenceExpression batchIdColumn = new ColumnReferenceExpression();  
        batchIdColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        batchIdColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(BatchIdColumnName, QuoteType.NotQuoted));  
  
        ColumnReferenceExpression descriptionColumn = new ColumnReferenceExpression();  
        descriptionColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        descriptionColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(DescriptionColumnName, QuoteType.NotQuoted));  
  
        insert.InsertSpecification.Columns.Add(batchIdColumn);  
        insert.InsertSpecification.Columns.Add(descriptionColumn);  
  
        // Build the values inserted  
        ValuesInsertSource valueSource = new ValuesInsertSource();  
        insert.InsertSpecification.InsertSource = valueSource;  
  
        RowValue values = new RowValue();  
        values.ColumnValues.Add(new IntegerLiteral { Value = batchId.ToString() });  
        values.ColumnValues.Add(new StringLiteral { Value = batchDescription });  
        valueSource.RowValues.Add(values);  
  
        return insert;  
    }  
  
    /// <summary>  
    /// This is a helper method that generates an if statement that checks the batches executed  
    /// table to see if the current batch has been executed.  The if statement will look like this  
    ///   
    /// if not exists(select 1 from [tempdb].[dbo].[$(CompletedBatches)]   
    ///                where BatchId = batchId)  
    /// begin  
    /// end  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <returns></returns>  
    private static IfStatement CreateIfNotExecutedStatement(int batchId)  
    {  
        // Create the exists/select statement  
        ExistsPredicate existsExp = new ExistsPredicate();  
        ScalarSubquery subQuery = new ScalarSubquery();  
        existsExp.Subquery = subQuery;  
  
        subQuery.QueryExpression = new QuerySpecification  
        {  
            SelectElements =  
            {  
                new SelectScalarExpression  { Expression = new IntegerLiteral { Value ="1" } }  
            },  
            FromClause = new FromClause  
            {  
                TableReferences =  
                    {  
                        new NamedTableReference() { SchemaObject = CreateCompletedBatchesName() }  
                    }  
            },  
            WhereClause = new WhereClause  
            {  
                SearchCondition = new BooleanComparisonExpression  
                {  
                    ComparisonType = BooleanComparisonType.Equals,  
                    FirstExpression = new ColumnReferenceExpression  
                    {  
                        MultiPartIdentifier = new MultiPartIdentifier  
                        {  
                            Identifiers = { CreateIdentifier(BatchIdColumnName, QuoteType.SquareBracket) }  
                        }  
                    },  
                    SecondExpression = new IntegerLiteral { Value = batchId.ToString() }  
                }  
            }  
        };  
  
        // Put together the rest of the statement  
        IfStatement ifNotExists = new IfStatement  
        {  
            Predicate = new BooleanNotExpression  
            {  
                Expression = existsExp  
            }  
        };  
  
        return ifNotExists;  
    }  
  
    /// <summary>  
    /// Helper method that generates a useful description of the step.  
    /// </summary>  
    private static void GetStepInfo(  
        DeploymentScriptDomStep domStep,  
        out string stepDescription,  
        out TSqlObject element)  
    {  
        element = null;  
  
        // figure out what type of step we've got, and retrieve  
        // either the source or target element.  
        if (domStep is CreateElementStep)  
        {  
            element = ((CreateElementStep)domStep).SourceElement;  
        }  
        else if (domStep is AlterElementStep)  
        {  
            element = ((AlterElementStep)domStep).SourceElement;  
        }  
        else if (domStep is DropElementStep)  
        {  
            element = ((DropElementStep)domStep).TargetElement;  
        }  
  
        // construct the step description by concatenating the type and the fully qualified  
        // name of the associated element.  
        string stepTypeName = domStep.GetType().Name;  
        if (element != null)  
        {  
            string elementName = GetElementName(element);  
  
            stepDescription = string.Format(CultureInfo.InvariantCulture, "{0} {1}",  
                stepTypeName, elementName);  
        }  
        else  
        {  
            // if the step has no associated element, just use the step type as the description  
            stepDescription = stepTypeName;  
        }  
    }  
  
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
  
    ```  
  
2.  將變更儲存至 SqlRestartableScriptContributor.cs。  
  
下一步，您會建置類別庫。  
  
#### <a name="to-sign-and-build-the-assembly"></a>若要簽署和建置組件  
  
1.  按一下 [專案] 功能表上的 [MyOtherDeploymentContributor 屬性]。  
  
2.  按一下 [ **簽署** ] 索引標籤。  
  
3.  按一下 [ **簽署組件**]。  
  
4.  在 [選擇強式名稱金鑰檔案] 中，按一下 **<New>**。  
  
5.  在 [ **建立強式名稱金鑰** ] 對話方塊中的 [ **金鑰檔名稱**]，輸入 **MyRefKey**。  
  
6.  (選擇性) 您可以為強式名稱金鑰檔指定密碼。  
  
7.  按一下 [確定] 。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
9. 按一下 [ **建置** ] 功能表上的 [ **建置方案**]。  
  
    下一步，您必須安裝組件，以便在部署 SQL 專案時將其載入。  
  
## <a name="InstallDeploymentContributor"></a>安裝部署參與者  
若要安裝部署參與者，您必須將組件和關聯的 .pdb 檔案複製到 Extensions 資料夾。  
  
#### <a name="to-install-the-myotherdeploymentcontributor-assembly"></a>若要安裝 MyOtherDeploymentContributor 組件  
  
1.  接下來，將組件資訊複製到 Extensions 目錄。 當 Visual Studio 啟動時，它會識別 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄和子目錄中的任何擴充功能，並讓這些擴充功能可供使用。  
  
2.  將 **MyOtherDeploymentContributor.dll** 組件檔案從輸出目錄複製到 %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions 目錄。 根據預設，編譯過的 .dll 檔案的路徑是 YourSolutionPath\YourProjectPath\bin\Debug 或 YourSolutionPath\YourProjectPath\bin\Release。  
  
## <a name="TestDeploymentContributor"></a>執行或測試您的部署參與者  
若要執行或測試部署參與者，您必須執行下列工作：  
  
-   將屬性加入至要建置的 .sqlproj 檔案。  
  
-   使用 MSBuild 並提供適當的參數，部署資料庫專案。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>將屬性加入至 SQL 專案檔 (.sqlproj)  
您一定要更新 SQL 專案檔，指定要執行之參與者的識別碼。 您可以使用下列其中一種作法：  
  
1.  手動修改 .sqlproj 檔案，加入必要的引數。 如果您的參與者沒有組態所需的任何參與者引數，或者如果您不想要在大量專案中重複使用組建參與者，可以選擇這樣做。 如果您選擇這個選項，將下列陳述式加入至 .sqlproj 檔案，在檔案的第一個 Import 節點後面：  
  
    ```  
    <PropertyGroup>  
      <DeploymentContributors>  
        $(DeploymentContributors); MyOtherDeploymentContributor.RestartableScriptContributor  
      </DeploymentContributors>  
    </PropertyGroup>  
    ```  
  
2.  第二個方法是建立包含必要參與者引數的目標檔案。 如果您針對多個專案使用同一個參與者而且有必要的參與者引數，因為其中包含預設值，這非常有用。 在此情況下，請在 MSBuild 擴充路徑建立目標檔案：  
  
    1.  巡覽至 %Program Files%\MSBuild。  
  
    2.  建立將儲存目標檔案的新資料夾 "MyContributors"。  
  
    3.  在這個目錄中建立新檔案 "MyContributors.targets"，在檔案中新增下列文字，然後儲存檔案：  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <DeploymentContributors>$(DeploymentContributors);MyOtherDeploymentContributor.RestartableScriptContributor</DeploymentContributors>  
          </PropertyGroup>  
        </Project>  
  
        ```  
  
    4.  針對要執行參與者的任何專案，在 .sqlproj 檔案內部匯入目標檔案，方法是將下列陳述式新增至 .sqlproj 檔案，在檔案的 \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> 節點後面：  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
  
        ```  
  
遵循其中一個方法之後，您可以使用 MSBuild，傳入命令列建置的參數。  
  
> [!NOTE]  
> 您一定要更新 "DeploymentContributors" 屬性指定您的參與者識別碼。 這是參與者原始程式檔中 "ExportDeploymentPlanModifier" 屬性所用相同的識別碼。 如果沒有這個識別碼，當您建置專案時不會執行參與者。 只有在您有參與者執行所需的引數時，才需要更新 "ContributorArguments" 屬性。  
  
## <a name="deploy-the-database-project"></a>部署資料庫專案  
  
#### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>若要部署 SQL 專案並產生部署報表  
  
-   您的專案可以在 Visual Studio 中正常發行或部署。 只要開啟包含 SQL 專案的方案，並從專案的滑鼠右鍵操作功能表中選擇 [發行...] 選項，或使用 F5 進行 LocalDB 偵錯部署。 在這個範例中，會使用 [發行...] 對話方塊產生部署指令碼。  
  
    1.  開啟 Visual Studio，並開啟包含 SQL 專案的方案。  
  
    2.  在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [發行...] 選項。  
  
    3.  設定發行目標伺服器名稱和資料庫名稱。  
  
    4.  從對話方塊的底部選項中選擇 [產生指令碼]。 這會建立可用於部署的指令碼。 我們會檢查這個指令碼，確認 IF 陳述式已加入，以便讓指令碼可重新啟動。  
  
    5.  檢查產生的部署指令碼。 在標示 "Pre-Deployment Script Template" 的區段之前，您應該會看到類似下列 Transact-SQL 語法的程式碼：  
  
        ```  
        :setvar CompletedBatches __completedBatches_CompareProjectDB_cd1e348a-8f92-44e0-9a96-d25d65900fca  
        :setvar TotalBatchCount 17  
        GO  
  
        if OBJECT_ID(N'tempdb.dbo.$(CompletedBatches)', N'U') is null  
        begin  
        use tempdb  
        create table [dbo].[$(CompletedBatches)]  
        (  
        BatchId int primary key,  
        Description nvarchar(300)  
        )  
        use [$(DatabaseName)]  
        end  
  
        ```  
  
        在部署指令碼後面，每個批次周圍，您會看到圍繞原始陳述式的 IF 陳述式。 例如，針對 CREATE SCHEMA 陳述式中可能出現下列程式碼：  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 0)  
            BEGIN  
                EXECUTE sp_executesql @stmt = N'CREATE SCHEMA [Sales]  
            AUTHORIZATION [dbo]';  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (0, N'CreateElementStep Sales batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        請注意，CREATE SCHEMA 是必須先包裝在 EXECUTE sp_executesql 陳述式中，再使用 IF 陳述式括住的其中一個陳述式。 CREATE TABLE 等陳述式不需要執行 EXECUTE sp_executesql 陳述式，類似於下列範例：  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 1)  
            BEGIN  
                CREATE TABLE [Sales].[Customer] (  
                    [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
                    [CustomerName] NVARCHAR (40) NOT NULL,  
                    [YTDOrders]    INT           NOT NULL,  
                    [YTDSales]     INT           NOT NULL  
                );  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (1, N'CreateElementStep Sales.Customer batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        > [!NOTE]  
        > 如果部署的資料庫專案與目標資料庫相同，產生的報表不會有多大意義。 若要更有意義的結果，請將變更部署至資料庫或部署新的資料庫。  
  
## <a name="command-line-deployment-using-generated-dacpac-file"></a>使用產生的 dacpac 檔案進行命令列部署  
建置 SQL 專案後，產生的 dacpac 檔案可用來從命令列部署結構描述，因此可以從另一部電腦 (例如組建電腦) 執行部署。 SqlPackage 是啟用 dacpac 部署的命令列公用程式，具有全套的選項可讓使用者部署 dacpac 或產生部署指令碼，以及其他動作。 如需詳細資訊，請參閱 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080(v=VS.103).aspx) \(機器翻譯\)。  
  
> [!NOTE]  
> 若要成功部署已定義 DeploymentContributors 屬性的專案所建立的 dacpac，在使用的電腦必須安裝包含部署參與者的 DLL。 這是因為它們已經標示為部署順利完成的必要項。  
>   
> 若要避免此要求，請從 .sqlproj 檔案排除部署參與者。 或者，使用 SqlPackage 與 **AdditionalDeploymentContributors** 參數來指定要在部署期間執行的參與者。 如果您只想要在特殊情況下使用參與者，例如部署到特定伺服器，這非常有用。  
  
## <a name="next-steps"></a>Next Steps  
在執行計畫之前，您可以嘗試部署計畫的其他修改類型。 您可能會想要執行的其他修改類型包含：  
  
-   將擴充屬性加入至有相關聯的版本號碼的所有資料庫物件。  
  
-   在部署指令碼中加入或移除其他診斷列印陳述式或註解。  
  
## <a name="see-also"></a>另請參閱  
[使用組建和部署參與者自訂資料庫建置和部署](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[逐步解說：延伸資料庫專案組建，以產生模型統計資料](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)  
[逐步解說：延伸資料庫專案部署以分析部署計畫](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
