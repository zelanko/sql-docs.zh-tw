---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2098830a06f8e5c2ddc38b12f0c035ec513433ca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206304"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定的交易屬性[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|會保留中止執行藉由呼叫[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)自動啟動新的交易。 並非所有提供者支援這個行為。|  
|**adXactCommitRetaining**|131072|藉由呼叫執行保留認可[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)自動啟動新的交易。 並非所有提供者支援這個行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>適用於  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
