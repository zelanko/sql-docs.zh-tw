---
title: 將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft Docs
description: 使用此建議的程式，將 SAP 調適型伺服器企業資料庫移轉至使用 SQL Server 移轉小幫手（SSMA） SQL Server 或 Azure SQL Database。
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a9bcca5d23fe147394a350ff8c640680ec674675
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292815"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database （SybaseToSQL）
適用于 SAP 調適型伺服器 Enterprise （ASE）的 SQL Server 移轉小幫手（SSMA）是一種完整的環境，可協助您快速將 SAP ASE 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 藉由使用適用于 SAP ASE 的 SSMA，您可以查看資料庫物件和資料、評估要遷移的資料庫、將資料庫物件遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，然後將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功地將物件和資料從 SAP ASE 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，請使用下列程式：  
  
1.  [建立新的 SSMA 專案](working-with-ssma-projects-sybasetosql.md)。  
  
    建立專案之後，您可以設定專案轉換、遷移和類型對應選項。 如需專案設定的詳細資訊，請參閱[&#40;SybaseToSQL&#41;設定專案選項](../../ssma/sybase/setting-project-options-sybasetosql.md)。 如需自訂資料類型對應的詳細資訊，請參閱將[SYBASE ASE 和 SQL Server 資料類型對應 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [連接到 SAP ASE 資料庫伺服器](connecting-to-sybase-ase-sybasetosql.md)。  
  
3.  [SQL Server 連接到實例](connecting-to-sql-server-sybasetosql.md)，或[連接到 Azure SQL Database 的實例](connecting-to-azure-sql-db-sybasetosql.md)。  
  
4.  [將 SAP ASE 資料庫架構對應至 SQL Server/Azure SQL Database 資料庫架構](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （選擇性）[建立評量報表](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)來評估要轉換的資料庫物件，並估計轉換時間。  
  
6.  [將 SAP ASE 資料庫架構轉換成 SQL Server/Azure SQL Database 架構](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [將轉換的資料庫物件載入 SQL Server/Azure SQL Database](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    請儲存腳本並在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 中執行，或同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server/Azure SQL Database](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 如有必要，請更新您的資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA for SAP ASE 的消費者入門 &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
