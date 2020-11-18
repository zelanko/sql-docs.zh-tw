---
title: 將 DB2 資料庫移轉至 SQL Server (DB2ToSQL) |Microsoft Docs
description: 使用這個建議的程式，將 DB2 資料庫移轉至 SQL Server 或 Azure SQL Database 使用 SQL Server 移轉小幫手 (SSMA) 。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e31d4b1d31cb186276d8424f8c49450cb4ce9406
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869526"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>將 DB2 資料庫移轉至 SQL Server (DB2ToSQL) 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for DB2 是全方位的環境，可協助您快速地將 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 您可以使用 SSMA for DB2 來查看資料庫物件和資料、評估要遷移的資料庫、將資料庫物件遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，然後將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 請注意，您無法遷移 SYS 和 SYSTEM DB2 架構。  
  
## <a name="recommended-migration-process"></a>建議的遷移程式  
若要成功將物件和資料從 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，請使用下列程式：  
  
1.  [新增 SSMA 專案](./new-project-db2tosql.md)。  
  
    建立專案之後，您可以設定專案轉換、遷移和類型對應選項。 如需專案設定的詳細資訊，請參閱 [&#40;轉換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) 和相關章節的專案設定。 如需如何自訂資料類型對應的詳細資訊，請參閱將 [DB2 和 SQL Server 資料類型對應 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
2.  [連接到 DB2 資料庫](./connecting-to-db2-database-db2tosql.md)。  
  
3.  [連接到 SQL Server](./connecting-to-sql-server-db2tosql.md)。  
  
4.  [將 DB2 架構對應至 SQL Server 架構](./mapping-db2-schemas-to-sql-server-schemas-db2tosql.md)。  
  
5.  （選擇性） [評估報表](./assessment-report-db2tosql.md) 以評估資料庫物件的轉換，並估計轉換時間。  
  
6.  [轉換 DB2 架構](./converting-db2-schemas-db2tosql.md)。  
  
7.  [將轉換的資料庫物件載入 SQL Server 中](./loading-converted-database-objects-into-sql-server-db2tosql.md)。  
  
    您可以透過下列其中一種方式來執行此動作：  
  
    -   儲存並執行腳本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   同步處理資料庫物件。  
  
8.  將[DB2 資料移轉至 SQL Server](./migrating-db2-data-into-sql-server-db2tosql.md)。  
  
9. 如有必要，請更新資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[消費者入門與 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
