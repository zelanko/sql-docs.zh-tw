---
title: 已備妥的屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917593"
---
# <a name="prepared-property-ado"></a>Prepared 屬性 (ADO)
指出是否要在執行之前儲存已編譯版本的[命令](../../../ado/reference/ado-api/command-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值，如果設定為**True**，則表示應該準備命令。  
  
## <a name="remarks"></a>備註  
 使用已**備**妥的屬性，讓提供者在[命令](../../../ado/reference/ado-api/command-object-ado.md)物件第一次執行之前，儲存[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性中指定之查詢的備妥（或已編譯）版本。 這可能會使命令的第一次執行速度變慢，但一旦提供者編譯命令，提供者將會使用命令的編譯版本進行任何後續的執行，這樣會導致效能提升。  
  
 如果屬性為**False**，則提供者會直接執行**命令**物件，而不會建立已編譯的版本。  
  
 如果提供者不支援命令準備，當這個屬性設定為**True**時，它可能會傳回錯誤。 如果提供者未傳回錯誤，它只會忽略準備命令的要求，並將**備**妥的屬性設定為**False**。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [備妥的屬性範例（VB）](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 屬性範例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
