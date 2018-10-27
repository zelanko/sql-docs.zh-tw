---
title: 建立伺服器連線檔案 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5ec1a21a717c642a4ca3b9ba83f3aba9636c8e4c
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099379"
---
# <a name="creating-the-server-connection-files-db2tosql"></a>建立伺服器連線檔案 (DB2ToSQL)
伺服器一節的指令碼檔案或不同的伺服器連線檔案中，可以指定伺服器的資訊。 伺服器連接檔案的命令列參數即`-c <serverconnectionfile>`。 如果存在於指令碼檔案與伺服器連線檔案相同的伺服器識別碼，則會視為在指令碼檔案中的伺服器定義。  
  
**範例： 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<db2 name="<source-server-unique-name>">  
  
    <standard-mode>  
  
      <connection-provider value ="OleDB Provider"/>  
  
      <!-- Defines server manager to connect.  
  
              Available manager attribute values  
  
              • zOs      - upgrades the project (default)  
  
              • LUW       - displays an error and halts the execution-->  
  
      <database-manager value="$Db2Manager$"/>  
  
      <server-name value="$Db2HostName$" />  
  
      <port value="$Db2Port$" />  
  
      <initial-catalog value="$Db2Instance$" />  
  
      <user-id value="$Db2UserName$" />  
  
      <password value="$Db2Password$"/>  
  
    </standard-mode>  
  
</db2>  
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
操作主控台的下一個步驟是[執行 SSMA 主控台&#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台](http://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
