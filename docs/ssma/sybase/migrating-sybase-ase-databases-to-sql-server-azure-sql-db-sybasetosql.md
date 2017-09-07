---
title: "將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63dc9188d93def41a5116386f93bf29e3b744e8e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-databases-to-sql-server---azure-sql-db-sybasetosql"></a>Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB (SybaseToSQL)
SQL Server 移轉小幫手 (SSMA) for Sybase 是完整的環境，可協助您快速 Sybase Adaptive Server Enterprise (ASE) 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 利用 SSMA for Sybase，檢閱資料庫物件和資料，評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、，然後將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
## <a name="recommended-migration-process"></a>建議您移轉程序  
若要成功移轉物件和資料，從 ASE 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，請使用下列程序：  
  
1.  [建立新的 SSMA 專案](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項 &#40;SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). 如需自訂資料型別對應資訊，請參閱[對應 Sybase ASE 和 SQL Server 資料類型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [連接到 Sybase ASE 資料庫伺服器](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614)。  
  
3.  [連接到 SQL Server 執行個體](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)或[連接到 Azure SQL DB 的執行個體](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)。  
  
4.  [ASE 資料庫結構描述對應到 SQL Server / Azure SQL DB 資料庫結構描述](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （選擇性）[建立的評估報告](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)以評估資料庫物件的轉換，並評估的轉換時間。  
  
6.  [將 Sybase ASE 資料庫結構描述轉換成 SQL Server / Azure SQL DB 結構描述](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [轉換的資料庫物件載入 SQL Server / Azure SQL DB](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    您可以透過其中一種儲存指令碼並執行它[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、 或者您可以同步處理資料庫物件。  
  
8.  [將資料移轉到 SQL Server / Azure SQL DB](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 必要時，更新您的資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[開始使用 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

