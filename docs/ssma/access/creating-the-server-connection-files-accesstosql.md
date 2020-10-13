---
description: '建立伺服器連接檔案 (AccessToSQL) '
title: 建立伺服器連接檔案 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 20c47935963473b7b6aced7d6b3eed4a53afbeac
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987514"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>建立伺服器連接檔案 (AccessToSQL) 
伺服器資訊可以在腳本檔案的 [伺服器] 區段中指定。 伺服器資訊也可以在個別的伺服器連接檔案中指定。 伺服器連接檔案的命令列參數為 `-c <serverconnectionfile>` 。 如果腳本和伺服器連接檔案中同時存在相同的伺服器識別碼，則會考慮腳本檔中的伺服器定義。  
  
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
使用者可以根據 [架構] 資料夾中提供的架構定義檔 **' A2SSConsoleScriptServersSchema .xsd '** ，輕鬆地驗證他/她的伺服器連接檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是 [執行 SSMA 主控台 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 (存取) ](./executing-the-ssma-console-accesstosql.md)  
