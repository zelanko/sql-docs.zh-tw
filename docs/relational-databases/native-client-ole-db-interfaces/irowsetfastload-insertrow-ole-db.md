---
title: IRowsetFastLoad::InsertRow (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c178f2e948e27b964b04f62508ec35038b204576
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307267"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  將資料列加入至大量複製資料列集。 如需範例，請參閱[使用 IRowsetFastLoad 大量複製資料 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) 和[使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
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
 取用者所擁有記憶體 (內含資料值) 的指標。 如需詳細資訊，請參閱 [DBBINDING 結構](https://go.microsoft.com/fwlink/?LinkId=65955)。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。 所有資料行的任何繫結狀態值都具有 DBSTATUS_S_OK 或 DBSTATUS_S_NULL 值。  
  
 E_FAIL  
 發生錯誤。 可以從資料列集的錯誤介面取得錯誤資訊。  
  
 E_INVALIDARG  
 *pData* 引數已設為 NULL 指標。  
  
 E_OUTOFMEMORY  
 SQLNCLI11 無法配置足夠的記憶體來完成要求。  
  
 E_UNEXPECTED  
 這個方法是在先前已藉由 [IRowsetFastLoad::Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) 方法設為無效之大量複製資料列集上呼叫。  
  
 DB_E_BADACCESSORHANDLE  
 取用者所提供的 *hAccessor* 引數無效。  
  
 DB_E_BADACCESSORTYPE  
 指定的存取子不是資料列存取子，或未指定取用者所擁有的記憶體。  
  
## <a name="remarks"></a>備註  
 將消費者數據轉換為列的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型時出錯,會導致從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式返回E_FAIL。 您可在任何 **InsertRow** 方法或僅在 **Commit** 方法上將資料傳輸至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 取用者應用程式可能會在使用錯誤的資料呼叫 **InsertRow** 方法很多次後，才收到發生了資料類型轉換錯誤的通知。 因為 **Commit** 方法會確保所有資料都由取用者正確指定，所以取用者可依需要適當地使用 **Commit** 方法來驗證資料。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE DB 提供程式批量複製列集僅寫入。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者不公開任何允許對行集進行使用者查詢的方法。 若要終止處理，取用者可以不必呼叫 **Commit** 方法，即釋放它在 [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 介面上的參考。 沒有功能可用來存取資料列集中取用者插入的資料列並變更其值，或將該資料列從資料列集個別地移除。  
  
 大量複製的資料列會在伺服器上針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定格式。 資料列格式會受到已針對連接或工作階段所設定之任何選項 (例如 ANSI_PADDING) 的影響。 默認情況下,對於透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式進行的任何連接,此選項處於打開狀態。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
