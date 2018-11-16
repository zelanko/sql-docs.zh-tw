---
title: 將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96ade7125c0d03963e8e012ed72bdb8fdef492cf
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662347"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>將 SAP ASE 資料庫移轉至 SQL Server-Azure SQL Database (SybaseToSQL)
SQL Server Migration Assistant (SSMA) for SAP Adaptive Server Enterprise (ASE) 是完整的環境，可協助您快速 SAP ASE 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database。 藉由使用適用於 SAP ASE 的 SSMA，您可以檢閱資料庫物件和資料、 評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從 SAP ASE 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database，使用下列程序：  
  
1.  [建立新的 SSMA 專案](working-with-ssma-projects-sybasetosql.md)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。 如需有關自訂資料型別對應資訊，請參閱[對應 Sybase ASE 和 SQL Server 資料類型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [連接到 SAP ASE 資料庫伺服器](connecting-to-sybase-ase-sybasetosql.md)。  
  
3.  [連接到 SQL Server 執行個體](connecting-to-sql-server-sybasetosql.md)或是[連接到 Azure SQL Database 的執行個體](connecting-to-azure-sql-db-sybasetosql.md)。  
  
4.  [SAP ASE 資料庫結構描述對應到 SQL Server / Azure SQL Database 資料庫結構描述](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （選擇性）[建立評定報表](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)評估進行轉換的資料庫物件，並且估計的轉換時間。  
  
6.  [將 SAP ASE 資料庫結構描述轉換成 SQL Server / Azure SQL Database 結構描述](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [已轉換的資料庫物件載入 SQL Server / Azure SQL Database](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    請儲存指令碼，並在執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database，或同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server / Azure SQL Database](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 如有必要，請更新您的資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[開始使用 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
