---
title: "將封裝部署至 Integration Services 伺服器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 將封裝部署至 Integration Services 伺服器
  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 引進累加封裝部署功能，可讓您將一或多個封裝部署到現有或新的專案中，而不需部署整個專案。  
  
##  <a name="DeployWizard"></a> 使用 Integration Services 部署精靈部署封裝  
  
1.  在命令提示字元中，從 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 執行 **isdeploymentwizard.exe**。 64 位元的電腦上的 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn** 也有提供 32 位元版本的工具。  
  
2.  在 [選取來源] 頁面上，切換至 [封裝部署模型]。 然後，選取含有來源封裝的資料夾並設定封裝。  
  
3.  完成精靈。 遵循 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) (封裝部署模型) 中所述的其餘步驟。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio 部署封裝  
  
1.  在 SQL Server Management Studio 中，依序展開物件總管中的 [Integration Services 目錄] > [SISDB] 節點。  
  
2.  以滑鼠右鍵按一下 [專案] 資料夾，然後按一下 [部署專案]。  
  
3.  如果您看到 [簡介] 頁面，按一下 [下一步] 以繼續。  
  
4.  在 [選取來源] 頁面上，切換至 [封裝部署模型]。 然後，選取含有來源封裝的資料夾並設定封裝。  
  
5.  完成精靈。 遵循 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) (封裝部署模型) 中所述的其餘步驟。  
  
##  <a name="SSDT"></a> 使用 SQL Server Data Tools 部署封裝 (Visual Studio)  
  
1.  在 Visual Studio 中，開啟 Integration Services 專案，並選取您想要部署的封裝。  
  
2.  按一下滑鼠右鍵並選取 [部署封裝]。 隨即開啟 [部署精靈]，其中包含設定為來源封裝的所選封裝。  
  
3.  完成精靈。 遵循 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) (封裝部署模型) 中所述的其餘步驟。  
  
##  <a name="StoredProcedure"></a> 使用 deploy_packages 預存程序部署封裝  
 您可以使用 **[catalog].[deploy_packages]** 預存程序，將一或多個 SSIS 封裝部署至 SSIS 目錄。 下列程式碼範例示範如何使用此預存程序，將封裝部署至 SSIS 伺服器。 如需詳細資訊，請參閱 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)。  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> 使用管理物件模型 API 部署封裝  
 下列程式碼範例示範如何使用管理物件模型 API，將封裝部署到伺服器。  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  