---
title: ConnectOptionEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae0f4a06d6c4f25d1d4cb0fb71d6b94a57a07cb2
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277187"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定是否[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件應該會傳回 （同步） 建立連接之後或之前 （非同步）。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以非同步方式開啟連接。 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件可能會用來判斷連線何時可用。|  
|**adConnectUnspecified**|-1|預設值。 以同步方式開啟連接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)
