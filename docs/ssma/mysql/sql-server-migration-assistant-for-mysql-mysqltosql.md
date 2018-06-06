---
title: MySQL (MySQLToSQL) 的 SQL Server 移轉小幫手 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
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
ms.assetid: 2793bc33-38d3-46ed-8277-b8580cf78ced
caps.latest.revision: 13
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 37dad40566af3492be7ab288711a6aeb22bed0ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-migration-assistant-for-mysql-mysqltosql"></a>MySQL (MySQLToSQL) 的 SQL Server 移轉小幫手
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) 的 MySQL 是一個工具，將 MySQL 資料庫移轉至[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 上 Windows 和 Linux （預覽） / Azure [!INCLUDE[msCoName](../../includes/msconame_md.md)] DB。 SSMA for MySQL 將 MySQL 資料庫物件轉換成 SQL Server 資料庫物件，會建立這些物件中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然後再移轉資料從 MySQL 至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
這份文件會為您介紹 SSMA for MySQL，並提供逐步指示，將 MySQL 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 下表顯示可協助您進一步了解主題：  
  
## <a name="contents"></a>目錄  
  
|||  
|-|-|  
|**區段**|**說明**|  
|[SSMA for MySQL 中最新消息](http://msdn.microsoft.com/en-us/1451a0b0-6713-4d0c-954f-ea3d8fce1d31)|在這一版的 SSMA for MySQL 最新消息|  
|[安裝 SSMA for MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)|包含提供先決條件與指示的 SSMA for MySQL 用戶端和必要的元件安裝在執行 SQL Server 的電腦上的主題。|  
|[開始使用 SSMA for MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)|導入的使用者介面、 專案和組態選項。|  
|[移轉的 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)|提供轉換程序和程序中的每個步驟的詳細的資訊的概觀。|  
|[使用者介面參考&#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)|包含 SSMA for MySQL 對話方塊文件。|  
|[使用 SSMA for MySQL 主控台](http://msdn.microsoft.com/en-us/240aaad1-d65d-4dea-b60b-315cb1ac733d)|包含 SSMA 主控台應用程式的文件|  
|[取得 SSMA for MySQL 協助](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供取得其他協助的相關資訊。|  
  
