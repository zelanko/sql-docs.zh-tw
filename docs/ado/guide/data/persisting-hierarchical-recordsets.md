---
description: 保存階層式資料錄集
title: 保存階層式記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: rothja
ms.author: jroth
ms.openlocfilehash: 9fef0aad67d6d6cd68f50cc8940e2ddf3c53a206
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980069"
---
# <a name="persisting-hierarchical-recordsets"></a>保存階層式資料錄集
您可以藉由呼叫[save](../../../ado/reference/ado-api/save-method.md)方法，將階層式**記錄集**儲存為 ADTG 或 XML 格式的檔案。 不過，以 XML 格式儲存階層式 **記錄集**時，會套用兩項限制：如果階層式 **記錄集** 包含暫止的更新，您就無法在 xml 中儲存，而且無法儲存參數化階層式 **記錄集**。  
  
 如需資料成形提供者的詳細資訊，請參閱適用 [于 OLE DB 的 Microsoft 資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) 和 [OLE DB 的資料成形服務總覽](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
