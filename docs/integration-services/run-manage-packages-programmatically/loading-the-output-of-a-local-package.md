---
title: 載入本機套件的輸出 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 385fd9fe4224c754af7546ffe2737316aaaf62fe
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65719285"
---
# <a name="loading-the-output-of-a-local-package"></a>載入本機封裝的輸出

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 將輸出儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地時，或使用 **System.IO** 命名空間，將輸出儲存到一般檔案目的地時，用戶端應用程式可以讀取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件的輸出。 但用戶端應用程式也可直接從記憶體讀取封裝的輸出，而無須在程序中間執行保存資料的步驟。 此解決方案的關鍵在於 **Microsoft.SqlServer.Dts.DtsClient** 命名空間，其中包含 **System.Data** 命名空間中的 **IDbConnection**、**IDbCommand** 和 **IDbDataParameter** 介面的特殊實作。 預設會在 **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn** 中安裝 Microsoft.SqlServer.Dts.DtsClient.dll 組件。  

> [!IMPORTANT]
> 本文中所述的程序 (使用 `DtsClient` 程式庫) 僅適用於以套件部署模型 (即 `/SQL`、`/DTS` 或 `/File` 選項) 部署的套件。 此程序不適用於以伺服器部署模型 (即 `/ISServer` 選項) 部署的套件。 若要取用以伺服器部署模型 (即 `/ISServer` 選項) 部署的本機套件輸出，請使用[資料流目的地](../data-flow/data-streaming-destination.md)取代本文中所述的程序。

> [!NOTE]  
> 本主題所述之程序需要將資料流程工作與任何父物件的 DelayValidation 屬性，設定成其預設值 **False**。
  
## <a name="description"></a>Description  
 這個程序示範如何以 Managed 程式碼開發用戶端應用程式，這個程式碼使用 DataReader 目的地直接從記憶體載入封裝的輸出。 這裡所摘要的步驟將在接下來的程式碼範例中示範。  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>將資料封裝輸出載入用戶端應用程式  
  
1.  在封裝中，設定 DataReader 目的地以接收您要讀到用戶端應用程式中的輸出。 給 DataReader 目的地一個描述性名稱，因為您稍後將在用戶端應用程式中使用這個名稱。 記下 DataReader 目的地的名稱。  
  
2.  在開發專案中，找到組件 **Microsoft.SqlServer.Dts.DtsClient.dll**，來設定 **Microsoft.SqlServer.Dts.DtsClient** 命名空間的參考。 此組件預設安裝在 **C:\Program Files\Microsoft SQL Server\100\DTS\Binn** 中。 使用 C# **Using** 或 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **Imports** 陳述式，將命名空間匯入至程式碼。  
  
3.  在您的程式碼中，使用含有 **dtexec.exe** 執行套件所需命令列參數的連接字串，建立類型為 **DtsClient.DtsConnection** 的物件。 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。 然後使用此連接字串開啟連接。 您也可以使用 **dtexecui** 公用程式，以視覺化方式建立所需的連接字串。  
  
    > [!NOTE]  
    >  範例程式碼透過使用 `/FILE <path and filename>` 語法示範從檔案系統載入封裝。 不過，您也可以使用 `/SQL <package name>` 語法從 MSDB 資料庫載入封裝，或是使用 `/DTS \<folder name>\<package name>` 語法從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝存放區載入。  
  
4.  建立類型為 **DtsClient.DtsCommand** 的物件，以使用先前建立的 **DtsConnection** 並將其 **CommandText** 屬性設定為套件中的 DataReader 目的地名稱。 然後呼叫命令物件的 **ExecuteReader** 方法，將套件結果載入新的 DataReader。  
  
5.  您可以選擇性地使用 **DtsCommand** 物件上的 **DtsDataParameter** 物件集合，間接地參數化套件輸出，以便將值傳遞給定義在套件中的變數。 您可以在封裝中使用這些變數做為查詢參數，或在運算式中加以運用，藉此影響傳回 DataReader 目的地的結果。 您必須先在 **DtsClient** 命名空間的套件中定義這些變數，才可將其用於用戶端應用程式的 **DtsDataParameter** 物件  (您可能需要按一下 [變數] 視窗中的 [選擇變數資料行] 工具列按鈕，才會顯示 [命名空間] 資料行)。在您的用戶端程式碼中，將 **DtsDataParameter** 新增至 **DtsCommand** 的 **Parameters** 集合時，請省略變數名稱中的 DtsClient 命名空間參考。 例如：  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  視需要以重複方式呼叫 DataReader 的 **Read** 方法，在輸出資料的資料列中執行迴圈。 在用戶端應用程式中使用資料或是儲存資料以供稍後使用。  
  
    > [!IMPORTANT]  
    >  在讀取最後一列的資料之後，實作 DataReader 的 **Read** 方法會再傳回 **true** 一次。 這使得在 **Read** 傳回 **true** 時，難以使用在 DataReader 中執行迴圈的一般程式碼。 如果您的程式碼在讀取預期數目的資料列之後，嘗試關閉 DataReader 或連線，而沒有額外或最後呼叫 **Read** 方法，則程式碼將引發未處理的例外狀況。 不過，如果您的程式碼嘗試在迴圈的這個最後反覆運算中讀取資料，當 **Read** 仍然傳回 **true**，但是已經傳遞最後一個資料列時，則程式碼將會引發未處理的 **ApplicationException**，並產生「SSIS IDataReader 超過結果集的結尾」的訊息。 這個行為與其他 DataReader 實作的行為不同。 因此，當使用迴圈讀取 DataReader 中的資料列，而 **Read** 傳回 **true** 時，您需要針對最後一次成功地呼叫 **Read** 方法，來撰寫程式碼以擷取、測試和捨棄這個預期的 **ApplicationException**。 或者，如果您事先知道預期的資料列數目，就可以處理資料列，然後在關閉 DataReader 與連線之前，再呼叫一次 **Read** 方法。  
  
7.  呼叫 **DtsCommand** 物件的 **Dispose** 方法。 如果您已經使用任何 **DtsDataParameter** 物件，這將特別重要。  
  
8.  關閉 DataReader 和連接物件。  
  
## <a name="example"></a>範例  
 下列範例執行的封裝，會計算單一彙總值並將值儲存到 DataReader 目的地，然後從 DataReader 讀取這個值，並在 Windows Form 的文字方塊中顯示值。  
  
 將封裝的輸出載入用戶端應用程式時，不需要使用參數。 如果您不想要使用參數，可以在 **DtsClient** 命名空間中省略變數的使用，並省略使用 **DtsDataParameter** 物件的程式碼。  
  
#### <a name="to-create-the-test-package"></a>建立測試封裝  
  
1.  建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 範例程式碼使用 "DtsClientWParamPkg.dtsx" 做為封裝的名稱。  
  
2.  在 DtsClient 命名空間中加入 String 類型的變數。 範例程式碼使用 Country 做為變數的名稱  (您可能需要按一下 [變數] 視窗中的 [選擇變數資料行] 工具列按鈕，才會顯示 [命名空間] 資料行)。  
  
3.  加入連接至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫的 OLE DB 連接管理員。  
  
4.  將資料流程工作加入封裝，並切換至資料流程設計介面。  
  
5.  將 OLE DB 來源加入資料流程並將它設定成使用先前建立的 OLE DB 連接管理員，並加入下列 SQL 命令：  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  按一下 [參數]，然後在 [設定查詢參數] 對話方塊中，將查詢中的單一輸入參數 Parameter0 對應至 DtsClient::Country 變數。  
  
7.  將彙總轉換加入資料流程，然後將 OLE DB 來源的輸出連接到轉換。 開啟「彙總轉換編輯器」並將它設定成在所有的輸入資料行 (*) 上執行 "Count all" 作業，並輸出別名為 CustomerCount 的彙總值。  
  
8.  將 DataReader 目的地加入資料流程，然後將彙總轉換的輸出連接到 DataReader 目的地。 範例程式碼使用 "DataReaderDest" 做為 DataReader 的名稱。 為目的地選取單一可用的輸入資料行 CustomerCount。  
  
9. 儲存封裝。 建立的測試應用程式將執行封裝並直接從記憶體擷取其輸出。  
  
#### <a name="to-create-the-test-application"></a>建立測試應用程式  
  
1.  建立新的 Windows Form 應用程式。  
  
2.  瀏覽至 **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn** 中同名的組件，以新增 **Microsoft.SqlServer.Dts.DtsClient** 命名空間的參考。  
  
3.  將下列範例程式碼複製並貼入表單的程式碼模組。  
  
4.  視需要修改 **dtexecArgs** 變數值，使之包含 **dtexec.exe** 執行套件所需的命令列參數。 範例程式碼會從檔案系統載入封裝。  
  
5.  視需要修改 **dataReaderName** 變數值，使它包含套件中的 DataReader 目的地名稱。  
  
6.  在表單上放置按鈕與文字方塊。 範例程式碼使用 **btnRun** 作為按鈕的名稱，並使用 **txtResults** 作為文字方塊的名稱。  
  
7.  執行應用程式，然後按一下按鈕。 在簡短地暫停封裝執行之後，您應該會在表單的文字方塊中，看到封裝計算的彙總值 (加拿大的客戶計數)。  
  
### <a name="sample-code"></a>範例程式碼  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解本機與遠端執行之間的差異](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [以程式設計方式載入和執行本機封裝](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [以程式設計方式載入和執行遠端套件](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
