---
title: 建立伺服器連線檔案 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server Connection File Creation
- Server Connection File, Server Connection File Validation
ms.assetid: 002f129e-0868-48ad-a4b4-c68b5007e12e
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 8f6eabe706197e8ab2bfb882510b6063bf4e884c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839346"
---
# <a name="creating-the-server-connection-files-oracletosql"></a>建立伺服器連線檔案 (OracleToSQL)
伺服器一節的指令碼檔案或不同的伺服器連線檔案中，可以指定伺服器的資訊。 伺服器連接檔案的命令列參數即`-c <serverconnectionfile>`。 如果存在於指令碼檔案與伺服器連線檔案相同的伺服器識別碼，則會視為在指令碼檔案中的伺服器定義。  
  
**範例 1:**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <tns-name-mode>  
  
    <connection-provider value="OracleClient"/>  
  
    <service-name value="(DESCRIPTION =(ADDRESS_LIST =(ADDRESS = (PROTOCOL = TCP)(HOST = <host-name>)(PORT = 1521)))(CONNECT_DATA =(SERVICE_NAME = <service-name>)))"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </tns-name-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
**範例： 2**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <connection-string-mode>  
  
    <connection-provider value="OleDB Provider"/>  
  
    <custom-connection-string value="Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<host-name>)(PORT=1521))(CONNECT_DATA=(SID=<instance-name>)));User ID=<user-name>;Password=<password>"/>  
  
  </connection-string-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
## <a name="next-step"></a>下一個步驟  
操作主控台的下一個步驟是[執行 SSMA 主控台&#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台](executing-the-ssma-console-oracletosql.md)  
  
