---
title: 以程式設計方式載入和執行遠端套件 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1cc7358a7058af9feb3f0540085ab140cfd8a7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889620"
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>以程式設計方式載入和執行遠端封裝
  若要從沒有安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的本機電腦執行遠端封裝，請啟動封裝，讓它們在已安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的遠端電腦上執行。 完成這項工作的方法是讓本機電腦使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent、Web 服務或遠端元件來啟動遠端電腦上的封裝。 如果您嘗試直接從本機電腦啟動遠端封裝，該封裝將載入並嘗試從本機電腦執行。 如果本機電腦沒有安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，封裝將不會執行。  
  
> [!NOTE]  
>  您無法在未安裝 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的用戶端電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 外部執行封裝，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 授權的條款可能也不讓您在其他電腦上安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是伺服器元件，不可轉散發至用戶端電腦。  
  
 或者，您可以從已安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的本機電腦執行遠端封裝。 如需詳細資訊，請參閱[以程式設計方式載入和執行本機套件](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)。  
  
##  <a name="top"></a> 在遠端電腦上執行遠端套件  
 如上所述，有多種方法可以在遠端伺服器上執行遠端封裝：  
  
-   [以程式設計方式使用 SQL Server Agent 執行遠端套件](#agent)  
  
-   [以程式設計方式使用 Web 服務或遠端元件執行遠端套件](#service)  
  
 本主題中幾乎所有用以載入和儲存封裝的方法，都需要 `Microsoft.SqlServer.ManagedDTS` 組件的參考。 例外狀況是執行本主題中示範的 ADO.NET 方法**sp_start_job**預存程序，需要一個參考以`System.Data`。 在新專案中加入 `Microsoft.SqlServer.ManagedDTS` 組件的參考之後，請使用 `using` 或 `Imports` 陳述式來匯入 <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間。  
  
###  <a name="agent"></a> 以程式設計方式使用 SQL Server Agent 在伺服器上執行遠端套件  
 下列程式碼範例示範如何以程式設計方式使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，在伺服器上執行遠端封裝。 程式碼範例會呼叫系統預存程序 **sp_start_job**，它將會啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 程序所啟動的作業其名稱為 `RunSSISPackage`，而且此作業是在遠端電腦上。 `RunSSISPackage` 作業接著會在遠端電腦上執行封裝。  
  
> [!NOTE]  
>  **sp_start_job** 預存程序的傳回值指出預存程序是否能夠順利地啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 傳回值不會指出封裝是成功或是失敗。  
  
 如需從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業執行之套件的疑難排解資訊，請參閱 Microsoft 文章：[從 SQL Server Agent 作業步驟呼叫 SSIS 套件時，SSIS 套件未執行](https://support.microsoft.com/kb/918760)。  
  
### <a name="sample-code"></a>範例程式碼  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
 
  
###  <a name="service"></a> 以程式設計方式使用 Web 服務或遠端元件執行遠端套件  
 在伺服器上以程式設計方式執行封裝的上述方案，並不需要伺服器上的任何自訂程式碼。 不過，您可能偏好使用不需依賴 SQL Server Agent 的方案來執行封裝。 下列範例示範可以在伺服器上建立的 Web 服務，以便在本機上啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以及可用以從用戶端電腦呼叫 Web 服務的測試應用程式。 如果您偏好建立遠端元件，而不是 Web 服務，則可以在遠端元件中透過非常少的變更來使用相同的程式碼邏輯。 不過，遠端元件可能需要比 Web 服務設定更大量的組態。  
  
> [!IMPORTANT]  
>  因為其驗證與授權的預設值，Web 服務通常沒有足夠的權限存取 SQL Server 或是檔案系統以載入和執行封裝。 您可能必須在 **web.config** 檔案中設定其驗證與授權設定，並適當地指派資料庫與檔案系統權限，以便將適當的權限指派給 Web 服務。 Web、資料庫以及檔案系統權限的完整討論不在本主題的範圍之內。  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "."、localhost 或是本機伺服器的伺服器名稱。 您無法使用 "(local)"。  
  
### <a name="sample-code"></a>範例程式碼  
 下列程式碼範例示範如何建立和測試 Web 服務。  
  
#### <a name="creating-the-web-service"></a>建立 Web 服務  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以直接從檔案、直接從 SQL Server 或從 SSIS 封裝存放區 (同時管理在 SQL Server 與特殊檔案系統資料夾中的封裝儲存體) 載入。 這個範例使用 `Select Case` 或 `switch` 建構以選取適當的封裝啟動語法並適當地串連輸入引數，來支援所有可用的選項。 LaunchPackage Web 服務方法會以整數而不是 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 值傳回封裝執行的結果，因此用戶端電腦不需要任何 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件的參考。  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>以程式設計方式建立 Web 服務以執行伺服器上的封裝  
  
1.  使用您慣用的程式語言，開啟 Visual Studio 並建立 Web 服務專案。 範例程式碼使用 LaunchSSISPackageService 做為專案的名稱。  
  
2.  將參考加入`Microsoft.SqlServer.ManagedDTS`並新增`Imports`或是`using`陳述式的程式碼檔案來**Microsoft.SqlServer.Dts.Runtime**命名空間。  
  
3.  將 LaunchPackage Web 服務方法的範例程式碼貼到類別中  (範例顯示程式碼視窗的整個內容)。  
  
4.  藉由為 LaunchPackage 方法的輸入引數提供一組指向現有封裝的有效值，建立並測試 Web 服務。 例如，如果 package1.dtsx 是儲存在伺服器上的 C:\My Packages 中，則傳遞 "file" 以做為 sourceType 的值，傳遞 "C:\My Packages" 做為 sourceLocation 的值，並傳遞 "package1" (沒有副檔名) 做為 packageName 的值。  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="http://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "http://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>測試 Web 服務  
 下列範例主控台應用程式使用 Web 服務執行封裝。 Web 服務的 LaunchPackage 方法會以整數而不是 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 值傳回封裝執行的結果，因此用戶端電腦不需要任何 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件的參考。 範例會建立一個私用列舉，其值會鏡像 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 值，以報告執行的結果。  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>建立主控台應用程式以測試 Web 服務  
  
1.  在 Visual Studio 中，使用您慣用的程式語言，將新主控台應用程式加入包含 Web 服務專案的相同方案。 範例程式碼使用 LaunchSSISPackageTest 做為專案的名稱。  
  
2.  將新主控台應用程式設定為方案中的啟動專案。  
  
3.  加入 Web 服務專案的 Web 參考。 若有需要，請在範例程式碼中，為指派到 Web 服務 Proxy 物件的名稱，調整變數宣告。  
  
4.  將 Main 常式與私用列舉的範例程式碼貼到程式碼中  (範例顯示程式碼視窗的整個內容)。  
  
5.  編輯呼叫 LaunchPackage 方法的程式碼行，為其輸入引數提供一組指向現有封裝的有效值。 例如，如果 package1.dtsx 是儲存在伺服器上的 C:\My Packages 中，則傳遞 "file" 以做為 `sourceType` 的值，傳遞 "C:\My Packages" 做為 `sourceLocation` 的值，並傳遞 "package1" (沒有副檔名) 做為 `packageName` 的值。  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  

  
## <a name="external-resources"></a>外部資源  
  
-   影片，[如何：使用 SQL Server Agent 讓 SSIS 套件執行自動化 (SQL Server)](https://technet.microsoft.com/sqlserver/ff686764.aspx) (位於 technet.microsoft.com)  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [了解本機與遠端執行之間的差異](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [以程式設計方式載入和執行本機封裝](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [載入本機套件的輸出](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
