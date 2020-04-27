---
title: SqlErrorLogFile 類別 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c5c6f1998cffc268a57318e0124f74d3411a3b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63249320"
---
# <a name="sqlerrorlogfile-class"></a>SqlErrorLogFile 類別
  提供屬性，用來檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>屬性  
 SQLErrorLogFile 類別會定義下列屬性。  
  
|||  
|-|-|  
|ArchiveNumber|資料類型：`uint32`<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 記錄檔的封存數目。|  
|InstanceName|資料類型：`string`<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 記錄檔所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|LastModified|資料類型：`datetime`<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 上次修改記錄檔的日期。|  
|LogFileSize|資料類型：`uint32`<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 記錄檔的大小 (以位元組為單位)。|  
|名稱|資料類型：`string`<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 記錄檔的名稱。|  
  
## <a name="remarks"></a>備註  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空間|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>範例  
 下列範例會抓取指定之[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例上所有記錄檔的相關資訊。 若要執行範例，請\<將*Instance_Name*> 取代為實例的名稱，例如 ' Instance1 '。  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>評價  
 當 WQL 語句中未提供*InstanceName*時，查詢將會傳回預設實例的資訊。 例如，下列 WQL 陳述式將傳回來自預設執行個體 (MSSQLSERVER) 的所有記錄檔相關資訊。  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>安全性  
 若要透過 WMI [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到記錄檔，您必須在本機和遠端電腦上都有下列許可權：  
  
-   **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間的讀取權限。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。  
  
    > [!NOTE]  
    >  如需有關如何驗證 WMI 許可權的詳細資訊，請參閱主題 [[離線記錄](../logs/view-offline-log-files.md)檔] 中的 [安全性] 區段。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔會位於下列路徑（其中\< *Drive>* 代表您安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的磁片磁碟機，而\< *InstanceName*> 是實例的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）：  
  
     **磁片磁碟機>： \Program Files\Microsoft SQL Server\MSSQL11。 \< ** ** \<InstanceName> \MSSQL\Log**  
  
 如果透過防火牆連接，請確定您已在遠端目標電腦上的 WMI 防火牆中設定例外狀況。 如需詳細資訊，請參閱[從 Windows Vista 開始遠端連線到 WMI](https://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另請參閱  
 [SqlErrorLogEvent 類別](sqlerrorlogevent-class.md)   
 [檢視離線記錄檔](../logs/view-offline-log-files.md)  
  
  
