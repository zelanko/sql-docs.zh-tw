---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0d4c765b774faf88ef36d24ec33d1d762d26d0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定是否[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件應該會傳回 （同步） 建立連接之後或之前 （非同步）。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以非同步方式開啟連接。 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件可能會用來判斷連線何時可用。|  
|**adConnectUnspecified**|-1|預設值。 以同步方式開啟連接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)
