---
title: "保存的階層式資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1c4a4fc782bfa6c6130a1acbd45ab1aa2ae3fcd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-hierarchical-recordsets"></a>保存的階層式資料錄集
您可以儲存階層式**資料錄集**藉由呼叫 ADTG 或 XML 格式檔[儲存](../../../ado/reference/ado-api/save-method.md)方法。 不過，兩個限制會套用儲存階層式時**資料錄集**s 以 XML 格式： 如果無法儲存在 XML 中階層式**資料錄集**包含擱置的更新，而且無法儲存參數化階層式**資料錄集**。  
  
 如需資料成形提供者的詳細資訊，請參閱[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) 和[的 OLE DB Data Shaping Service 概觀](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)
