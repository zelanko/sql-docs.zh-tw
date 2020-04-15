---
title: 執行預存程序 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f01c5e43d7d451cbcdca30dd66cf2ca70227541
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305330"
---
# <a name="stored-procedures---running"></a>預存程序 - 執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  執行陳述式時，在資料來源上呼叫預存程序 (而非直接在用戶端應用程式中執行或準備陳述式) 可以提供：  
  
-   較高的效能。  
  
-   降低的網路負擔。  
  
-   更好的一致性。  
  
-   更好的精確度。  
  
-   增加的功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機客戶端 OLE 資料庫[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]提供者支援 儲存程序用於傳回資料的三種機制:  
  
-   程序中的每個 SELECT 陳述式都會產生一個結果集。  
  
-   程序可以透過輸出參數傳回資料。  
  
-   程序可以有一個整數的傳回碼。  
  
 應用程式必須能夠處理預存程序中的所有這些輸出。  
  
 不同的 OLE DB 提供者在結果處理期間，會在不同時間傳回輸出參數和傳回值。 對於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式,在消費者檢索或取消儲存過程返回的結果集之前,不會提供輸出參數和返回代碼。 傳回碼和輸出參數會由來自伺服器的最後一個 TDS 封包傳回。  
  
 當它傳回輸出參數和傳回碼時，提供者會使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 屬性來報告。 這個屬性位於 DBPROPSET_DATASOURCEINFO 屬性集中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式將DBPROP_OUTPUTPARAMETERAVAILABILITY屬性設置為DBPROPVAL_OA_ATROWRELEASE,以指示在處理或釋放結果集之前不會返回返回代碼和輸出參數。  
  
## <a name="see-also"></a>另請參閱  
 [預存程序](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
