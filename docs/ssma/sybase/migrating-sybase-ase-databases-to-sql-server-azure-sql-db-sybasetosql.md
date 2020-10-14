---
title: 將 Sybase ASE 資料庫移轉至 SQL Server Azure SQL Database |Microsoft Docs
description: 使用這個建議的程式，將 SAP 調適型 Server Enterprise 資料庫移轉至 SQL Server 或 Azure SQL Database 使用 SQL Server 移轉小幫手 (SSMA) 。
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f37f80cda41279b7c773d7a2c89216c5f24e9000
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034975"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database (SybaseToSQL) 
SQL Server 移轉小幫手 SAP 調適型 Server Enterprise (ASE)  (SSMA) 是全方位的環境，可協助您快速地將 SAP ASE 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 藉由使用 SSMA for SAP ASE，您可以查看資料庫物件和資料、評估要遷移的資料庫、將資料庫物件遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，然後將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功將物件和資料從 SAP ASE 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，請使用下列程式：  
  
1.  [建立新的 SSMA 專案](working-with-ssma-projects-sybasetosql.md)。  
  
    建立專案之後，您可以設定專案轉換、遷移和類型對應選項。 如需專案設定的詳細資訊，請參閱 [&#40;SybaseToSQL&#41;設定專案選項 ](../../ssma/sybase/setting-project-options-sybasetosql.md)。 如需自訂資料類型對應的相關資訊，請參閱 [對應 SYBASE ASE 和 SQL Server 資料類型 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [連接到 SAP ASE 資料庫伺服器](connecting-to-sybase-ase-sybasetosql.md)。  
  
3.  [SQL Server 連接到實例](connecting-to-sql-server-sybasetosql.md) ，或 [連接到 Azure SQL Database 的實例](connecting-to-azure-sql-db-sybasetosql.md)。  
  
4.  [將 SAP ASE 資料庫架構對應至 SQL Server/Azure SQL Database 資料庫架構](./mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
5.  （選擇性） [建立評量報告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) 以評估資料庫物件的轉換，並估計轉換時間。  
  
6.  [將 SAP ASE 資料庫架構轉換成 SQL Server/Azure SQL Database 架構](./converting-sybase-ase-database-objects-sybasetosql.md)。  
  
7.  [將轉換的資料庫物件載入 SQL Server/Azure SQL Database](./loading-converted-database-objects-into-sql-server-sybasetosql.md)。  
  
    請儲存腳本，並在中執行腳本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，或同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server/Azure SQL Database](./migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)。  
  
9. 如有必要，請更新您的資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝適用于 SAP ASE 的 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[消費者入門搭配適用于 SAP ASE 的 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
