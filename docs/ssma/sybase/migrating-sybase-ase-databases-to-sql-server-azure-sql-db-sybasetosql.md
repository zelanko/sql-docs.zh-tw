---
title: 將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft 文件
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8c097aa322f7ffe68f7cb886119162c2fc56d14f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>SAP ASE 資料庫移轉到 SQL Server-Azure SQL Database (SybaseToSQL)
SQL Server 移轉小幫手 (SSMA) 的 SAP Adaptive Server Enterprise (ASE) 是一種完整的環境，可協助您快速 SAP ASE 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database。 藉由使用 SAP ASE SSMA，檢閱資料庫物件和資料，評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從 SAP ASE 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database，使用下列程序：  
  
1.  [建立新的 SSMA 專案](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。 如需自訂資料型別對應資訊，請參閱[對應 Sybase ASE 和 SQL Server 資料型別&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [連接到 SAP ASE 資料庫伺服器](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614)。  
  
3.  [連接到 SQL Server 執行個體](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)或[連接到 Azure SQL Database 的執行個體](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)。  
  
4.  [SAP ASE 資料庫結構描述對應到 SQL Server / Azure SQL Database 的資料庫結構描述](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （選擇性）[建立的評估報告](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)以評估資料庫物件的轉換，並評估的轉換時間。  
  
6.  [將 SAP ASE 資料庫結構描述轉換成 SQL Server / Azure SQL Database 的結構描述](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [轉換的資料庫物件載入 SQL Server / Azure SQL Database](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    請儲存指令碼，並執行它[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL Database，或同步處理資料庫物件。  
  
8.  [將資料移轉到 SQL Server / Azure SQL Database](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 必要時，更新您的資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[SSMA 安裝 SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA for 入門 SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
