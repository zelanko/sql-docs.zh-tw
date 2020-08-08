---
title: " (SybaseToSQL) 建立伺服器連接檔案 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Server Connection Files
- Sybase Console,Server Connection File Validation
ms.assetid: 35ef396f-9f98-429d-9fc5-4f413d08fb37
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d50dead28fa182c946ec1abf0ac9cc4bb3f052d9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931881"
---
# <a name="creating-the-server-connection-files-sybasetosql"></a>建立伺服器連線檔案 (SybaseToSQL)
您可以在腳本檔案的 [伺服器] 區段中，或在個別的伺服器連接檔案中指定伺服器資訊。 伺服器連接檔案的命令列參數是、 `-c <serverconnectionfile>` 。 如果腳本檔案和伺服器連接檔案中同時出現相同的伺服器識別碼，則會考慮腳本檔案中的伺服器定義。  
  
**範例︰**  
  
```  
1.<!--Sample of server connection file commands -->  
  
<sybase name="<source-server-unique-name>">  
  
  <standard-mode>  
  
    <provider value="Ole DB Provider"/>  
  
    <server-name value="<server-name>"/>  
  
    <server-port value="<port>"/>  
  
    <user-id value="<password>"/>  
  
  </standard-mode>  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
```  
2.<!-Sample of server connection file commands-->  
<sybase name="<source-server-unique-name>">  
  
  <advanced-mode>  
  
    <connection-string value="User ID=<user-name>;Password=<password>;Provider=ASEOLEDB.1;Server=<server-name>;Port=<port>;OLE DB Services = -2;"/>  
  
  </advanced-mode >  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication >  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
## <a name="server-connection-file-validation"></a>伺服器連接檔案驗證  
使用者可以針對 [架構] 資料夾中提供的架構定義檔**S2SSConsoleScriptServersSchema** ，輕鬆地驗證其伺服器連接檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[執行 SSMA 主控台，&#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台](executing-the-ssma-console-sybasetosql.md)  
  
