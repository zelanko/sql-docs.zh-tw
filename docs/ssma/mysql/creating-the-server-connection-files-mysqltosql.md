---
title: " (MySQLToSQL) 建立伺服器連接檔案 |Microsoft Docs"
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
ms.openlocfilehash: fa9505c0f5c40dcf2ff7cd84fc956240728385b3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935727"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>建立伺服器連線檔案 (MySQLToSQL)
您可以在腳本檔案的 [伺服器] 區段中，或在個別的伺服器連接檔案中指定伺服器資訊。 伺服器連接檔案的命令列參數是、 `-c <serverconnectionfile>` 。 如果腳本檔案和伺服器連接檔案中同時出現相同的伺服器識別碼，則會考慮腳本檔案中的伺服器定義。  
  
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
使用者可以針對 [架構] 資料夾中提供的架構定義檔 [ **2ssconsolescriptserversschema** ]，輕鬆驗證其伺服器連接檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[執行 SSMA 主控台，&#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[ (MySQL) 執行 SSMA 主控台](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
