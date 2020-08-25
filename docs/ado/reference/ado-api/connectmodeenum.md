---
description: ConnectModeEnum
title: ConnectModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: rothja
ms.author: jroth
ms.openlocfilehash: 10bc68683f337f5a0bdf6fc5679c4276925a4234
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775847"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定在[連接](./connection-object-ado.md)中修改資料、開啟[記錄](./record-object-ado.md)，或針對**記錄**和[資料流程](./stream-object-ado.md)物件的[Mode](./mode-property-ado.md)屬性指定值的可用許可權。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|表示唯讀許可權。|  
|**adModeReadWrite**|3|表示讀取/寫入權限。|  
|**adModeRecursive**|0x400000|與其他* \* ShareDeny \* *值一起使用 (**adModeShareDenyNone**、 **adModeShareDenyWrite**或**adModeShareDenyRead**) ，以將共用限制傳播至目前**記錄**的所有子記錄。 如果 **記錄** 沒有任何子系，則不會有任何影響。 如果只與 **adModeShareDenyNone** 搭配使用，就會產生執行階段錯誤。 不過，它可以搭配使用 **adModeShareDenyNone** 與其他值。 例如，您可以使用 "**adModeRead** " 或 [ **adModeShareDenyNone** ] 或 [ **adModeRecursive**]。|  
|**adModeShareDenyNone**|16|允許其他人開啟具有任何許可權的連接。 無法拒絕他人的讀取或寫入權限。|  
|**adModeShareDenyRead**|4|防止其他人開啟具有讀取權限的連接。|  
|**adModeShareDenyWrite**|8|防止其他人開啟具有寫入權限的連接。|  
|**adModeShareExclusive**|12|防止其他人開啟連接。|  
|**adModeUnknown**|0|預設值。 指出尚未設定或無法判斷許可權。|  
|**adModeWrite**|2|表示僅限寫入的許可權。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. ConnectMode. 讀取|  
|AdoEnums. ConnectMode|  
| (沒有對等的 AdoEnums ConnectMode。遞迴) |  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode。未知|  
|AdoEnums. ConnectMode 寫|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Mode 屬性 (ADO)](./mode-property-ado.md)  
        [Open 方法 (ADO Record)](./open-method-ado-record.md)  
    :::column-end:::
    :::column:::
        [Open 方法 (ADO Stream)](./open-method-ado-stream.md)  
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::