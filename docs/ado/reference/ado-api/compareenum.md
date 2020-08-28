---
description: CompareEnum
title: CompareEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareEnum
helpviewer_keywords:
- CompareEnum enumeration [ADO]
ms.assetid: bc8f710d-0621-4673-8d8e-0361e44abed0
author: rothja
ms.author: jroth
ms.openlocfilehash: a5a983f1808d71404279c5332aedfcfb1f1501d5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975019"
---
# <a name="compareenum"></a>CompareEnum
指定兩筆記錄以其書簽表示的相對位置。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adCompareEqual**|1|指出書簽相等。|  
|**adCompareGreaterThan**|2|指出第一個書簽是在第二個書簽之後。|  
|**adCompareLessThan**|0|指出第一個書簽是在第二個書簽之前。|  
|**adCompareNotComparable**|4|表示無法比較書簽。|  
|**adCompareNotEqual**|3|指出書簽不相等且未排序。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums，比較. 等於|  
|AdoEnums. GREATERTHAN|  
|AdoEnums. LESSTHAN|  
|AdoEnums. NOTCOMPARABLE|  
|AdoEnums. NOTEQUAL|  
  
## <a name="applies-to"></a>套用至  
 [CompareBookmarks 方法 (ADO)](./comparebookmarks-method-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CompareBookmarks 方法 (ADO)](./comparebookmarks-method-ado.md)