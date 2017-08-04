---
title: "建立伺服器連接檔案 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 333640f0b258c97ba87c56fe4bd8a15100bba858
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="creating-the-server-connection-files-accesstosql"></a>建立伺服器連接檔案 (AccessToSQL)
指令碼檔案的 [伺服器] 區段中或在不同的伺服器連接檔案中，可以指定伺服器的資訊。 伺服器連接檔案的命令列參數即`-c <serverconnectionfile>`。 如果指令碼檔案和伺服器連接檔案中存在相同的伺服器識別碼，則會被視為指令碼檔案中的伺服器定義。  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>伺服器連接檔案驗證  
使用者可輕鬆地驗證其伺服器連線檔之結構描述定義檔**'A2SSConsoleScriptServersSchema.xsd'**可用 '結構描述' 資料夾中。  
  
## <a name="next-step"></a>下一個步驟  
在操作主控台的下一個步驟是[執行 SSMA 主控台 &#40;AccessToSQL &#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  

