---
title: ConnectOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9df3fd695e9bf281133dabf436e5e8b5de7e0b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646616"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定是否[開放](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件應該會傳回 （同步） 建立連線之後或之前 （非同步）。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以非同步方式開啟連接。 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件可用來判斷連線何時可用。|  
|**adConnectUnspecified**|-1|預設值。 以同步方式開啟連接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)
