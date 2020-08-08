---
title: DB2 (DB2ToSQL) 的 SQL Server 移轉小幫手 |Microsoft Docs
description: 瞭解 SSMA for DB2，並遵循將 DB2 資料庫移轉至 SQL Server 或 Azure SQL Database 的逐步指示。
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 6ade3ce31bed08bdb7b25b09ec0d5bbcf91405f1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936477"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 (DB2ToSQL 的 SQL Server 移轉小幫手) 
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 (SSMA) FOR db2 是用來將 db2 資料庫移轉至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的工具2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2017、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2019，或 Azure SQL Database。 SSMA for DB2 會將 DB2 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件，在中建立這些物件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 然後將資料從 DB2 遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。  
  
本檔將介紹如何 SSMA for DB2，並提供將 DB2 資料庫移轉至的逐步指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 下表顯示可協助您深入瞭解的文章：  
  
## <a name="contents"></a>目錄  
  
|區段|描述|  
|-----------|---------------|
|[SSMA for DB2 的新功能](https://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|這個版本的 SSMA for DB2 的新功能|  
|[安裝 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含的文章會提供必要條件，以及在執行的電腦上安裝 SSMA for DB2 用戶端和必要元件的指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[消費者入門與 DB2 &#40;DB2ToSQL 的 SSMA&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[&#40;DB2ToSQL&#41;的使用者介面參考](../../ssma/db2/user-interface-reference-db2tosql.md)|包含 SSMA for DB2 對話方塊的檔。|  
|[使用 SSMA for DB2 主控台](https://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含 SSMA 主控台應用程式的檔|  
|[取得 DB2 協助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
