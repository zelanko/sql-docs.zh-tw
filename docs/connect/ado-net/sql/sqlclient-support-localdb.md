---
title: SqlClient 對 LocalDB 的支援
description: 描述 SqlClient 對 LocalDB 資料庫的支援。
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 189d0a2997b256f9c9b615fc81b5b9ed3ef46a5c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918726"
---
# <a name="sqlclient-support-for-localdb"></a>SqlClient 對 LocalDB 的支援

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

從 SQL Server 代號名稱 Denali 開始，將會提供稱為 LocalDB 的輕量版 SQL Server。 此主題將討論如何連線到 LocalDB 資料庫。  
  
## <a name="remarks"></a>備註  
如需 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱《SQL Server 線上叢書》。  
  
摘要說明您可以使用 LocalDB 執行的作業：  
  
- 使用 sqllocaldb.exe 或您的 app.config 檔案來建立及啟動 LocalDB 執行個體。  
  
- 使用 sqlcmd.exe 可在 LocalDB 執行個體中新增和修改資料庫。 例如： `sqlcmd -S (localdb)\myinst` 。  
  
- 使用 `AttachDBFilename` 連接字串關鍵字，將資料庫新增至您的 LocalDB 執行個體。 使用 `AttachDBFilename` 時，如果您沒有使用 `Database` 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。  
  
- 請在連接字串中指定 LocalDB 執行個體。 例如，您的執行個體名稱是 `myInstance`，連接字串就會包含：  
  
```console
server=(localdb)\\myInstance  
```  
  
連線到 LocalDB 資料庫時，不允許使用 `User Instance=True`。  
  
您可以從 [Microsoft SQL Server 2012 功能套件](https://www.microsoft.com/download/en/details.aspx?id=29065)下載 LocalDB。 如果您將使用 sqlcmd.exe 來修改 LocalDB 執行個體中的資料，您將需要 SQL Server 2012 中的 sqlcmd，您也可以從 SQL Server 2012 功能套件取得 sqlcmd。  
  
## <a name="programmatically-create-a-named-instance"></a>以程式設計方式建立具名執行個體  
應用程式可以建立具名執行個體，並指定資料庫，如下所示：  
  
- 指定要在 app.config 檔案中建立的 LocalDB 執行個體，如下所示。  執行個體的版本號碼應該與您 LocalDB 安裝的版本號碼相同。  
  
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
  
- 使用 `server` 連接字串關鍵字來指定執行個體的名稱。  在 `server` 連接字串關鍵字中指定的執行個體名稱，必須與 app.config 檔案指定的名稱相符。  
  
- 使用 `AttachDBFilename` 連接字串關鍵字來指定 .MDF 檔案。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
