---
title: 傳回碼 | Microsoft Docs
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
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301015"
---
# <a name="return-codes"></a>傳回碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在大部分的基本層級，成員函數不是成功就是失敗。 在更精確一點的層級，函數可能會成功，但是其成功可能不是應用程式開發人員所樂見的。  
  
 如需 OLE DB 傳回碼的詳細資訊，請參閱 [Return Codes (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631) (傳回碼 (OLE DB))。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式成員函數返回S_OK時,該函數成功。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式成員函數不返回S_OK時,OLE/COM HRESULT 解包失敗和IS_ERROR宏可以確定函數的總體成功或失敗。  
  
 如果"失敗"或"IS_ERROR返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]TRUE,則本機用戶端 OLE DB 提供程式使用者將確保成員函數執行失敗。 當 FAILED 或 IS_ERROR返回 FALSE 且 HRESULT[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不等於S_OK時,本機用戶端 OLE DB 提供程式消費者可以確信該函數在某種程度上成功。 消費者可以從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式錯誤介面檢索有關此"成功資訊"返回的詳細資訊。 此外,在函數明顯失敗的情況下(FAILED 宏返回 TRUE),從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端OLE DB提供程式錯誤介面中提供了擴展的錯誤資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式消費者通常遇到DB_S_ERRORSOCCURRED「成功與資訊」HRESULT 返回。 傳回 DB_S_ERRORSOCCURRED 的成員函數通常會定義一或多個可提供狀態值給取用者的參數。 取用者無法取得在狀態值參數中傳回之錯誤資訊以外的錯誤資訊，因此取用者應該在可取得錯誤資訊時，實作應用程式邏輯來擷取狀態值。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE DB 提供程式成員函數不返回成功代碼S_FALSE。 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式成員函數始終返回S_OK以指示成功。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
