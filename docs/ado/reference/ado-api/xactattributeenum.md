---
description: XactAttributeEnum
title: XactAttributeEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c7ea7ccbf1a588458db9e213bfa57837e89898f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776817"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
指定 [連接](./connection-object-ado.md) 物件的交易屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|藉由呼叫 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留中止。 並非所有提供者都支援此行為。|  
|**adXactCommitRetaining**|131072|藉由呼叫 [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 來自動啟動新的交易，以執行保留認可。 並非所有提供者都支援此行為。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](./attributes-property-ado.md)