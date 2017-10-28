---
title: "Sybase (SybaseToSQL) 的 SQL Server 移轉小幫手 |Microsoft 文件"
ms.custom: 
ms.date: 08/14/2017
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
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 5316f9d560f7e15bb0699780f67aff641067b203
ms.openlocfilehash: 7ca9cad19b0a6e9eadb4c369eb6405298a31ac6b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/15/2017

---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase (SybaseToSQL) 的 SQL Server 移轉小幫手
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 (SSMA) 的 Sybase Adaptive Server Enterprise (ASE) 是一個工具，將 ASE 資料庫移轉至[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年或[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年或[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年或[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年或[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016年或[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 上 Windows 和 Linux （預覽） 或[!INCLUDE[msCoName](../../includes/msconame_md.md)]Azure SQL DB。 SSMA for Sybase 轉換 ASE 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件，會建立這些物件中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 中，然後再移轉資料至 ASE 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL。  
  
這份文件會為您介紹 SSMA for Sybase 並提供逐步指示 ASE 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和移轉之後可能會發生問題的相關資訊。 若要進一步了解，請參閱下列主題。  
  
## <a name="contents"></a>目錄  
  
|章節|Description|  
|-----------|---------------|  
|[SSMA for Sybase &#40; 在最新消息SybaseToSQL &#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|列出 SSMA 版本所做的變更。|  
|[安裝 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|包含的主題將提供的必要條件和安裝的 SSMA for Sybase 用戶端和必要的元件正在執行的電腦上的指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體。|  
|[開始使用 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|導入的使用者介面、 專案和組態選項。|  
|[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|提供轉換程序和程序中的每個步驟的詳細的資訊的概觀。|  
|[使用者介面參考 &#40;SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|包含 SSMA for Sybase 對話方塊文件。|  
|[使用 SSMA for Sybase 主控台](http://msdn.microsoft.com/c465e477-c479-4aa8-918d-58bf30884789)|包含 SSMA 主控台應用程式的文件。|  
|[取得 SSMA for Sybase 協助](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供取得其他協助的相關資訊。|  
  

