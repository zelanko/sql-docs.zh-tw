---
description: 回送案例的用戶端憑證驗證
title: 回送案例的用戶端憑證驗證 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: peterbae
ms.author: v-hyba
ms.openlocfilehash: bfc8816c30020669918b3632f94e289524097537
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438440"
---
# <a name="client-certificate-authentication-for-loopback-scenarios"></a>Loopback 案例的用戶端憑證驗證

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 2016 中已新增名為 sp_execute_external_script (SPEES) 的新預存程序。 此預存程序可讓 SQL Server 啟動並執行 SQL Server 之外的外部指令碼，作為擴充性工作的一部分。 其也帶來 R 與 Python 指令碼的支援，兩者皆具有可以使用 JDBC 驅動程式來連線至 SQL Server 的程式庫。 雖然 Windows 電腦上的 SQL Server 可以使用 Windows 整合式驗證搭配與啟動查詢之使用者相同的認證來驗證這些回送連線，Linux SQL Server 並無法做到這一點。 因此，已新增用戶端憑證驗證來允許使用者使用憑證與金鑰來進行驗證。

## <a name="connecting-using-client-certificate-authentication"></a>使用用戶端憑證驗證進行連線

JDBC 驅動程式針對此功能新增三個連線屬性：

* clientCertificate - 指定要用於驗證的憑證。 JDBC 驅動程式將會支援 PFX、PEM、DER 與 CER 副檔名。

格式
```
clientCertificate=<file_location>
``` 
驅動程式會使用憑證檔案。 針對 PEM、DER 與 CER 格式的憑證，clientKey 屬性為必要項目。 檔案位置可以是相對或絕對的。
 
* clientKey - 針對 clientCertificate 屬性所指定的 PEM、DER 與 CER 憑證，指定私密金鑰的檔案位置。

格式
```
clientKey=<file_location>
```
指定私密金鑰檔案的位置。 如果私密金鑰檔案受到密碼保護，則需要密碼關鍵字。 檔案位置可以是相對或絕對的。

* clientKeyPassword - 提供以存取 clientKey 檔案之私密金鑰的選擇性密碼字串。

此功能僅正式支援針對 Linux SQL Server 2019 與更新版本的回送驗證案例。

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
