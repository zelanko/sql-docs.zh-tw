---
description: 建立伺服器連線檔案 (MySQLToSQL)
title: 建立伺服器連接檔案 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server connection file validation
- Server connection files
ms.assetid: df0e970c-da0b-4118-b359-c9dcbbad16d6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8799b58a43c5456141694ded0d82f87afd88eb60
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988420"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>建立伺服器連線檔案 (MySQLToSQL)
您可以在腳本檔案的 [伺服器] 區段或個別的伺服器連接檔案中指定伺服器資訊。 伺服器連接檔案的命令列參數為、 `-c <serverconnectionfile>` 。 如果腳本檔案和伺服器連接檔案中同時出現相同的伺服器識別碼，則會考慮腳本檔中的伺服器定義。  
  
**範例︰**  
  
```xml  
<!--Sample of server connection file commands -->  
  
<mysql name ="<source-server-unique-name>">  
  
   <standard-mode>  
  
      <server value ="<server-name>"/>  
  
      <user-id value ="<user-name>"/>  
  
      <password value ="<password>"/>  
  
      <port value ="<port>"/>  
  
   </standard-mode>  
  
</mysql>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
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
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="<target-server-unique-name>">  
  
   <server value="<server-name>"/>  
  
   <database value="<database-name>"/>  
  
   <user-id value="<user-name>"/>  
  
   <password value="<password>"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>伺服器連接檔案驗證  
使用者可以在 [架構] 資料夾中，輕鬆地針對架構定義檔 ' **2ssconsolescriptserversschema .xsd '** 驗證其伺服器連接檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是 [執行 SSMA 主控台 &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[ (MySQL) 執行 SSMA 主控台 ](./executing-the-ssma-console-mysqltosql.md)  
