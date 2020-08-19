---
description: Parameter (ADO for Visual C++ 語法)
title: Visual C++ 語法的參數 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Parameter collection [ADO], ADO for Visual C++ syntax
ms.assetid: 74801dc1-cf0f-4a6e-960b-5990fe55e30d
author: rothja
ms.author: jroth
ms.openlocfilehash: d80c216e6e62a523c26c5b9690a8135163873904
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442840"
---
# <a name="parameter-ado-for-visual-c-syntax"></a>Parameter (ADO for Visual C++ 語法)
## <a name="methods"></a>方法  
  
```  
AppendChunk(VARIANT Val)  
```  
  
## <a name="properties"></a>屬性  
  
```  
get_Attributes(LONG *plParmAttribs)  
put_Attributes(LONG lParmAttribs)  
get_Direction(ParameterDirectionEnum *plParmDirection)  
put_Direction(ParameterDirectionEnum lParmDirection)  
get_Name(BSTR *pbstr)  
put_Name(BSTR bstr)  
get_NumericScale(BYTE *pbScale)  
put_NumericScale(BYTE bScale)  
get_Precision(BYTE *pbPrecision)  
put_Precision(BYTE bPrecision)  
get_Size(long *pl)  
put_Size(long l)  
get_Type(DataTypeEnum *psDataType)  
put_Type(DataTypeEnum sDataType)  
get_Value(VARIANT *pvar)  
put_Value(VARIANT val)  
```  
  
## <a name="see-also"></a>另請參閱  
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)
