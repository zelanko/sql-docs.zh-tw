---
title: 資料空間 (ADO-WFC 語法) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160fe6068b86edc5d10f277dbd298954dc37838f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="dataspace-ado---wfc-syntax"></a>資料空間 (ADO-WFC 語法)
**CreateObject**方法**DataSpace**類別會指定這兩個商務物件來處理用戶端應用程式要求 (*progid*) 和通訊協定與伺服器 (*連接*)。 **createObject**傳回[ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md)代表伺服器的物件。  
  
## <a name="package-commswfcdata"></a>封裝 com.ms.wfc.data  
  
### <a name="constructor"></a>建構函式  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>方法  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
