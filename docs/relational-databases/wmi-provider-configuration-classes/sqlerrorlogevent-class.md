---
title: SqlErrorLogEvent 類別
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d2a07c87dea5be1a3d66c5e24996a120323d09ce
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738462"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 類別
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  提供屬性，用來檢視指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔中的事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>屬性  
 SQLErrorLogEvent 類別會定義下列屬性。  
  
|||  
|-|-|  
|FileName|資料類型：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 錯誤記錄檔的名稱。|  
|InstanceName|資料類型：**字串**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> 記錄檔所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|LogDate|資料類型： **datetime**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 將事件記錄到記錄檔中的日期和時間。|  
|訊息|資料類型：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 事件訊息。|  
|ProcessInfo|資料類型：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 事件之來源伺服器處理序識別碼 (SPID) 的相關資訊。|  
  
## <a name="remarks"></a>備註  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空間|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>範例  
 下列範例會顯示如何擷取指定的記錄檔中所有已記錄事件的值。 若要執行範例，請將取代為 \<*Instance_Name*> 實例的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，例如 ' Instance1 '，並以錯誤記錄檔的名稱取代 ' File_Name '，例如 ' 錯誤記錄檔 1 '。  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>註解  
 當 WQL 語句中未提供*InstanceName*或*FileName*時，查詢將會傳回預設實例和目前記錄檔的資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，下列 WQL 陳述式將傳回來自預設執行個體 (MSSQLSERVER) 上之目前記錄檔 (ERRORLOG) 的所有記錄事件。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>安全性  
 若要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過 WMI 連接到記錄檔，您必須在本機和遠端電腦上都有下列許可權：  
  
-   **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間的讀取權限。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔位於下列路徑中（其中 \<*Drive> * 代表您安裝的磁片磁碟機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而 \<*InstanceName*> 是實例的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）：  
  
     ** \<Drive> ： \PROGRAM Files\Microsoft SQL Server\MSSQL13** **。 \<InstanceName>\MSSQL\Log**  
  
 如果透過防火牆連接，請確定您已在遠端目標電腦上的 WMI 防火牆中設定例外狀況。 如需詳細資訊，請參閱[從 Windows Vista 開始遠端連線到 WMI](https://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另請參閱  
 [SqlErrorLogFile 類別](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)  
  
  
