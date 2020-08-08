---
title: 適用于 MySQL 的 SQL Server 移轉小幫手 (MySQLToSQL) |Microsoft Docs
description: 瞭解適用于 MySQL 的 SSMA，並遵循將 MySQL 資料庫遷移至 SQL Server 或 Azure SQL Database 的逐步指示。
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2793bc33-38d3-46ed-8277-b8580cf78ced
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 294c91e0d1fa62c548bc88c834e292ab34ec0015
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935157"
---
# <a name="sql-server-migration-assistant-for-mysql-mysqltosql"></a>適用于 MySQL 的 SQL Server 移轉小幫手 (MySQLToSQL) 

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]適用于 MySQL 的移轉小幫手 (SSMA) 是一種工具，可將 MySQL 資料庫遷移至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2017、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2019，或 Azure [!INCLUDE[msCoName](../../includes/msconame_md.md)] 資料庫。 適用于 MySQL 的 SSMA 會將 MySQL 資料庫物件轉換成 SQL Server 資料庫物件、在中建立這些物件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 然後將資料從 MySQL 遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
本檔將為您介紹 SSMA for MySQL，並提供將 MySQL 資料庫遷移至的逐步指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 下表顯示可協助您深入瞭解的文章：  
  
## <a name="contents"></a>目錄  
  
|區段|描述|
|-----------|---------------|
|[SSMA for MySQL 的新功能](https://msdn.microsoft.com/1451a0b0-6713-4d0c-954f-ea3d8fce1d31)|這一版的 SSMA for MySQL 的新功能|  
|[安裝 SSMA for MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)|包含的文章會提供必要條件和指示，說明如何在執行 SQL Server 的電腦上安裝 SSMA for MySQL 用戶端和必要元件。|  
|[適用于 MySQL 的 SSMA &#40;MySQLToSQL&#41;的消費者入門](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[&#40;MySQLToSQL&#41;的使用者介面參考](../../ssma/mysql/user-interface-reference-mysqltosql.md)|包含 [適用于 MySQL 的 SSMA] 對話方塊的檔。|  
|[使用 SSMA for MySQL 主控台](working-with-ssma-for-mysql-console-mysqltosql.md)|包含 SSMA 主控台應用程式的檔|  
|[取得 MySQL 的 SSMA 協助](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
