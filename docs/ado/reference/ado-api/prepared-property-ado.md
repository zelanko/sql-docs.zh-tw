---
title: 備妥屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7317b6b9a5251c8d104e6c2153ec8c009b2aea7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027803"
---
# <a name="prepared-property-ado"></a>Prepared 屬性 (ADO)
指出是否要儲存已編譯的版本[命令](../../../ado/reference/ado-api/command-object-ado.md)之前執行。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值，如果設定為 **，則為 True**，指出應該準備命令。  
  
## <a name="remarks"></a>備註  
 使用**已準備**屬性，讓儲存的查詢中指定的備妥 （或已編譯） 版本的提供者[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性，才能[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的第一次執行。 這可能會降低命令的第一次執行，但一旦提供者會編譯的命令，提供者會使用編譯的版本的命令的任何後續的執行作業，將會導致更佳的效能。  
  
 如果屬性是**假**，提供者會執行**命令**物件，而建立的已編譯的版本不直接。  
  
 如果提供者不支援命令準備，它就可能會傳回錯誤，當這個屬性設定為 **，則為 True**。 如果提供者不會傳回錯誤，它會完全忽略準備的命令並將設定要求**已準備**屬性設**False**。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Prepared 的屬性範例 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 屬性範例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
