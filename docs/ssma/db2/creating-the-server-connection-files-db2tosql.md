---
title: 建立伺服器連接檔案（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4a1ee05cbf14f18a34b15161eec88df04be5539b
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2020
ms.locfileid: "86392776"
---
# <a name="creating-the-server-connection-files-db2tosql"></a>建立伺服器連接檔案（DB2ToSQL）

您可以在腳本檔案的 [伺服器] 區段中，或在個別的伺服器連接檔案中指定伺服器資訊。 伺服器連接檔案的命令列參數是、 `-c <serverconnectionfile>` 。 如果腳本檔案和伺服器連接檔案中同時出現相同的伺服器識別碼，則會考慮腳本檔案中的伺服器定義。

**範例：1**

```xml
<!-- Sample of server connection file commands -->
<db2 name="<source-server-unique-name>">
  <standard-mode>

    <connection-provider value="OleDB Provider" />

    <!-- Defines server manager to connect.
         Available manager attribute values
           • zOs - DB2 for z/OS
           • LUW - DB2 for Linux, Unix and Windows
           • DBi - DB2 for i -->
    <database-manager value="$Db2Manager$" />

    <server-name value="$Db2HostName$" />

    <port value="$Db2Port$" />

    <initial-catalog value="$Db2Instance$" />

    <user-id value="$Db2UserName$" />

    <password value="$Db2Password$"/>

  </standard-mode>
</db2>
```

```xml
<sql-server name="<target-server-unique-name>">
  <sql-server-authentication>

    <server value="<server-name>" />

    <database value="<database-name>" />
  
    <user-id value="<user-name>"/>
  
    <password value="<password>"/>

  </sql-server-authentication>
</sql-server>
```

## <a name="next-step"></a>後續步驟

操作主控台的下一個步驟是[執行 SSMA 主控台，&#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)

## <a name="see-also"></a>另請參閱

- [執行 SSMA 主控台](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)
