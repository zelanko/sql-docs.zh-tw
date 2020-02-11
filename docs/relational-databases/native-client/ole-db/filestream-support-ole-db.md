---
title: FILESTREAM 支援（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff05424d9b8726f21c8c4aa2facd42b87961cc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73760873"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支援 (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  從[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 開始，OLE DB 支援增強型 FILESTREAM 功能。 如需這項功能的詳細資訊，請參閱[FILESTREAM 支援](../../../relational-databases/native-client/features/filestream-support.md)。 如需範例，請參閱[Filestream 和 OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 若要傳送和接收大於 2 GB 的**Varbinary （max）** 值，應用程式會使用參數和結果系結中的**DBTYPE_IUNKNOWN** 。 針對參數，提供者必須針對 ISequentialStream 呼叫 IUnknown：： QueryInterface，並針對傳回 ISequentialStream 的結果。  
  
 針對 OLE DB，將會放寬與 ISequentialStream 值相關的檢查。 當*wType*在**DBBINDING**結構中**DBTYPE_IUNKNOWN**時，可以藉由省略來自*dwPart*的**DBPART_LENGTH** ，或將資料的長度（在資料緩衝區中的位移*obLength* ）設定為 ~ 0，來停用長度檢查。 在此情況下，提供者將不會檢查值的長度，而且將會透過資料流要求並傳回所有可用的資料。 這項變更將會套用到所有大型物件 (LOB) 類型與 XML，但是只會在連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 伺服器時才會套用。 這將會提供開發人員更大的彈性，同時維持現有應用程式與下層伺服器的一致性與回溯相容性。  
  
 這種變更會影響所有傳輸資料的介面，主要是 IRowset：： ICommand：： Execute 和 IRowsetFastLoad：： InsertRow。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
