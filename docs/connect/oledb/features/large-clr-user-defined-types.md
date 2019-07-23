---
title: 大型 CLR 使用者定義類型 |Microsoft Docs
description: SQL Server OLE DB 驅動程式中的大型 CLR 使用者定義類型
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: acbdd170808ed9f6d7f67265a4e0d18f3b9e8eb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989075"
---
# <a name="large-clr-user-defined-types"></a>大型 CLR 使用者定義型別
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在 SQL Server 2005，Common Language Runtime (CLR) 中的使用者定義型別 (UDT) 在大小上限制為 8,000 個位元組。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更新版本中已提高此限制。 CLR UDT 現在會以大型物件 (LOB) 類型類似的方式處理。 也就是說，小於或等於 8,000 個位元組的 UDT 行為與 SQL Server 2005 相同，但是支援較大的 UDT，而且會將其大小報告為「無限制」。  
  
 如需詳細資訊, 請參閱[OLE DB&#41;的大型 CLR &#40;使用者定義類型](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md)。  
  
## <a name="use-cases"></a>使用案例   
  
 對於 OLE DB，大型 UDT 的支援包括能夠使用 ISequentialStream 繫結，在伺服器來回串流 UDT 值。  
  
 小於或等於 8,000 個位元組的 UDT 行為如同在 SQL Server 2005 中的行為。 對於 OLE DB, 您仍然可以使用 ISequentialStream 系結來串流小型的 Udt。  
  
 原生程式碼有時候必須了解 CLR UDT 的內容，但不必具現化 Managed 物件。 如果是這種情況，您可以使用自訂序列化，將伺服器上的 UDT 值轉換為用戶端熟知的格式。  
  
 對於擁有現有資料存取程式碼的應用程式，您可以透過原生 API 擷取 UDT，並使用混合模式應用程式中的 C++ CLI Interop 進行具現化，藉以利用用戶端上的 CLR UDT 行為。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
