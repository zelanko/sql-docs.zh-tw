---
title: "LocalDB 的 SQL Server Native Client 支援 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9bad296ee4f5d0d713441981cb4e536eeec7ca31
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client 對 LocalDB 的支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，將會提供稱為 LocalDB 的輕量版 SQL Server。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。  
  
## <a name="remarks"></a>備註  
 如需有關 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱：  
  
-   [SQL Server Express LocalDB 參考](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 總而言之，LocalDB 可讓您：  
  
-   使用**sqllocaldb.exe 我**探索預設執行個體的名稱。  
  
-   使用**AttachDBFilename**應該附加至指定的資料庫檔案伺服器的連接字串關鍵字。 使用時**AttachDBFilename**，如果您未指定的資料庫名稱**資料庫**連接字串關鍵字，資料庫會移除的 LocalDB 執行個體時應用程式會關閉。  
  
-   在連接字串中指定 LocalDB 執行個體：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如， **sqlcmd-S (localdb) \v11.0**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
