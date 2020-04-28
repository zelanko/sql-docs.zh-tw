---
title: SQL Server 移轉小幫手 for DB2 （DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 62b4910d6073da7ec845cc5e754a4e005f5d1461
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72252162"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>適用于 DB2 的 SQL Server 移轉小幫手（DB2ToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手（SSMA） for db2 是一種工具，可將 db2 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫移轉[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至 2012 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2014 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2016、windows 和 linux [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的2017、windows 和 linux 上的2019，或 Azure SQL Database。 SSMA for DB2 會將 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]轉換成資料庫物件，在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立這些物件，然後將資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 遷移至或 Azure SQL Database。  
  
本檔將介紹如何 SSMA for DB2，並提供將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的逐步指示。 下表顯示可協助您深入瞭解的文章：  
  
## <a name="contents"></a>內容  
  
|區段|描述|  
|-----------|---------------|
|[SSMA for DB2 的新功能](https://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|這個版本的 SSMA for DB2 的新功能|  
|[安裝 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含的文章會提供必要條件，以及在執行的電腦上安裝 SSMA for DB2 用戶端和必要元件的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指示。|  
|[消費者入門與 DB2 &#40;DB2ToSQL 的 SSMA&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[&#40;DB2ToSQL&#41;的使用者介面參考](../../ssma/db2/user-interface-reference-db2tosql.md)|包含 SSMA for DB2 對話方塊的檔。|  
|[使用 SSMA for DB2 主控台](https://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含 SSMA 主控台應用程式的檔|  
|[取得 DB2 協助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
