---
title: 'IRowsetFastLoad:: Commit (OLE DB) |Microsoft Docs'
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d76ad5dc881ab4f31808d738d9beacd85929d279
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994406"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 如需範例, 請參閱[使用 IRowsetFastLoad &#40;OLE DB&#41;大量資料複製](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md), 並[使用 IRowsetFastLoad 和&#40;ISEQUENTIALSTREAM OLE DB&#41;將 BLOB 資料傳送到 SQL SERVER](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>引數  
 *fDone*[in]  
 如果為 FALSE，此資料列集就會維持有效性，而且可供取用者用於其他資料列插入作業。 如果為 TRUE，此資料列集就會喪失有效性，而且取用者無法完成其他插入作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功，而且所有插入的資料都已經寫入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中。  
  
 E_FAIL  
 發生了提供者特定的錯誤。 請從提供者中擷取特定錯誤文字的錯誤資訊。  
  
 E_UNEXPECTED  
 這個方法是在先前已藉由 **IRowsetFastLoad::Commit** 方法設為無效之大量複製資料列集上呼叫。  
  
## <a name="remarks"></a>Remarks  
 SQL Server 大量複製資料列集的 OLE DB 驅動程式會以延遲更新模式資料列集的形式運作。 因為使用者會透過資料列集插入資料列的資料，所以插入的資料列會以相同的方式被視為支援 **IRowsetUpdate** 之資料列集上的暫止插入。  
  
 取用者必須針對大量複製資料列集呼叫 **Commit** 方法，才能將插入的資料列寫入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中，其方式就如同使用 **IRowsetUpdate::Update** 方法，將暫止資料列提交給 SQL Server 執行個體。  
  
 如果取用者釋放大量複製資料列集的參考，而沒有呼叫 **Commit** 方法，所有先前並未寫入的已插入資料列都會遺失。  
  
 取用者可以呼叫 **Commit** 方法，並將 *fDone* 引數設定為 FALSE，藉以批次處理插入的資料列。 當 *fDone* 設定為 TRUE 時，此資料列集就會成為無效。 無效的大量複製資料列集僅支援 **ISupportErrorInfo** 介面和 **IRowsetFastLoad::Release** 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
