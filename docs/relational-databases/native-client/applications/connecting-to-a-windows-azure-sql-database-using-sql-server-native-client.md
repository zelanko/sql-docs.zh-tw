---
title: "連接到 Windows Azure SQL 資料庫使用 SQL Server Native Client |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: native-client|applications
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d52109ed61ad125deadb35dacf7a0426601951c4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="connecting-to-a-windows-azure-sql-database-using-sql-server-native-client"></a>使用 SQL Server Native Client 連接至 Windows Azure SQL 資料庫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  如需範例，示範如何連接到[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，請參閱[開發： 使用說明主題 (Windows Azure SQL Database)](http://msdn.microsoft.com/library/ee621787.aspx)。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>連接至 SQL 資料庫時的已知問題  
 以下是使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client 連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時的已知問題：  
  
-   與所建立的連接**SQLBrowseConnect**如果可能會遭到拒絕**SQLBrowseConnect**階段中使用。  例如，如果在第一次呼叫中傳送驅動程式名稱，在第二次呼叫中傳送伺服器和認證 (使用者和密碼)，然後建立連接，再於第三次呼叫中傳送資料庫名稱和語言，  則第三次呼叫會導致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 發出 USE 陳述式以變更資料庫。 但是，[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 不支援 USE 陳述式，因此產生下列錯誤：  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
