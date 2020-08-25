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
ms.openlocfilehash: 2c073d0ef7cceb74864b7f526ef9a5283ca946a7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773527"
---
# <a name="pagesize-property-ado"></a>PageSize 屬性 (ADO)
指出記錄 [集](./recordset-object-ado.md)內有多少筆記錄組成一個頁面。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，指出頁面上有多少筆記錄。 預設值為 **10**。  
  
## <a name="remarks"></a>備註  
 您可以使用 **PageSize** 屬性來判斷組成資料邏輯頁面的記錄數目。 建立頁面大小可讓您使用 [AbsolutePage](./absolutepage-property-ado.md) 屬性移至特定頁面的第一筆記錄。 當您想要允許使用者逐頁查看資料、一次查看特定的記錄數目時，這項功能就很有用。  
  
 您可以隨時設定這個屬性，其值將用來計算特定頁面之第一筆記錄的位置。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) ](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VC + +) ](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [ (ADO) 的 AbsolutePage 屬性 ](./absolutepage-property-ado.md)   
 [PageCount 屬性 (ADO)](./pagecount-property-ado.md)