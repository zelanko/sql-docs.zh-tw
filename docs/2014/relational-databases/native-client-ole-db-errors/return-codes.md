---
title: 傳回碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dd033d16b1e95773d2cab1c4e1fca733dc491b96
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048063"
---
# <a name="return-codes"></a>傳回碼
  在大部分的基本層級，成員函數不是成功就是失敗。 在更精確一點的層級，函數可能會成功，但是其成功可能不是應用程式開發人員所樂見的。  
  
 如需 OLE DB 傳回碼的詳細資訊，請參閱 [Return Codes (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631) (傳回碼 (OLE DB))。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者成員函式傳回 S_OK 時，函數會成功。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者成員函式未傳回 S_OK 時，OLE/COM HRESULT 解除封裝失敗，而 IS_ERROR 宏可以判斷函式的整體成功或失敗。  
  
 如果 FAILED 或 IS_ERROR 傳回 TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者就能確保成員函式執行失敗。 當 FAILED 或 IS_ERROR 傳回 FALSE，而且 HRESULT 不等於 S_OK 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者可確保函數在某種意義上會成功。 取用者可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者錯誤介面，取得此「具有資訊的成功」傳回的詳細資訊。 此外，在函式明確失敗的情況下（FAILED 宏會傳回 TRUE），可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者錯誤介面取得擴充的錯誤資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者取用者通常會遇到「具有資訊的成功」 HRESULT 傳回的 DB_S_ERRORSOCCURRED。 傳回 DB_S_ERRORSOCCURRED 的成員函數通常會定義一或多個可提供狀態值給取用者的參數。 取用者無法取得在狀態值參數中傳回之錯誤資訊以外的錯誤資訊，因此取用者應該在可取得錯誤資訊時，實作應用程式邏輯來擷取狀態值。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者成員函式不會傳回成功的程式碼 S_FALSE。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者成員函式一律會傳回 S_OK 以表示成功。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](errors.md)  
  
  
