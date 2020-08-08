---
title: " (AccessToSQL) 建立伺服器連接檔案 |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b74cf86e6a68653a2047aebefc7ca86ab6868475
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933979"
---
# <a name="creating-the-server-connection-files-accesstosql"></a> (AccessToSQL 建立伺服器連接檔案) 
伺服器資訊可以在腳本檔案的 [伺服器] 區段中指定。 伺服器資訊也可以在個別的伺服器連接檔案中指定。 伺服器連接檔案的命令列參數是 `-c <serverconnectionfile>` 。 如果腳本和伺服器連接檔案中同時出現相同的伺服器識別碼，則會考慮腳本檔案中的伺服器定義。  
  
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
使用者可以針對 [架構] 資料夾中提供的架構定義檔 **' A2SSConsoleScriptServersSchema** ，輕鬆地驗證其伺服器連接檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[執行 SSMA 主控台，&#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[ (存取) 執行 SSMA 主控台](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
