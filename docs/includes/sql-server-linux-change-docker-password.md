---
ms.openlocfilehash: 4803a99e0fb1435b545ec775b2a8abe063d9fd8d
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890913"
---
**SA** 帳戶是在安裝期間建立的 SQL Server 執行個體系統管理員。 在您建立 SQL Server 容器之後，在容器中執行 `echo $MSSQL_SA_PASSWORD`，即可探索您指定的 `MSSQL_SA_PASSWORD` 環境變數。 基於安全性考量，請變更您的 SA 密碼：

1. 選擇要為 SA 使用者使用的強式密碼。

1. 使用 `docker exec` 來執行 **sqlcmd** 公用程式，以透過 Transact-SQL 陳述式來變更密碼。 將 `<YourStrong!Passw0rd>` 與 `<YourNewStrong!Passw0rd>` 取代為您自己的密碼值：

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
