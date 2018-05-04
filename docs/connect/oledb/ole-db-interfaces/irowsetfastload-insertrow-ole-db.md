---
title: 'Irowsetfastload:: Insertrow (OLE DB) |Microsoft 文件'
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e0baa549d302c551f2d5a0fcac90ab533607360b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  將資料列加入至大量複製資料列集。 如需範例，請參閱[大量資料使用 IRowsetFastLoad 大量複製&#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)和[將 BLOB 資料傳送至 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>引數  
 *hAccessor*[in]  
 針對大量複製而定義資料列資料的存取子控制代碼。 所參考的存取子是資料列存取子，會繫結取用者所擁有的記憶體 (內含資料值)。  
  
 *pData*[in]  
 取用者所擁有記憶體 (內含資料值) 的指標。 如需詳細資訊，請參閱[DBBINDING 結構](http://go.microsoft.com/fwlink/?LinkId=65955)。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。 所有資料行的任何繫結狀態值都具有 DBSTATUS_S_OK 或 DBSTATUS_S_NULL 值。  
  
 E_FAIL  
 發生錯誤。 可以從資料列集的錯誤介面取得錯誤資訊。  
  
 E_INVALIDARG  
 *PData*引數已設為 NULL 指標。  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL 無法配置足夠的記憶體來完成要求。  
  
 E_UNEXPECTED  
 在先前被驗證為無效的大量複製資料列集上呼叫此方法[irowsetfastload:: Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)方法。  
  
 DB_E_BADACCESSORHANDLE  
 *HAccessor*取用者提供的引數無效。  
  
 DB_E_BADACCESSORTYPE  
 指定的存取子不是資料列存取子，或未指定取用者所擁有的記憶體。  
  
## <a name="remarks"></a>備註  
 取用者將資料轉換為錯誤[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料行的資料類型會造成 E_FAIL 從傳回 OLE DB 驅動程式的 SQL Server。 資料可以傳輸到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]任何**InsertRow**方法或僅在**認可**方法。 取用者應用程式可以呼叫**InsertRow**多次使用錯誤的資料才會收到通知確認資料類型轉換錯誤存在的方法。 因為**認可**方法可確保，所有的資料已正確指定取用者，取用者可以使用**認可**方法適當地驗證必要的資料。  
  
 SQL Server 大量複製資料列集，OLE DB 驅動程式是唯寫。 SQL Server OLE DB 驅動程式會公開允許取用者資料列集的查詢沒有任何方法。 若要終止處理，取用者可以在釋放其參考[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)介面，而不需呼叫**認可**方法。 沒有功能可用來存取資料列集中取用者插入的資料列並變更其值，或將該資料列從資料列集個別地移除。  
  
 大量複製的資料列會在伺服器上針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 設定格式。 資料列格式會受到已針對連接或工作階段所設定之任何選項 (例如 ANSI_PADDING) 的影響。 適用於 SQL Server 透過 OLE DB 驅動程式進行任何連接的預設值是設定這個選項。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
