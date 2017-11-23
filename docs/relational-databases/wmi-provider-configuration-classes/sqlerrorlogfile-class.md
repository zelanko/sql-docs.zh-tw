---
title: "SqlErrorLogFile 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0c3bf6c5f7121a4420410230c29a63492a0a353
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sqlerrorlogfile-class"></a>SqlErrorLogFile 類別
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]提供用於檢視相關資訊的屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔。  
  
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
|ArchiveNumber|資料型別： **uint32**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 記錄檔的封存數目。|  
|InstanceName|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 記錄檔所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|LastModified|資料型別：**日期時間**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 上次修改記錄檔的日期。|  
|LogFileSize|資料型別： **uint32**<br /><br /> 存取類型：唯讀<br /><br /> <br /><br /> 記錄檔的大小 (以位元組為單位)。|  
|名稱|資料型別：**字串**<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 記錄檔的名稱。|  
  
## <a name="remarks"></a>備註  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空間|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>範例  
 下列範例會擷取所有的相關資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上指定的執行個體的記錄檔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要執行範例時，取代\< *Instance_Name*> 的執行個體，例如，'Instance1' 的名稱。  
  
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
  
## <a name="comments"></a>註解  
 當*InstanceName*中未提供的 WQL 陳述式中，查詢會傳回預設執行個體的資訊。 例如，下列 WQL 陳述式將傳回來自預設執行個體 (MSSQLSERVER) 的所有記錄檔相關資訊。  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>安全性  
 若要連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔透過 WMI 中，您必須擁有下列權限，本機和遠端電腦上：  
  
-   讀取權限**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。  
  
    > [!NOTE]  
    >  如何確認 WMI 權限的相關資訊，請參閱本主題的 [安全性] 區段[檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔位於下列路徑 (其中\<*磁碟機 >*表示安裝所在的磁碟機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和\< *InstanceName*> 是執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<磁碟機 >: \Program Files\Microsoft SQL Server\MSSQL11** **。\<執行個體名稱 > \MSSQL\Log**  
  
 如果透過防火牆連接，請確定您已在遠端目標電腦上的 WMI 防火牆中設定例外狀況。 如需詳細資訊，請參閱[連接到 WMI 遠端從 Windows Vista 開始](http://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>請參閱＜  
 [SqlErrorLogEvent 類別](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md)   
 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)  
  
  
