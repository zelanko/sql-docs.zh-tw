---
title: FILESTREAM 支援 (OLE DB) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a21d4b69d475c346a6e08f72f23ad361d6756242
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支援 (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  開頭為[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0、 OLE DB 支援增強型的 FILESTREAM 功能。 如需有關這項功能的詳細資訊，請參閱[FILESTREAM 支援](../../../relational-databases/native-client/features/filestream-support.md)。 如需範例，請參閱[Filestream 和 OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 傳送和接收**varbinary （max)**值大於 2 GB，應用程式使用**DBTYPE_IUNKNOWN**參數和結果繫結中。 參數提供者必須呼叫 iunknown:: Queryinterface ISequentialStream 與傳回 ISequentialStream 的結果。  
  
 OLE db，請檢查相關的 ISequentialStream 值將會放寬。 當*wType*是**DBTYPE_IUNKNOWN**中**DBBINDING**結構長度檢查可以藉由略過停用**DBPART_LENGTH**從*dwPart*或設定資料的長度 (位移*obLength*資料緩衝區中) 以 ~ 0。 在此情況下，提供者將不會檢查值的長度，而且將會透過資料流要求並傳回所有可用的資料。 這項變更將會套用到所有大型物件 (LOB) 類型與 XML，但是只會在連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 伺服器時才會套用。 這將會提供開發人員更大的彈性，同時維持現有應用程式與下層伺服器的一致性與回溯相容性。  
  
 這項變更會影響資料，主要是 irowset:: Getdata、 icommand:: Execute 和 irowsetfastload:: Insertrow 傳送的所有介面。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
