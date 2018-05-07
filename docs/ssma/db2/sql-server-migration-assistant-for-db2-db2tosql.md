---
title: DB2 的 SQL Server 移轉小幫手 (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 08/09/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 12e96334e19d6991ad9d80d1b0af51797fefc6f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 的 SQL Server 移轉小幫手 (DB2ToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) for DB2 是一個工具，將 DB2 資料庫移轉至[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016， [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 上 （Windows 和 Linux預覽） 或 Azure SQL DB。 SSMA for DB2 將轉換至 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件，會建立這些物件中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然後再移轉資料的 DB2 至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
這份文件會為您介紹 SSMA for DB2，並提供逐步指示，將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 下表顯示可協助您進一步了解主題：  
  
## <a name="contents"></a>目錄  
  
|章節|Description|  
|-----------|---------------|  
|[SSMA for DB2 的新功能](http://msdn.microsoft.com/en-us/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|在這一版的 SSMA for DB2 中最新消息|  
|[DB2 用戶端安裝 SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含的主題將提供的必要條件和安裝的 SSMA for DB2 用戶端和必要的元件正在執行的電腦上的指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[SSMA for 入門 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|導入的使用者介面、 專案和組態選項。|  
|[SQL server 資料庫移轉 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|提供轉換程序和程序中的每個步驟的詳細的資訊的概觀。|  
|[使用者介面參考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)|包含 DB2 對話方塊 SSMA 文件。|  
|[使用 SSMA for DB2 主控台](http://msdn.microsoft.com/en-us/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含 SSMA 主控台應用程式的文件|  
|[取得 SSMA 協助 DB2](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供取得其他協助的相關資訊。|  
  
