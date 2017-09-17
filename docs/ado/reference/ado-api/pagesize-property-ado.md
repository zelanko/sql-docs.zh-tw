---
title: "PageSize 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fde7e53b844ece01f85b7ecba7e309a71107029d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pagesize-property-ado"></a>PageSize 屬性 (ADO)
表示構成的多少筆記錄中的每一頁[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，指出是否在頁面上的多少筆記錄。 預設值是**10**。  
  
## <a name="remarks"></a>備註  
 使用**PageSize**屬性來判斷多少筆記錄組成一個邏輯頁面的資料。 建立頁面大小可讓您使用[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)移至特定頁面的第一個記錄的屬性。 當您想要讓使用者逐頁查看資料，一次檢視的記錄數目，這是 Web 伺服器案例中很有用。  
  
 這個屬性可以設定在任何時間，而且其值會用於計算特定的頁面上第一筆記錄的位置。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

