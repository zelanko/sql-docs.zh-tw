---
title: FILESTREAM 支援 (OLE DB) |Microsoft 文件
description: FILESTREAM 支援 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbe3ce15444b0c6556cf3cef0267e99bb55657f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/11/2018
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支援 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  開頭為[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和 OLE DB 驅動程式會針對 SQL Server OLE DB 支援增強型的 FILESTREAM 功能。 如需有關這項功能的詳細資訊，請參閱[FILESTREAM 支援](../../oledb/features/filestream-support.md)。 如需範例，請參閱[Filestream 和 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 傳送和接收**varbinary （max)** 值大於 2 GB，應用程式使用**DBTYPE_IUNKNOWN**參數和結果繫結中。 參數提供者必須呼叫 iunknown:: Queryinterface ISequentialStream 與傳回 ISequentialStream 的結果。  
  
 OLE db，請檢查相關的 ISequentialStream 值將會放寬。 當*wType*是**DBTYPE_IUNKNOWN**中**DBBINDING**結構長度檢查可以藉由略過停用**DBPART_LENGTH**從*dwPart*或設定資料的長度 (位移*obLength*資料緩衝區中) 以 ~ 0。 在此情況下，提供者將不會檢查值的長度，而且將會透過資料流要求並傳回所有可用的資料。 這項變更將會套用到所有大型物件 (LOB) 類型與 XML，但是只會在連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 伺服器時才會套用。 這將會提供開發人員更大的彈性，同時維持現有應用程式與下層伺服器的一致性與回溯相容性。  
  
 這項變更會影響資料，主要是 irowset:: Getdata、 icommand:: Execute 和 irowsetfastload:: Insertrow 傳送的所有介面。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
