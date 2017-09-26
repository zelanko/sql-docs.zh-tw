---
title: "使用指令碼元件建立 ODBC 目的地 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>使用指令碼元件建立 ODBC 目的地
  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，您通常將資料儲存到 ODBC 目的地使用[!INCLUDE[vstecado](../../includes/vstecado-md.md)]目的地和[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]Data Provider for ODBC。 不過，您也可以建立在單一封裝中要使用的特定 ODBC 目的地。 若要建立這個特定的 ODBC 目的地，可以使用如下列範例所示的指令碼元件。  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>範例  
 下列範例示範如何建立一個目的地元件，使用現有的 ODBC 連接管理員加入到資料流程中的資料儲存[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 這個範例是自訂的修改的版本[!INCLUDE[vstecado](../../includes/vstecado-md.md)]> 主題中所示範的目的[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 不過，在這個範例中，已修改自訂 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地以搭配 ODBC 連接管理員使用，並將資料儲存到 ODBC 目的地。 這些修改也包括下列變更：  
  
-   您不能呼叫**AcquireConnection**方法的 ODBC 連接管理員，從 managed 程式碼，因為它會傳回原生物件。 因此，這個範例使用連接管理員的連接字串以 Managed ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者直接連到資料來源。  
  
-   **OdbcCommand**需要位置參數。 參數的位置由命令文字中的問號 (?) 指出  (相較之下， **SqlCommand**需要具名的參數。)  
  
 這個範例會使用**Person.Address**資料表中**AdventureWorks**範例資料庫。 範例會將第一個和第四個資料行， * *int*AddressID** * 和**nvarchar (30) 縣 （市)**資料行，並透過資料流程此資料表。 用於這個相同的資料來源、 轉換和目的地範例 > 主題中的[開發特定類型的指令碼元件](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  建立 ODBC 連接管理員，連接到**AdventureWorks**資料庫。  
  
2.  建立目的地資料表中執行下列 TRANSACT-SQL 命令**AdventureWorks**資料庫：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
4.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件  (不需要任何轉換，就可以直接將來源連接到目的地)。為了確保這個範例可運作，上游元件的輸出必須包含至少**AddressID**和**縣 （市)**中的資料行**Person.Address**資料表**AdventureWorks**範例資料庫。  
  
5.  開啟**指令碼轉換編輯器**。 在**的輸入資料行**頁面上，選取**AddressID**和**縣 （市)**資料行。  
  
6.  在**輸入和輸出**頁面上，例如重新命名以更具描述性的名稱輸入**MyAddressInput**。  
  
7.  在**連接管理員**頁面上，加入或建立 ODBC 連接管理員使用描述性的名稱這類**MyODBCConnectionManager**。  
  
8.  在**指令碼**頁面上，按一下**編輯指令碼**，然後輸入指令碼中，如下所示**ScriptMain**類別。  
  
9. 關閉指令碼開發環境中，關閉**指令碼轉換編輯器**，然後執行範例。  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
