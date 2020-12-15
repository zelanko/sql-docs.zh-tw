---
description: 使用 SQL Server Native Client 連線到 Azure SQL Database
title: 連線至 Azure SQL Database
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab4f4836d2d0979e6eed68a297f0d583dd612719
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462069"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>使用 SQL Server Native Client 連線到 Azure SQL Database
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如需示範如何使用 Native Client 連接到的 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 範例 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，請參閱 [開發：使用說明主題 (Azure SQL Database) ](/previous-versions/azure/ee621787(v=azure.100))。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>連接至 SQL 資料庫時的已知問題  
 以下是使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client 連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時的已知問題：  
  
-   如果階段使用 **SQLBrowseConnect** ，則可能會拒絕與 **SQLBrowseConnect** 建立的連接。  例如，如果在第一次呼叫中傳送驅動程式名稱，在第二次呼叫中傳送伺服器和認證 (使用者和密碼)，然後建立連接，再於第三次呼叫中傳送資料庫名稱和語言，  則第三次呼叫會導致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 發出 USE 陳述式以變更資料庫。 但是，[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 不支援 USE 陳述式，因此產生下列錯誤：  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
