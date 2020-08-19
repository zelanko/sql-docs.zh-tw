---
description: PageSize 屬性 (ADO)
title: " (ADO) 的 PageSize 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 99365747e5049da4b8dd3cc58f58fd6e2a542e76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442850"
---
# <a name="pagesize-property-ado"></a>PageSize 屬性 (ADO)
指出記錄 [集](../../../ado/reference/ado-api/recordset-object-ado.md)內有多少筆記錄組成一個頁面。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，指出頁面上有多少筆記錄。 預設值為 **10**。  
  
## <a name="remarks"></a>備註  
 您可以使用 **PageSize** 屬性來判斷組成資料邏輯頁面的記錄數目。 建立頁面大小可讓您使用 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 屬性移至特定頁面的第一筆記錄。 當您想要允許使用者逐頁查看資料、一次查看特定的記錄數目時，這項功能就很有用。  
  
 您可以隨時設定這個屬性，其值將用來計算特定頁面之第一筆記錄的位置。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) ](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VC + +) ](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [ (ADO) 的 AbsolutePage 屬性 ](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
