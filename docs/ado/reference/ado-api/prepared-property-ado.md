---
title: 備妥屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 452777c142b01b21a258e6f5432c48b243d45a40
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="prepared-property-ado"></a>已備妥的屬性 (ADO)
指出是否要儲存已編譯的版本[命令](../../../ado/reference/ado-api/command-object-ado.md)之前執行。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值，如果設定為**True**，指出應該準備此命令。  
  
## <a name="remarks"></a>備註  
 使用**已準備**屬性，讓儲存在指定的查詢已備妥 （或編譯） 版本的提供者[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性之後再[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的第一次執行。 這可能會降低命令的第一次執行，但一旦提供者會編譯的命令，提供者會使用命令的已編譯的版本供任何後續執行，將會提高效能。  
  
 如果屬性是**False**，提供者會執行**命令**物件直接建立編譯的版本。  
  
 如果提供者不支援命令準備，它就可能會傳回錯誤，當這個屬性設定為**True**。 如果提供者不會傳回錯誤，它只會忽略準備的命令並將設定要求**已準備**屬性**False**。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [已備妥的屬性範例 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 屬性範例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
