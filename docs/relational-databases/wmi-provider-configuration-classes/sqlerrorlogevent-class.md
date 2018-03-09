---
title: "SqlErrorLogEvent 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 197fafbe3d6cea3f1e2d99a49d4e75a3b4adbba7
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 類別
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
|FileName|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 錯誤記錄檔的名稱。|  
|InstanceName|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> 記錄檔所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|LogDate|資料型別：**日期時間**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 將事件記錄到記錄檔中的日期和時間。|  
|訊息|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 事件訊息。|  
|ProcessInfo|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 事件之來源伺服器處理序識別碼 (SPID) 的相關資訊。|  
  
## <a name="remarks"></a>備註  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|네임스페이스|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>範例  
 下列範例會顯示如何擷取指定的記錄檔中所有已記錄事件的值。 若要執行範例時，取代\< *Instance_Name*> 的執行個體的名稱取代[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，例如 'Instance1'，並取代 'File_Name' 與錯誤記錄檔的名稱，例如，ERRORLOG.1' '。  
  
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
 當*InstanceName*或*FileName*並未提供的 WQL 陳述式中，查詢會傳回預設執行個體和目前資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔。 例如，下列 WQL 陳述式會傳回從目前的記錄檔 (ERRORLOG) 的預設執行個體 (MSSQLSERVER) 的所有記錄事件。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Security  
 若要連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔透過 WMI 中，您必須擁有下列權限，本機和遠端電腦上：  
  
-   讀取權限**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔位於下列路徑 (其中\<*磁碟機 >*表示安裝所在的磁碟機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和\< *InstanceName*> 是執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Drive>:\Program Files\Microsoft SQL Server\MSSQL13** **.\<InstanceName>\MSSQL\Log**  
  
 如果透過防火牆連接，請確定您已在遠端目標電腦上的 WMI 防火牆中設定例外狀況。 如需詳細資訊，請參閱[連接到 WMI 遠端從 Windows Vista 開始](http://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另請參閱  
 [SqlErrorLogFile 類別](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)  
  
  
