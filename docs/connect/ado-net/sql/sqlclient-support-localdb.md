---
title: SqlClient 對 LocalDB 的支援
description: 描述 LocalDB 資料庫的 SqlClient 支援。
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 14cbe4ccf227c9462d2a2dc19fb42d913ca7bc5a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451978"
---
# <a name="sqlclient-support-for-localdb"></a>SqlClient 對 LocalDB 的支援

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

從 SQL Server 的程式碼名稱 Denali 開始，將會提供輕量版本的 SQL Server （稱為 LocalDB）。 本主題討論如何連接到 LocalDB 資料庫。  
  
## <a name="remarks"></a>Remarks  
如需 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱《SQL Server 線上叢書》。  
  
總結您可以使用 LocalDB 執行的工作：  
  
- 使用 sqllocaldb 或 app.config 檔案來建立及啟動 LocalDB 實例。  
  
- 使用 sqlcmd.exe 可在 LocalDB 執行個體中新增和修改資料庫。 例如， `sqlcmd -S (localdb)\myinst`。  
  
- 使用 `AttachDBFilename` 連接字串關鍵字，將資料庫加入至您的 LocalDB 實例。 使用 `AttachDBFilename` 時，如果您沒有使用 `Database` 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。  
  
- 請在連接字串中指定 LocalDB 執行個體。 例如，您的實例名稱是 `myInstance`，連接字串會包含：  
  
```console
server=(localdb)\\myInstance  
```  
  
連接到 LocalDB 資料庫時，不允許 `User Instance=True`。  
  
您可以從 [Microsoft SQL Server 2012 功能套件](https://www.microsoft.com/download/en/details.aspx?id=29065)下載 LocalDB。 如果您將使用 sqlcmd.exe 來修改 LocalDB 執行個體中的資料，您將需要 SQL Server 2012 中的 sqlcmd，您也可以從 SQL Server 2012 功能套件取得 sqlcmd。  
  
## <a name="programmatically-create-a-named-instance"></a>以程式設計方式建立已命名的實例  
應用程式可以建立名為的實例，並指定資料庫，如下所示：  
  
- 指定要在 app.config 檔案中建立的 LocalDB 實例，如下所示。  實例的版本號碼應該與 LocalDB 安裝的版本號碼相同。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- 使用 `server` 連接字串關鍵字來指定實例的名稱。  在 `server` 連接字串關鍵字中指定的執行個體名稱，必須與 app.config 檔案指定的名稱相符。  
  
- 請使用 `AttachDBFilename` 連接字串關鍵字來指定.MDF 檔案。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
