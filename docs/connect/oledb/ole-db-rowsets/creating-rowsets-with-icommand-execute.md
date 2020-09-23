---
title: 使用 ICommand::Execute 建立資料列集 (OLE DB 驅動程式) | Microsoft Docs
description: 了解如何使用 OLE DB Driver for SQL Server 中的 ICommand::Execute 建立資料列集。 您在資料列集中所需的屬性可以限制命令文字。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
- Execute method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a6ca010dc702471ceb932119d30ab97d249b2bf
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862250"
---
# <a name="creating-rowsets-with-icommandexecute"></a>使用 ICommand:: Execute 建立資料列集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  對於使用 **ICommand::Execute** 方法建立的資料列集，您希望存在於所產生之資料列集中的屬性可以限制命令的文字。 這對於支援動態命令文字的取用者而言，特別重要。  
  
 OLE DB Driver for SQL Server 無法使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標支援許多命令所產生的多個資料列集結果。 如果取用者要求需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標支援的資料列集，當命令文字產生多個單一資料列集做為其結果時，會發生錯誤。 如需詳細資訊，請參閱[產生多個資料列集結果的命令](../../oledb/ole-db-commands/commands-generating-multiple-rowset-results.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標支援可捲動的 OLE DB Driver for SQL Server 資料列集。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會針對受其他資料庫使用者所進行之變更影響的資料指標，強制施行限制。 特別是，某些資料指標中的資料列無法進行排序，而且嘗試使用包含 SQL ORDER BY 子句的命令建立資料列集可能會失敗。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
