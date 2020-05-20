---
title: 空間（ADO-WFC 語法） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: rothja
ms.author: jroth
ms.openlocfilehash: c736dc38949945a6e62e5121c4edf4b98dfbc7fc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763449"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO - WFC 語法)
「**空間**」類別的**createObject**方法會指定商務物件來處理用戶端應用程式要求（*progid*）和通訊協定和伺服器（*連接*）。 **createObject**會傳回代表伺服器的[ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md)物件。  
  
## <a name="package-commswfcdata"></a>封裝 .com. wfc. 資料  
  
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
