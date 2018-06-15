---
title: 'Irowsetfastload:: Commit (OLE DB) |Microsoft 文件'
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ad752273420523a9f8a72db01b8c3053a5b05bfb
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306127"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 如需範例，請參閱[大量資料使用 IRowsetFastLoad 大量複製&#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)和[將 BLOB 資料傳送至 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
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
 在先前被驗證為無效的大量複製資料列集上呼叫此方法**irowsetfastload:: Commit**方法。  
  
## <a name="remarks"></a>備註  
 SQL Server 大量複製資料列集 OLE DB 驅動程式的行為如同延遲更新模式的資料列集。 因為使用者會透過資料列集的資料列資料，插入的資料列會被視為相同的方式暫止插入資料列集支援**IRowsetUpdate**。  
  
 取用者必須呼叫**認可**方法寫入插入的資料列大量複製資料列集上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表中的相同方式**irowsetupdate:: Update**方法用來提交暫止的資料列SQL Server 執行個體。  
  
 如果取用者釋放大量複製資料列集，而不會呼叫其參考**認可**方法，所有插入先前並未寫入的資料列都會遺失。  
  
 取用者可以藉由呼叫批次處理插入的資料列**認可**方法*fDone*引數設定為 FALSE。 當*fDone*是設為 TRUE，資料列集就會變成無效。 無效的大量複製的資料列集僅支援**ISupportErrorInfo**介面和**irowsetfastload:: Release**方法。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
