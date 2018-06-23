---
title: SqlErrorLogFile 類別 |Microsoft 文件
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
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5e23c4512f04370fa24b3eb4ff3b74a072f6a2e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133677"
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
|[屬性]|資料類型：`string`<br /><br /> 存取類型：唯讀<br /><br /> 限定詞：索引鍵<br /><br /> <br /><br /> 記錄檔的名稱。|  
  
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
  
## <a name="security"></a>Security  
 若要連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔透過 WMI 中，您必須擁有下列權限，本機和遠端電腦上：  
  
-   讀取權限**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。  
  
    > [!NOTE]  
    >  如何確認 WMI 權限的相關資訊，請參閱本主題的 [安全性] 區段[檢視離線記錄檔](../logs/view-offline-log-files.md)。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔位於下列路徑 (其中\<*磁碟機 >* 表示安裝所在的磁碟機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和\< *InstanceName*> 是執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<磁碟機 >: \Program Files\Microsoft SQL Server\MSSQL11** **。\<執行個體名稱 > \MSSQL\Log**  
  
 如果透過防火牆連接，請確定您已在遠端目標電腦上的 WMI 防火牆中設定例外狀況。 如需詳細資訊，請參閱[連接到 WMI 遠端從 Windows Vista 開始](http://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另請參閱  
 [SqlErrorLogEvent 類別](sqlerrorlogevent-class.md)   
 [檢視離線記錄檔](../logs/view-offline-log-files.md)  
  
  