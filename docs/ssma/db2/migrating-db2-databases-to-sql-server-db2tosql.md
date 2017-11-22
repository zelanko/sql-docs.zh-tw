---
title: "移轉的 DB2 資料庫到 SQL Server (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 17531f8b6b7dab8e5afe75203f73e946c46129af
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>DB2 資料庫移轉至 SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 (SSMA) for DB2 是一個完整的環境，可協助您快速 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 利用 SSMA for DB2，檢閱資料庫物件和資料，評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、，然後將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 請注意您無法移轉 SYS 和系統 DB2 結構描述。  
  
## <a name="recommended-migration-process"></a>建議您移轉程序  
若要成功移轉物件和資料，從 DB2 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，請使用下列程序：  
  
1.  [新的 SSMA 專案](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[專案設定 &#40;轉換 &#41;&#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)和相關的區段。 如需如何自訂資料型別對應資訊，請參閱[對應 DB2 與 SQL Server 資料類型 &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
2.  [連接到 DB2 資料庫](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)。  
  
3.  [連接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
4.  [DB2 結構描述對應到 SQL Server 結構描述](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)。  
  
5.  （選擇性）[評估報告](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de)以評估資料庫物件的轉換，並評估的轉換時間。  
  
6.  [將 DB2 結構描述轉換](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0)。  
  
7.  [轉換的資料庫物件載入 SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)。  
  
    您可以下列方式之一：  
  
    -   儲存指令碼，執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步處理資料庫物件。  
  
8.  [將 DB2 資料移轉至 SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)。  
  
9. 如有必要，更新資料庫的應用程式。  
  
## <a name="see-also"></a>請參閱＜  
[SSMA 安裝 DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[SSMA for 入門 DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
