---
title: "執行預存程序 (OLE DB) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85703d6fdc0e68b8ea0a28989f8871a804a5ae5d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="stored-procedures---running"></a>預存程序-執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  執行陳述式時，在資料來源上呼叫預存程序 (而非直接在用戶端應用程式中執行或準備陳述式) 可以提供：  
  
-   較高的效能。  
  
-   降低的網路負擔。  
  
-   更好的一致性。  
  
-   更好的精確度。  
  
-   增加的功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援三種機制，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用來傳回資料的預存程序：  
  
-   程序中的每個 SELECT 陳述式都會產生一個結果集。  
  
-   程序可以透過輸出參數傳回資料。  
  
-   程序可以有一個整數的傳回碼。  
  
 應用程式必須能夠處理預存程序中的所有這些輸出。  
  
 不同的 OLE DB 提供者在結果處理期間，會在不同時間傳回輸出參數和傳回值。 如果是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者的輸出參數和傳回碼，才會提供取用者已經擷取或取消預存程序所傳回的結果集之後。 傳回碼和輸出參數會由來自伺服器的最後一個 TDS 封包傳回。  
  
 當它傳回輸出參數和傳回碼時，提供者會使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 屬性來報告。 這個屬性位於 DBPROPSET_DATASOURCEINFO 屬性集中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將 DBPROP_OUTPUTPARAMETERAVAILABILITY 屬性設定為 DBPROPVAL_OA_ATROWRELEASE，表示傳回碼和輸出參數不會傳回結果集是處理或釋出之前。  
  
## <a name="see-also"></a>請參閱  
 [預存程序](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
