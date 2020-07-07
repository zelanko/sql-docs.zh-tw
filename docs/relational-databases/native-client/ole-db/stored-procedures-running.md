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
ms.openlocfilehash: 2c86490f0a33ba1582ebebb3a9c1da78553098ff
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012010"
---
# <a name="stored-procedures---running"></a>預存程序 - 執行
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  執行陳述式時，在資料來源上呼叫預存程序 (而非直接在用戶端應用程式中執行或準備陳述式) 可以提供：  
  
-   較高的效能。  
  
-   降低的網路負擔。  
  
-   更好的一致性。  
  
-   更好的精確度。  
  
-   增加的功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預存程式用來傳回資料的三種機制：  
  
-   程序中的每個 SELECT 陳述式都會產生一個結果集。  
  
-   程序可以透過輸出參數傳回資料。  
  
-   程序可以有一個整數的傳回碼。  
  
 應用程式必須能夠處理預存程序中的所有這些輸出。  
  
 不同的 OLE DB 提供者在結果處理期間，會在不同時間傳回輸出參數和傳回值。 如果是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，在取用者抓取或取消預存程式所傳回的結果集之前，不會提供輸出參數和傳回碼。 傳回碼和輸出參數會由來自伺服器的最後一個 TDS 封包傳回。  
  
 當它傳回輸出參數和傳回碼時，提供者會使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 屬性來報告。 這個屬性位於 DBPROPSET_DATASOURCEINFO 屬性集中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會將 DBPROP_OUTPUTPARAMETERAVAILABILITY 屬性設定為 DBPROPVAL_OA_ATROWRELEASE，以指出在處理或釋放結果集之前，不會傳回傳回碼和輸出參數。  
  
## <a name="see-also"></a>另請參閱  
 [預存程式](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
