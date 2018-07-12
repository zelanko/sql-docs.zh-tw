---
title: 'Irowsetfastload:: Commit (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 745282c1d1e8fa36c9d0a407ac32171304d05197
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417167"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 如需範例，請參閱[大量複製資料檔案 _ 使用 IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md)並[將 BLOB 資料傳送到 SQL SERVER 使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
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
 先前失效的大量複製資料列集上呼叫方法**irowsetfastload:: Commit**方法。  
  
## <a name="remarks"></a>備註  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者大量複製資料列集行為會如同延遲更新模式的資料列集。 因為使用者會透過資料列集的資料列資料，插入的資料列會以相同方式處理暫止插入資料列集，支援**IRowsetUpdate**。  
  
 取用者必須呼叫**認可**大量複製資料列集，將插入的資料列上的方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表中的相同方式來**irowsetupdate:: Update**方法用來提交暫止的資料列SQL Server 執行個體。  
  
 如果取用者釋放大量複製資料列集，而不需呼叫的參考**認可**方法中，所有插入先前並未寫入的資料列都會遺失。  
  
 取用者可以藉由呼叫批次處理插入的資料列**認可**方法*fDone*引數設定為 FALSE。 當*fDone*是設為 TRUE，資料列集就會變成無效。 無效的大量複製資料列集僅支援**ISupportErrorInfo**介面並**irowsetfastload:: Release**方法。  
  
## <a name="see-also"></a>另請參閱  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
