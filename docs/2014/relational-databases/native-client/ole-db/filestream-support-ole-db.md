---
title: FILESTREAM 支援 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
ms.openlocfilehash: 925c624139e64b5d3aeb371e5eaf70b0fa1da171
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416957"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支援 (OLE DB)
  開頭[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，OLE DB 支援增強型的 FILESTREAM 功能。 如需這項功能的詳細資訊，請參閱[FILESTREAM 支援](../features/filestream-support.md)。 如需範例，請參閱[Filestream 和 OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 若要傳送與接收大於 2 GB 的 `varbinary(max)` 值，應用程式會在參數和結果繫結中使用 `DBTYPE_IUNKNOWN`。 參數提供者必須呼叫 iunknown:: Queryinterface ISequentialStream 以及傳回 ISequentialStream 的結果。  
  
 對於 OLE DB 中，檢查相關 ISequentialStream 值將會放寬。 當*wType*是`DBTYPE_IUNKNOWN`中`DBBINDING`結構長度檢查可以藉由省略停用`DBPART_LENGTH`從*dwPart*或藉由設定資料的長度 （位移*obLength*資料緩衝區中) 至 ~ 0。 在此情況下，提供者將不會檢查值的長度，而且將會透過資料流要求並傳回所有可用的資料。 這項變更將會套用到所有大型物件 (LOB) 類型與 XML，但是只會在連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 伺服器時才會套用。 這將會提供開發人員更大的彈性，同時維持現有應用程式與下層伺服器的一致性與回溯相容性。  
  
 這項變更會影響所有傳輸資料，主要是 irowset:: Getdata、 icommand:: Execute 和 irowsetfastload:: Insertrow 的介面。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../sql-server-native-client-programming.md)  
  
  
