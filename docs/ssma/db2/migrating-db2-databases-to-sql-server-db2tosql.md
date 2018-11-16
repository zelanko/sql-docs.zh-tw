---
title: 移轉的 DB2 資料庫到 SQL Server (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8ee6e9cca2e16a180f869df7bcec07bb7b09e390
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51658407"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>將 DB2 資料庫移轉至 SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) for DB2 是完整的環境，可協助您快速地移轉到 DB2 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 使用 SSMA for DB2 中，檢閱資料庫物件和資料、 評估要移轉的資料庫、 將資料庫物件，來移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，然後移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 請注意您無法將 SYS 和系統 DB2 結構描述移轉。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從 DB2 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，使用下列程序：  
  
1.  [新的 SSMA 專案](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[專案設定&#40;轉換&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md)和相關的區段。 如需如何自訂資料型別對應資訊，請參閱[對應 DB2 和 SQL Server 資料類型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
2.  [連接到 DB2 資料庫](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)。  
  
3.  [連接到 SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
4.  [DB2 結構描述對應到 SQL Server 結構描述](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)。  
  
5.  （選擇性）[評估報告](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de)評估進行轉換的資料庫物件，並且估計的轉換時間。  
  
6.  [將 DB2 結構描述轉換](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0)。  
  
7.  [已轉換的資料庫物件載入 SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)。  
  
    您可以透過下列方式之一來這麼做：  
  
    -   儲存指令碼，並在執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   同步處理資料庫物件。  
  
8.  [將 DB2 資料移轉至 SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b)。  
  
9. 如有必要，更新資料庫的應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[開始使用 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
