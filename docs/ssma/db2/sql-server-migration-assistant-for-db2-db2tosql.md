---
title: DB2 的 SQL Server 移轉小幫手 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
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
ms.openlocfilehash: b01bdfccc9ba67bedc350e67af95bf9345a2e52b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985660"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 的 SQL Server 移轉小幫手 (DB2ToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) for DB2 會將 DB2 資料庫移轉至的工具[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 年[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上 Windows 和 Linux （2017年預覽狀態），或 Azure SQL DB。 SSMA for DB2 會將轉換至 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件，會建立在這些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然後將資料從 DB2，以便移轉和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
這份文件為您介紹 SSMA for DB2，並提供逐步指示，將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 下表顯示可協助您了解更多主題：  
  
## <a name="contents"></a>目錄  
  
|章節|描述|  
|-----------|---------------|  
|[SSMA for DB2 的新功能](http://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|在這個版本的 SSMA for DB2 中最新消息|  
|[安裝 SSMA for DB2 用戶端&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含的主題會提供先決條件與指示正在執行的電腦上安裝 SSMA for DB2 用戶端和必要的元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[開始使用 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|導入的使用者介面、 專案和組態選項。|  
|[移轉的 DB2 資料庫到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|提供轉換程序和程序中的每個步驟的詳細的資訊的概觀。|  
|[使用者介面參考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)|包含文件 SSMA for DB2 的對話方塊。|  
|[使用 SSMA for DB2 主控台](http://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含在 SSMA 主控台應用程式上的文件|  
|[取得 SSMA for DB2 的協助](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供取得其他協助的相關資訊。|  
  
