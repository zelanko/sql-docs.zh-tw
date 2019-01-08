---
title: 建立伺服器連線檔案 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fabc454fe6adc77ec3e9789925e099fb6b0de6b1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407738"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>建立伺服器連線檔案 (AccessToSQL)
伺服器的資訊可以是指定伺服器一節的指令碼檔案。 伺服器的資訊也可以指定不同的伺服器連線檔案中。 伺服器連接檔案的命令列參數是`-c <serverconnectionfile>`。 相同的伺服器識別碼是否存在於指令碼和伺服器連線檔案，則會視為在指令碼檔案中的伺服器定義。  
  
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
  
## <a name="server-connection-file-validation"></a>伺服器連線檔案驗證  
使用者可以輕鬆地驗證他/她伺服器連線檔案對結構描述定義檔 **'A2SSConsoleScriptServersSchema.xsd'** 可用 [結構描述] 資料夾中。  
  
## <a name="next-step"></a>下一步  
操作主控台的下一個步驟是[執行 SSMA 主控台&#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 （存取）](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
