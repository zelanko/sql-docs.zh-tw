---
title: SQL Server Native Client 支援 localdb |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 245c50f73b15792a8cd3535aaba32f84f57e3b3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62744760"
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
  
-   使用**sqllocaldb.exe 我**探索的預設執行個體的名稱。  
  
-   使用 **AttachDBFilename** 連接字串關鍵字來指定伺服器應該附加的資料庫檔案。 使用 **AttachDBFilename** 時，如果您沒有使用 **Database** 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。  
  
-   在連接字串中指定 LocalDB 執行個體：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如， **sqlcmd-S (localdb) \v11.0**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
