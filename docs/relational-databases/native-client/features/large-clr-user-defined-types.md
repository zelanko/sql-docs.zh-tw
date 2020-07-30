---
title: 大型 CLR 使用者定義型別 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 78928140c3aed95662535410501622e9554fc2d0
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245765"
---
# <a name="large-clr-user-defined-types-in-sql-server-native-client"></a>SQL Server Native Client 中的大型 CLR 使用者自訂類型
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在 SQL Server 2005，Common Language Runtime (CLR) 中的使用者定義型別 (UDT) 在大小上限制為 8,000 個位元組。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更新版本中已提高此限制。 CLR UDT 現在會以大型物件 (LOB) 類型類似的方式處理。 也就是說，小於或等於 8,000 個位元組的 UDT 行為與 SQL Server 2005 相同，但是支援較大的 UDT，而且會將其大小報告為「無限制」。  
  
 如需詳細資訊，請參閱[大型 Clr 使用者自訂類型 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)和[大型 Clr 使用者定義類型 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="use-cases"></a>使用案例  
 對於 ODBC，大型 UDT 的支援包括能夠以片段當做資料執行中 (data-at-execution) 參數傳送 UDT 值。 這項作業是使用 SQLPutData 來完成。  
  
 對於 OLE DB，大型 UDT 的支援包括能夠使用 ISequentialStream 繫結，在伺服器來回串流 UDT 值。  
  
 小於或等於 8,000 個位元組的 UDT 行為如同在 SQL Server 2005 中的行為。 對於 OLE DB，您仍然可以使用 ISequentialStream 繫結來串流處理小型 UDT。  
  
 原生程式碼有時候必須了解 CLR UDT 的內容，但不必具現化 Managed 物件。 如果是這種情況，您可以使用自訂序列化，將伺服器上的 UDT 值轉換為用戶端熟知的格式。  
  
 對於擁有現有資料存取程式碼的應用程式，您可以透過原生 API 擷取 UDT，並使用混合模式應用程式中的 C++ CLI Interop 進行具現化，藉以利用用戶端上的 CLR UDT 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
