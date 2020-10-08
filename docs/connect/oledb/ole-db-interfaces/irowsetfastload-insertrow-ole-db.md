---
title: IRowsetFastLoad::InsertRow (OLE DB Driver) | Microsoft Docs
description: 了解 IRowsetFastLoad::InsertRow 方法如何將資料列新增至 OLE DB Driver for SQL Server 中的大量複製資料列集。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a631a9385b323b3b8b8ac0d276ff9eb2d560ef3
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726927"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  將資料列加入至大量複製資料列集。 如需範例，請參閱[使用 IRowsetFastLoad 大量複製資料 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) 和[使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
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
 取用者所擁有記憶體 (內含資料值) 的指標。 如需詳細資訊，請參閱 [DBBINDING 結構](/previous-versions/windows/desktop/ms716845(v=vs.85))。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。 所有資料行的任何繫結狀態值都具有 DBSTATUS_S_OK 或 DBSTATUS_S_NULL 值。  
  
 E_FAIL  
 發生錯誤。 可以從資料列集的錯誤介面取得錯誤資訊。  
  
 E_INVALIDARG  
 *pData* 引數已設為 NULL 指標。  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL 無法配置足夠的記憶體來完成要求。  
  
 E_UNEXPECTED  
 這個方法是在先前已藉由 [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) 方法設為無效之大量複製資料列集上呼叫。  
  
 DB_E_BADACCESSORHANDLE  
 取用者所提供的 *hAccessor* 引數無效。  
  
 DB_E_BADACCESSORTYPE  
 指定的存取子不是資料列存取子，或未指定取用者所擁有的記憶體。  
  
## <a name="remarks"></a>備註  
 將取用者資料轉換成資料行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型時發生的錯誤會導致 OLE DB Driver for SQL Server 傳回 E_FAIL。 您可在任何 **InsertRow** 方法或僅在 **Commit** 方法上將資料傳輸至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 取用者應用程式可能會在使用錯誤的資料呼叫 **InsertRow** 方法很多次後，才收到發生了資料類型轉換錯誤的通知。 因為 **Commit** 方法會確保所有資料都由取用者正確指定，所以取用者可依需要適當地使用 **Commit** 方法來驗證資料。  
  
 OLE DB Driver for SQL Server 大量複製資料列集是唯寫的。 OLE DB Driver for SQL Server 沒有公開任何允許取用者查詢資料列集的方法。 若要終止處理，取用者可以不必呼叫 **Commit** 方法，即釋放它在 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 介面上的參考。 沒有功能可用來存取資料列集中取用者插入的資料列並變更其值，或將該資料列從資料列集個別地移除。  
  
 大量複製的資料列會在伺服器上針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 設定格式。 資料列格式會受到已針對連接或工作階段所設定之任何選項 (例如 ANSI_PADDING) 的影響。 根據預設，針對透過 OLE DB Driver for SQL Server 所建立的任何連線，此選項皆設定為開啟。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
