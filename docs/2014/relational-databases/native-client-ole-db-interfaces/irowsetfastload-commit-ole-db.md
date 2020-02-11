---
title: IRowsetFastLoad：： Commit （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e6983eaccf1a934a318c69e72ebdfebf17d2ad9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63224729"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 如需範例，請參閱[使用 IRowsetFastLoad &#40;大量資料複製 OLE DB&#41;](irowsetfastload-ole-db.md) ，並[使用 IRowsetFastLoad 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;將 BLOB 資料傳送到 SQL SERVER ](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *fDone*[in]  
 如果為 FALSE，此資料列集就會維持有效性，而且可供取用者用於其他資料列插入作業。 如果為 TRUE，此資料列集就會喪失有效性，而且取用者無法完成其他插入作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功，而且所有插入的資料都已經寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
 E_FAIL  
 發生了提供者特定的錯誤。 請從提供者中擷取特定錯誤文字的錯誤資訊。  
  
 E_UNEXPECTED  
 這個方法是在先前已藉由 **IRowsetFastLoad::Commit** 方法設為無效之大量複製資料列集上呼叫。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者大量複製資料列集的行為是延遲更新模式資料列集。 因為使用者會透過資料列集插入資料列的資料，所以插入的資料列會以相同的方式被視為支援 **IRowsetUpdate** 之資料列集上的暫止插入。  
  
 取用者必須針對大量複製資料列集呼叫 **Commit** 方法，才能將插入的資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，其方式就如同使用 **IRowsetUpdate::Update** 方法，將暫止資料列提交給 SQL Server 執行個體。  
  
 如果取用者釋放大量複製資料列集的參考，而沒有呼叫 **Commit** 方法，所有先前並未寫入的已插入資料列都會遺失。  
  
 取用者可以呼叫 **Commit** 方法，並將 *fDone* 引數設定為 FALSE，藉以批次處理插入的資料列。 當 *fDone* 設定為 TRUE 時，此資料列集就會成為無效。 無效的大量複製資料列集僅支援 **ISupportErrorInfo** 介面和 **IRowsetFastLoad::Release** 方法。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
