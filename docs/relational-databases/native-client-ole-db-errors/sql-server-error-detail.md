---
title: SQL Server 錯誤詳細資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7eeea46789b52353ade93f1d4836a9e40a3da9e1
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669178"
---
# <a name="sql-server-error-detail"></a>SQL Server 錯誤詳細資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義提供者特有的錯誤介面[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)。 此介面會傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的詳細資料，在命令執行或資料列集作業失敗時非常有用。  
  
 取得 **ISQLServerErrorInfo** 介面存取權的方法有兩種。  
  
 取用者可以呼叫 **IErrorRecords::GetCustomerErrorObject** 來取得 **ISQLServerErrorInfo** 指標，如下列程式碼範例所示 (不需要取得 **ISQLErrorInfo**)。**ISQLErrorInfo** 和 **ISQLServerErrorInfo** 這兩者都是自訂的 OLE DB 錯誤物件，其中 **ISQLServerErrorInfo** 是用來取得伺服器錯誤資訊 (包括程序名稱和行號之類的詳細資料) 的介面。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 另一種取得 **ISQLServerErrorInfo** 指標的方法是在已取得的 **ISQLErrorInfo** 指標上呼叫 **QueryInterface** 方法。 請注意，因為 **ISQLServerErrorInfo** 包含 **ISQLErrorInfo** 所提供資訊的超集，所以透過 **GetCustomerErrorObject** 直接存取 **ISQLServerErrorInfo** 很合理。  
  
 **ISQLServerErrorInfo** 介面會公開一個成員函數 [ISQLServerErrorInfo::GetErrorInfo](../../relational-databases/native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)。 該函數會傳回 SSERRORINFO 結構的指標以及字串緩衝區的指標。 這兩個指標都會參考取用者必須使用 **IMalloc::Free** 方法來取消配置的記憶體。  
  
 SSERRORINFO 結構成員會依下列方式由取用者解譯。  
  
|成員|描述|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息。 與 **IErrorInfo::GetDescription** 中傳回的字串相同。|  
|*pwszServer*|工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|*pwszProcedure*|如果適用，則為發生錯誤之程序的名稱， 否則便為空字串。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生錯誤號碼。 與 **ISQLErrorInfo::GetSQLInfo** 的 *plNativeError* 參數中所傳回的值相同。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息的狀態。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息的嚴重性。|  
|*wLineNumber*|在適用時，這是發生錯誤之預存程序的行號。|  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
