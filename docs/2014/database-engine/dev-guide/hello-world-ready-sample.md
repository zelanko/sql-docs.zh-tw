---
title: Hello World Ready 範例 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1cb94266-f702-4a57-a1ae-689a89c98757
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e4fed72859ff91a9a0056529893c7f5664fe6254
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032622"
---
# <a name="hello-world-ready-sample"></a>Hello World Ready 範例
  Hello World Ready 範例示範涉及建立、部署及測試以簡單全球化整備 Common Language Runtime (CLR) 整合為基礎之預存程序的基本作業。 全球化整備元件可以輕鬆地當地語系化成全世界不同市場的不同語言，而不變更元件的原始程式碼。 此範例還示範如何透過輸出參數，以及透過由預存程序動態建構及傳回至用戶端的記錄來傳回資料。此範例與 Hello World 範例幾乎相同，但它可更容易、更安全地當地語系化此應用程式。 若要變更當地語系化文字，需要依照以下進行：  
  
1.  變更 XML 檔案 (。`resx` 檔案） 的資源目錄中的特定文化特性  
  
2.  使用 `resgen` 建立文化資源檔  
  
3.  為該文化建立已更新的附屬 DLL  
  
4.  在 SQL Server 中卸除及加入該組件  
  
 CLR 預存程序本身的原始程式碼和組件不會變更。 系統會提供 `build.cmd` 指令碼，其示範如何編譯及連結資源組件。雖然應用程式的原始程式碼會根據目前正在執行的組件建立資源管理員，但是您不一定要在包含預存程序的 DLL 中內嵌文化特性中性的資源。 `System.Resources.NeutralResourcesLanguage attribute` 允許文化特性中性的資源存在於附屬 DLL 中。 為此最好使用個別的 DLL，如此一來，當需要加入或變更當地語系化文字時，就無須變更包含 CLR 預存程序的主要 DLL。 這對 CLR 使用者定義型別特別有用，這些型別可能含有資料行及其他相依性，而使得型別難以卸除及重新加入。通常，附屬 DLL 版本必須與主組件版本相同。 不過，您也可以使用 `SatelliteContractVersion` 屬性來允許主組件更新，而不更新附屬組件。 如需詳細資訊，請參閱 Microsoft .NET 文件集中的 `ResourceManager` 類別。  
  
## <a name="prerequisites"></a>必要條件  
 此範例僅適用於 SQL Server 2005 和更新版本。  
  
 若要建立並執行這個專案，您必須安裝下列軟體：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文件集和範例[網站](http://go.microsoft.com/fwlink/?LinkId=31046)免費取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開發人員[網站](http://go.microsoft.com/fwlink/?linkid=62796)取得 AdventureWorks 資料庫  
  
-   .NET Framework SDK 2.0 或更新版本或是 Microsoft Visual Studio 2005 或更新版本。 您可以免費取得 .NET Framework SDK。  
  
-   此外，您也必須符合下列條件：  
  
-   您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須啟用 CLR 整合。  
  
-   若要啟用 CLR 整合，請執行下列步驟：  
  
    #### <a name="enabling-clr-integration"></a>啟用 CLR 整合  
  
    -   執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  若要啟用 CLR 整合，您必須擁有 `ALTER SETTINGS` 伺服器層級權限，此權限是由系統管理員 (`sysadmin`) 和伺服器管理員 (`serveradmin`) 固定伺服器角色的成員以隱含方式持有。  
  
-   AdventureWorks 資料庫必須安裝在您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。  
  
-   如果您不是正在使用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的管理員，則必須讓管理員授與您 **CreateAssembly** 權限來完成安裝。  
  
## <a name="building-the-sample"></a>建立範例  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>使用下列指示來建立並執行範例：  
  
1.  開啟 Visual Studio 或 .NET Framework 命令提示字元。  
  
2.  必要時，請建立範例的目錄。 在此範例中，我們將使用 C:\MySample。  
  
3.  在 c:\MySample 中，建立 `HelloWorld.vb` (適用於 Visual Basic 範例) 或 `HelloWorld.cs` (適用於 C# 範例) 並將適當的 Visual Basic 或 C# 範例程式碼 (下面) 複製到檔案中。  
  
4.  在 c:\MySample 中，建立 `messages.resx` 檔案並將範例程式碼複製到此檔案中。  
  
5.  在 c:\MySample，建立檔案`messages.de.resx`來儲存檔案`messages.resx`為`messages.de.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">Hallo Welt!</value>`  
  
6.  在 c:\MySample，建立檔案`messages.es.resx`來儲存檔案`messages.resx`為`messages.es.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">Hola a todos</value>`  
  
7.  在 c:\MySample，建立檔案`messages.fr.resx`來儲存檔案`messages.resx`為`messages.fr.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">BonjourÂ !</value>`  
  
8.  在 c:\MySample，建立檔案`messages.fr-FR.resx`來儲存檔案`messages.resx`為`messages.fr-FR.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">Bonjour de France!</value>`  
  
9. 在 c:\MySample，建立檔案`messages.it.resx`來儲存檔案`messages.resx`為`messages.it.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">Buongiorno</value>`  
  
10. 在 c:\MySample，建立檔案`messages.ja.resx`來儲存檔案`messages.resx`為`messages.ja.resx`之後變更的行  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   若要讀取  
  
    -   `<value xml:space="preserve">` `ã“ã‚“ã«ã¡ã¯</value>`  
  
11. 在 c:\MySample 中，建立 `build.com` 檔案並將範例程式碼複製到此檔案中。  
  
12. 執行在命令提示字元中建立的檔案，藉以建立附屬組件。  
  
13. 在命令列提示字元中執行下列其中一段程式碼，藉以編譯範例程式碼：  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:HelloWorldReady.dll /target:library HelloWorld.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /out:HelloWorldReady.dll /target:library Hello.csCopy the tsql installation code into a file and save it as Install.sql in the sample directory.`  
  
14. 如果此範例安裝在 `C:\MySample\` 以外的目錄中，請依照指示編輯 `Install.sql` 檔案，以指向該位置。  
  
15. 部署組件和預存程序，方法是執行  
  
    -   `sqlcmd -E -I -i install.sql`  
  
16. 複製[!INCLUDE[tsql](../../includes/tsql-md.md)]測試命令指令碼至檔案，並將它儲存成`test.sql`範例目錄中。  
  
17. 使用下列命令來執行測試指令碼  
  
    -   `sqlcmd -E -I -i test.sql`  
  
18. 將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除指令碼複製到檔案中，並將它儲存成範例目錄中的 `cleanup.sql`。  
  
19. 使用下列命令來執行指令碼  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>範例程式碼  
 下面是此範例的程式碼清單。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Globalization;  
using System.Threading;  
using System.Resources;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
  
[assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)]  
[assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)]  
[assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.MayCorruptInstance, System.Runtime.ConstrainedExecution.Cer.None)]  
  
    public sealed partial class StoredProcedures  
    {  
        private StoredProcedures()  
        {  
        }  
  
        [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1021:AvoidOutParameters"), Microsoft.SqlServer.Server.SqlProcedure]  
        public static void HelloWorldReady(string culture, out string greeting)  
        {  
ResourceManager rm   
= new ResourceManager("Messages",   
Assembly.GetExecutingAssembly());  
  
string message = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture));  
  
            Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 24);  
            SqlDataRecord greetingRecord  
                = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
            greetingRecord.SetString(0, message);  
            SqlContext.Pipe.Send(greetingRecord);  
            greeting = message;  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Globalization  
Imports System.Resources  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
<Assembly: AssemblyVersion("1.0.*")>   
<Assembly: System.Runtime.InteropServices.ComVisible(False)>   
<Assembly: System.CLSCompliant(True)>   
<Assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)>   
<Assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)>   
<Assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.WillNotCorruptState, Runtime.ConstrainedExecution.Cer.None)>   
  
Partial Public NotInheritable Class StoredProcedures  
    Private Sub New()  
    End Sub  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorldReady(ByVal culture As String, ByRef greeting As String)  
        Dim rm As New ResourceManager("Messages", Assembly.GetExecutingAssembly())  
        Dim message As String = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture))  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 24)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, message)  
        SqlContext.Pipe.Send(greetingRecord)  
        greeting = message  
    End Sub  
End Class  
  
```  
  
 這是 `build.com`，它會建立附屬組件。  
  
```  
resgen Messages.resx  
resgen Messages.de.resx  
resgen Messages.es.resx  
resgen Messages.fr.resx  
resgen Messages.fr-Fr.resx  
resgen Messages.it.resx  
resgen Messages.ja.resx  
if not exist de/ mkdir de  
if not exist es/ mkdir es  
if not exist fr/ mkdir fr  
if not exist fr-FR/ mkdir fr-FR  
if not exist it/ mkdir it  
if not exist ja/ mkdir ja  
al /t:lib /culture:de /embed:Messages.de.resources /out:de\HelloWorldReady.resources.dll  
al /t:lib /culture:es /embed:Messages.es.resources /out:es\HelloWorldReady.resources.dll  
al /t:lib /culture:fr /embed:Messages.fr.resources /out:fr\HelloWorldReady.resources.dll  
al /t:lib /culture:fr-FR /embed:Messages.fr-FR.resources /out:fr-FR\HelloWorldReady.resources.dll  
al /t:lib /culture:it /embed:Messages.it.resources /out:it\HelloWorldReady.resources.dll  
al /t:lib /culture:ja /embed:Messages.ja.resources /out:ja\HelloWorldReady.resources.dll  
al /t:lib /culture:"" /embed:Messages.resources /out:HelloWorldReady.resources.dll  
```  
  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝指令碼 (`Install.sql`)，它會部署組件並在資料庫中建立預存程序。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = N'C:\MySample\'  
  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY HelloWorldReady  
FROM @SamplesPath + 'HelloWorldReady.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.neutral]  
FROM @SamplesPath + 'HelloWorldReady.resources.dll'  
WITH permission_set = Safe;   
  
CREATE ASSEMBLY [HelloWorldReady.resources.de]  
FROM @SamplesPath + '\de\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.es]  
FROM @SamplesPath + '\es\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr]  
FROM @SamplesPath + '\fr\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr-FR]  
FROM @SamplesPath + '\fr-FR\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.it]  
FROM @SamplesPath + '\it\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.ja]  
FROM @SamplesPath + '\ja\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorldReady  
(  
@Culture NVarchar(12),  
@Greeting NVarchar(24) OUTPUT  
)  
AS EXTERNAL NAME HelloWorldReady.StoredProcedures.HelloWorldReady;  
GO  
  
USE master;  
GO  
```  
  
 這是 `test.sql`，它會在每個地區設定上執行函數，藉以測試範例。  
  
```  
USE AdventureWorks  
GO  
  
DECLARE @GreetingDe nvarchar(24);  
DECLARE @GreetingDe_CH nvarchar(24);  
DECLARE @GreetingEn nvarchar(24);  
DECLARE @GreetingEs nvarchar(24);  
DECLARE @GreetingFr nvarchar(24);  
DECLARE @GreetingFr_FR nvarchar(24);  
DECLARE @GreetingIt nvarchar(24);  
DECLARE @GreetingJa nvarchar(24);  
  
--German as spoken anywhere in the world (the neutral German culture)  
EXEC usp_HelloWorldReady 'de', @GreetingDe OUTPUT;  
--German as spoken in Switzerland.  Because we don't have a specific assembly  
--for this case, the .NET Framework will automatically fall back to the neutral German culture DLL.  
EXEC usp_HelloWorldReady 'de-CH', @GreetingDe_CH OUTPUT;  
EXEC usp_HelloWorldReady 'en', @GreetingEn OUTPUT;  
EXEC usp_HelloWorldReady 'es', @GreetingEs OUTPUT;  
--French as spoken anywhere in the world (the neutral French culture)  
EXEC usp_HelloWorldReady 'fr', @GreetingFr OUTPUT  
--French as spoken in France.  Since we do have a specific assembly for this case, a specific   
--greeting is provided from that DLL.  The neutral French culture DLL is not used in this case.  
EXEC usp_HelloWorldReady 'fr-FR', @GreetingFr_FR OUTPUT  
EXEC usp_HelloWorldReady 'it', @GreetingIt OUTPUT;  
EXEC usp_HelloWorldReady 'ja', @GreetingJa OUTPUT;  
  
SELECT @GreetingDe AS OUTPUT_PARAMETER_DE;  
SELECT @GreetingDe_CH AS OUTPUT_PARAMETER_De_CH;  
SELECT @GreetingEn AS OUTPUT_PARAMETER_EN;  
SELECT @GreetingEs AS OUTPUT_PARAMETER_ES;  
SELECT @GreetingFr AS OUTPUT_PARAMETER_FR;  
SELECT @GreetingFr_FR AS OUTPUT_PARAMETER_Fr_FR;  
SELECT @GreetingIt AS OUTPUT_PARAMETER_IT;  
SELECT @GreetingJa AS OUTPUT_PARAMETER_JA;  
  
GO  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會從資料庫中移除組件和預存程序。  
  
```  
USE AdventureWorks;  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
USE master;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  