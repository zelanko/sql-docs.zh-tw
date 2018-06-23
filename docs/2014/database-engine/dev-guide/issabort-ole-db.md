---
title: ISSAbort (OLE DB) |Microsoft 文件
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
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 53c6e2c7c06331ce75883f86a8935d4d1c2419c4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032825"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  **ISSAbort**介面中公開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，提供[issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)方法用來取消目前的資料列集加上任何命令批次使用命令一開始會產生資料列集，並可對尚未完成執行。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 提供者特定介面，可以使用**QueryInterface**上**IMultipleResults**所傳回物件**Icommand:: Execute**或**iopenrowset:: Openrowset**。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|描述|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  