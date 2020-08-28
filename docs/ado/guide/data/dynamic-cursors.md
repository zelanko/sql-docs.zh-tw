---
description: 動態資料指標
title: 動態資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: rothja
ms.author: jroth
ms.openlocfilehash: e8ce85233cec96af3d804652225b4d14698287db
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991349"
---
# <a name="dynamic-cursors"></a>動態資料指標
動態資料指標會偵測結果集中對資料列所做的所有變更，不論變更是從資料指標內部或資料指標以外的其他使用者進行。 所有使用者所做的所有 insert、update 和 delete 語句都可以透過資料指標來顯示。 動態資料指標可以偵測在開啟資料指標之後，對結果集內的資料列、順序和值所做的任何變更。 除非資料指標交易隔離等級設定為「未認可」 ) ，否則在資料指標外部進行的更新將不會顯示，直到認可為止 (。  
  
 例如，假設動態資料指標提取兩個數據列和另一個應用程式，然後更新其中一個資料列並刪除另一個。 如果動態資料指標之後擷取這些資料列，它會找不到已刪除的資料列，但會顯示已更新資料列的新值。  
  
 如果您的應用程式必須偵測其他使用者所做的所有並行更新，動態資料指標就是很好的選擇。 使用 **AdOpenDynamic CursorTypeEnum** 來指出您想要在 ADO 中使用動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](./forward-only-cursors.md)   
 [靜態資料指標](./static-cursors.md)   
 [索引鍵集資料指標](./keyset-cursors.md)