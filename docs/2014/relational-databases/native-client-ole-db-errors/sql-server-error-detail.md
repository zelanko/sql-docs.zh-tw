---
title: SQL Server 錯誤詳細資料 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cbbf2365603998edabe58a01de840f2969a8c263
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133939"
---
# <a name="sql-server-error-detail"></a>SQL Server 錯誤詳細資料
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義提供者特有的錯誤介面[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)。 此介面會傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的詳細資料，在命令執行或資料列集作業失敗時非常有用。  
  
 有兩種方式以取得存取權**ISQLServerErrorInfo**介面。  
  
 取用者可以呼叫**ierrorrecords:: Getcustomererrorobject**取得**ISQLServerErrorInfo**指標，如下列程式碼範例所示。 (沒有不需要取得**ISQLErrorInfo。**)同時**ISQLErrorInfo**和**ISQLServerErrorInfo**是自訂的 OLE DB 錯誤物件，其中**ISQLServerErrorInfo**被用來取得資訊的介面伺服器錯誤，包括程序名稱和行號之類的詳細資料。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 若要取得另一種方式**ISQLServerErrorInfo**指標就是呼叫**QueryInterface**方法已取得**ISQLErrorInfo**指標。 請注意，因為**ISQLServerErrorInfo**包含的可用資訊的超集**ISQLErrorInfo**，直接前往合理**ISQLServerErrorInfo**透過**Isqlservererrorinfo**。  
  
 **ISQLServerErrorInfo**介面會公開一個成員函式， [isqlservererrorinfo:: Geterrorinfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)。 該函數會傳回 SSERRORINFO 結構的指標以及字串緩衝區的指標。 這兩個指標參考記憶體取用者必須解除配置使用**imalloc:: Free**方法。  
  
 SSERRORINFO 結構成員會依下列方式由取用者解譯。  
  
|成員|描述|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息。 在傳回的字串相同**ierrorinfo:: Getdescription**。|  
|*pwszServer*|工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|*pwszProcedure*|如果適用，則為發生錯誤之程序的名稱， 否則便為空字串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生錯誤號碼。 在傳回的值相同*isqlerrorinfo:: Getsqlinfo*參數 **:: Getsqlinfo<**。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息的狀態。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息的嚴重性。|  
|*wLineNumber*|在適用時，這是發生錯誤之預存程序的行號。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
