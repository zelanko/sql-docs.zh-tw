---
title: LocalDB 的支援
description: 瞭解如何連接到 LocalDB 實例中的資料庫，這是 SQL Server Native Client 所支援 SQL Server 的輕量版本。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc043b9e26f9a940575689b9392efef5b7ee1a4a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009896"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client 對 LocalDB 的支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，將會提供稱為 LocalDB 的輕量版 SQL Server。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。  
  
## <a name="remarks"></a>備註  
 如需有關 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱：  
  
-   [SQL Server Express LocalDB 參考](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 總而言之，LocalDB 可讓您：  
  
-   使用 **sqllocaldb.exe i** 來探索預設執行個體的名稱。  
  
-   使用 **AttachDBFilename** 連接字串關鍵字來指定伺服器應該附加的資料庫檔案。 使用 **AttachDBFilename** 時，如果您沒有使用 **Database** 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。  
  
-   在連接字串中指定 LocalDB 執行個體：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如，**sqlcmd -S (localdb)\v11.0**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
