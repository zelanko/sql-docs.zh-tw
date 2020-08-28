---
description: Collections (ADO - WFC 語法)
title: 集合 (ADO-WFC 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
author: rothja
ms.author: jroth
ms.openlocfilehash: a6afa603b169949673544791849ecbbc5d312cfb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975339"
---
# <a name="collections-ado---wfc-syntax"></a>Collections (ADO - WFC 語法)
**封裝 .com. 資料**  
  
## <a name="parameters"></a>參數  
  
### <a name="methods"></a>方法  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>欄位  
  
### <a name="methods"></a>方法  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>Errors  
  
### <a name="methods"></a>方法  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 收集錯誤 ](./errors-collection-ado.md)   
 [ (ADO) 的欄位集合 ](./fields-collection-ado.md)   
 [Parameters 集合 (ADO)](./parameters-collection-ado.md)