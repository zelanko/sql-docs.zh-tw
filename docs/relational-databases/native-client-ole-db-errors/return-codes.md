---
title: '傳回碼 (Native Client OLE DB 提供者) '
description: 瞭解 SQL Server Native Client OLE DB 所支援的傳回碼，包括常見的 DB_S_ERRORSOCCURRED HRESULT 值。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2644a34817c4319dff877a162963b2525d259cae
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869298"
---
# <a name="return-codes-native-client-ole-db-provider"></a>傳回碼 (Native Client OLE DB 提供者) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在大部分的基本層級，成員函數不是成功就是失敗。 在更精確一點的層級，函數可能會成功，但是其成功可能不是應用程式開發人員所樂見的。  
  
 如需 OLE DB 傳回碼的詳細資訊，請參閱 [Return Codes (OLE DB)](/previous-versions/windows/desktop/ms725451(v=vs.85)) (傳回碼 (OLE DB))。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider 成員函式傳回 S_OK 時，函數會成功。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider 成員函式未傳回 S_OK 時，OLE/COM HRESULT 解壓縮失敗，而且 IS_ERROR 宏可以判斷函式的整體成功或失敗。  
  
 如果 FAILED 或 IS_ERROR 傳回 TRUE，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者取用者可確保成員函式執行失敗。 當 FAILED 或 IS_ERROR 傳回 FALSE，而且 HRESULT 不等於 S_OK 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider 取用者可確保函數在某種意義上成功。 取用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者錯誤介面中，取得這個「資訊成功」的詳細資訊。 此外，如果函式清楚地失敗 (失敗的宏會傳回 TRUE) ，則可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者錯誤介面取得擴充的錯誤資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者取用者通常會遇到「資訊成功」 HRESULT 的 DB_S_ERRORSOCCURRED。 傳回 DB_S_ERRORSOCCURRED 的成員函數通常會定義一或多個可提供狀態值給取用者的參數。 取用者無法取得在狀態值參數中傳回之錯誤資訊以外的錯誤資訊，因此取用者應該在可取得錯誤資訊時，實作應用程式邏輯來擷取狀態值。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者成員函式不會傳回成功的程式碼 S_FALSE。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者成員函式一律會傳回 S_OK 以表示成功。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
